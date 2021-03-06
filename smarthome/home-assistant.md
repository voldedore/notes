# Home assistant learning log

## Hass.io

Hass.io là image được build cho RPI nhờ vào resin.io, tức là sau khi burn sẽ connect vào một container được chạy qua docker của RPI.

Hassbian là OS raspbian có cài home assistant vào.

1.  **Installation**

- Download from the github repo the ready-to-be-burnt image. There are a wide range of available images.
- Use etcher.io to burn the just downloaded image.
- Plug the card to a PC, mount the hass-boot (or something like that). Create a CONFIG folder, then network, then touch a `my-network` file. Bref: `CONFIG/network/my-network`.
- Follow the guide: https://github.com/home-assistant/hassos/blob/dev/Documentation/network.md
- The wifi and static ip network should be configured:

      [connection]
      id=hassos-network
      uuid=72111c67-4a5d-4d5c-925e-f8ee26efb3c3
      type=802-11-wireless

      [802-11-wireless]
      mode=infrastructure
      ssid=MY_SSID
      # Uncomment below if your SSID is not broadcasted
      #hidden=true

      [802-11-wireless-security]
      auth-alg=open
      key-mgmt=wpa-psk
      psk=MY_WLAN_SECRET_KEY

      [ipv4]
      method=manual
      address=192.168.1.111/24,192.168.1.1
      dns=8.8.8.8;8.8.4.4;

      [ipv6]
      addr-gen-mode=stable-privacy
      method=auto

- Insert sd card to the rpi.
- The rpi should boot up and provide an http access from http://the-rpi-ip:8123
- This will update the hass OS (in about 20min, as the banner says)

2. **First-time config**

- Provide some initial user information: Fullname, username, password...

- Enable SSH:

  - Go to addons store (Hamburger > Hass.io > Add-ons store). Then look for SSH server.
  - Install it and provide your ssh public key to the middle of the config:

        {
          "authorized_keys": [
            "ssh-rsa adsad== your-key"
          ],
          "password": ""
        }

  - That would add the public key to the root user on the hassio.
  - Then start the SSH service.
  - Test it by `ssh root@ip`
  - After successfully connecting to the hassio, cd to `/config`, this directory contains all the configuration files of the hassos.

3. **configuration.yml**

The file is structure like:

    component_type:
      - some options

Eg

    device_tracker
      - platform: nmap...

Check the file syntax by Hamburger > Config > Check config

After editing the config, the hass os must be restart for enabling the configuration.

4. **Presence detection**

Declare some zone:

configuration.yml

    # Declaration of some zones
    zone:
      - name: 402
        latitude: 10.354004
        longitude: 106.399291
        icon: mdi:home

Enable some `device_tracker` component by adding this to the end (or somewhere else) of the `configuration.yml`

    # Presence detection component
    device_tracker:
      - platform: nmap_tracker
        hosts: 192.168.1.0/24

Some 'random' devices will appears in the homepage. After the `device_tracker` component is enabled, it will automatically create a `known_devices.yml` file in the same location of the configuration file.

5. Connect to Apple HomeKit

The component will transfer all things in the HA to your Home app

- Add the following code to the config file

      # Config for HomeKit component

      homekit:

- Well, there are a lot more option, those are optional though. Check [here](https://www.home-assistant.io/components/homekit/) for more details. Save it and restart the pi.

- In the home page, there should be a HomeKit card displaying 8-digit pin code.

- Open your Home app in the iDevices.
- Add accessory. Select Home Assistant Bridge. Enter pin code.

- Everytime you add a new component in the HA, that component (or accessory) should be automatically added into the HomeKit app too.

6. Switch

- Add current 'virtual' switch:

      # Switch component
      switch:
        - platform: command_line
          switches:
            test_sw:
              command_on: echo `date`on >> /config/test_sw.txt
              command_off: echo `date`off >> /config/test_sw.txt
              friendly_name: Test switch

- Restart HA
- In homepage of HA, there should be a new card of Test switch card.
- In the Home app, there also should be a new switch.
- Test the switch by

      tail -f config/test_sw.txt

- Then turn the switch on/off several times.

7. voice cmd

- This is interesting... and I really meant it.
- In the Home app. Create new Scene and what you name it matters!
- For french spearkers, I, e.g, named it "Je m'en vais", adding my test switch above with the off position. Save the things.
- tail -f /config/test_sw.txt
- Open siri then says: Je m'en vais.
- In the log file should be a new line showing that the switch is turned off.

TODO: add some condition to scene: If I head home in the evening (when the sun is set), then turn the lights on, no need to pay extra electric for the idea when returning home in the mid of the day.

CHưa thể control 1 cách từ xa qua Home app được (lúc này k bắt được cái bridge - một component của HA, HomeKit component), ddns có thể xử lý được?

---

Cách dùng shell_command

Không dùng trực tiếp mpv được mà phải dùng thông qua 1 file shell, sau đó `/bin/sh file_shell.sh`

---

## Hassbian

Khi cài hassbian xong, OS sẽ tự install cái home assistant, nhưng có thể phải tùy chỉnh 1 số thứ như

1. Static IP (`/etc/dhcpcd.conf`)
2. DNS

Vì k có DNS nên phần install lúc đầu sẽ bị fail. Sau đó phải install lại phần này bằng lệnh

    sudo hassbian-config install homêassistant

Xem danh sách bằng cách

    sudo hassbian-config show

Để xài HomeKit phải cài thêm

    sudo journalctl -fu home-assistant@homeassistant.service

Xem log của service tại

    sudo journalctl -fu home-assistant@homeassistant.service

## mpv

Để xài được `mpv`, user phải được add vào group `audio` (raspberry pi 3 & raspbian)

## Radio (streaming), mpd (media player daemon)

Cài gói `mpd` vào.

Sau đó, phải tạo 1 cái select box chứa các đài, và khai báo một `media_player`:

File `configuration.yaml`:

    # Input select
    input_select:
      radio_station:
        name: Radio Station
        options:
          - None
          - VOV1
          - VOV3
        initial: None
        icon: mdi:radio

    # Media player
    media_player:
      - platform: mpd
        host: localhost

Lúc này sẽ xuất hiện 1 cái select box trong dashboard. Để lấy event (triggered) khi chọn option của select, phải thêm vào 1 automation bắt khi chọn cái state của `input_select` đó:

File `automation.yaml`:

    - id: '3'
      alias: Stop Streaming Radio
      trigger:
        platform: state
        entity_id: input_select.radio_station
        to: "None"
      action:
        service: media_player.turn_off

    - id: '4'
      alias: Stream Radio - Template
      trigger:
        - platform: state
          entity_id: input_select.radio_station
      action:
        - service: media_player.play_media
          data_template:
            media_content_id: >
                {% if is_state("input_select.radio_station", "VOV1") %}
                  https://5a6872aace0ce.streamlock.net/nghevov1/vov1.stream_aac/chunklist_w968906280.m3u8
                {%-elif is_state("input_select.radio_station", "VOV3") %}
                  https://5a6872aace0ce.streamlock.net/nghevov3/vov3.stream_aac/playlist.m3u8
                {% else %}
                  none
                {% endif %}
            media_content_type: music
