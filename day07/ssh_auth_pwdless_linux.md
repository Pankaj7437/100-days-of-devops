# Day 7 – Configure Passwordless SSH

## Objective
Enable passwordless SSH access from the jump host user `thor` to all application servers.

## Steps

Generate SSH key

```bash
ssh-keygen
```

Copy key to servers

```bash
ssh-copy-id tony@stapp01
ssh-copy-id steve@stapp02
ssh-copy-id banner@stapp03
```

## Result
User `thor` can now SSH into all application servers without entering a password.
