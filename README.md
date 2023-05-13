# fwupd-GUI
A simple systemd service using Zenity and notify-send to notify users about firmware updates.

Idea:

- a udev rule checks if A the user is attached to AC or B the user has over 70% battery life
- the udev rule activates a systemd unit that indicates a secure state to execute updates
- the timer will then start and run the service
- the service runs a bash script stored in /etc/firmwareupdate
- the bash script checks if there are available updates, reformats the output and shows available devices in a zenity dialog. The user has the opportunity to update via the GUI or to skip the update


ToDo:

- make sure the service checks for updates as soon as power is connected
- make sure "skip" only waits 24h and the next day the user is notified again
- cleanup the script, documentation, testing
