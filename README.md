# Luciphone2

## Dependance : 
policykit-1, python-pymedia

## Installation :

- Allow user pi to shutdown

  Create as root /etc/polkit-1/localauthority/50-local.d/all_all_users_to_shutdown_reboot.pkla with the following content:

```
[Allow all users to shutdown and reboot]
Identity=unix-user:*
Action=org.freedesktop.login1.power-off;org.freedesktop.login1.power-off-multiple-sessions;org.freedesktop.login1.reboot;org.freedesktop.login1.reboot-multiple-sessions
ResultAny=yes
```
