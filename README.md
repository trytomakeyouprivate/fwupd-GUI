# fwupd GUI
A simple systemd service using Zenity and notify-send to notify users about firmware updates.

Goal of this project: Remove dependency from bloated software stores for an easy GUI firmware update integration. It should be essential for everyone to apply them as fast as possible. As it is a rather invasive process, it needs user interaction.

![grafik](https://github.com/trytomakeyouprivate/fwupd-GUI/assets/113100745/9583d325-3afb-44da-92e6-7c3a7d1cf48d)

Try it:

```
sudo wget https://github.com/trytomakeyouprivate/fwupd-GUI/raw/main/99-charged.rules -P /etc/udev/rules.d &&\
sudo wget https://github.com/trytomakeyouprivate/fwupd-GUI/raw/main/firmwareupdate -P /etc/ &&\
sudo wget https://github.com/trytomakeyouprivate/fwupd-GUI/raw/main/charged.service -P /etc/systemd/system &&\
sudo wget https://github.com/trytomakeyouprivate/fwupd-GUI/raw/main/firmwareupdate.service -P /etc/systemd/system &&\
sudo wget https://github.com/trytomakeyouprivate/fwupd-GUI/raw/main/firmwareupdate.timer -P /etc/systemd/system &&\
sudo systemctl enable firmwareupdate.service && echo "Firmware updater installed"
```

Idea:

- a udev rule checks if A: the user is attached to AC or B: the user has over 70% battery life (this should cover Desktop and laptop users)
- the udev rule activates a systemd unit that indicates a secure state to execute updates
- the timer will then start and run the service
- the service runs a bash script stored as /etc/firmwareupdate
- the bash script checks if there are available updates, reformats the output and shows available devices in a zenity dialog. The user has the opportunity to update via the GUI or to skip the update. A message informs how to update manually
- When skipped the service runs the next day again. 
- If there are no updates the memory load will be minimal and the service will be silent all the time


ToDo:

- testing, troubleshooting
- fixing systemctl enabling
- testing fwupdmgr output reformatting
- testing no-action scenarios
- fixing buttons in zenity
- writing a noninvasive log about successful update checks with none available

Contributions welcome!
