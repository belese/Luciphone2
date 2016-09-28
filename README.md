# Luciphone2

## Installation :

on a raspbian minimal image

- Login as root
```
sudo -i
```
- Install dependencies
```
sudo apt-get install policykit-1, python-pymedia
```
- Install [PhatDac sound card](https://learn.pimoroni.com/tutorial/phat/raspberry-pi-phat-dac-install)
```
curl -sS get.pimoroni.com/phatdac | bash
```
  
- Allow user pi to shutdown

  Create /etc/polkit-1/localauthority/50-local.d/all_all_users_to_shutdown_reboot.pkla with the following content:

```
[Allow all users to shutdown and reboot]
Identity=unix-user:*
Action=org.freedesktop.login1.power-off;org.freedesktop.login1.power-off-multiple-sessions;org.freedesktop.login1.reboot;org.freedesktop.login1.reboot-multiple-sessions
ResultAny=yes
```
