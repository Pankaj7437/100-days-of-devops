# Day 05 – Disable SELinux Permanently

## Objective
Install required SELinux packages and configure SELinux to be permanently disabled on App Server 3.

## Commands Used

Install SELinux packages

```bash
sudo yum install -y selinux-policy selinux-policy-targeted
```

Edit SELinux configuration

```bash
sudo vi /etc/selinux/config
```

Update the configuration:

```
SELINUX=disabled
```

## Notes
The server was not rebooted as the maintenance reboot was already scheduled.
After reboot, SELinux will be permanently disabled.
