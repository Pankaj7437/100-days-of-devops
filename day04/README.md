# Day 04 – Grant Script Execution Permissions

## Objective
Ensure that the script `/tmp/xfusioncorp.sh` on **App Server 1** has executable permissions so that all users can run it.

---

## Problem Description
The system administration team distributed a backup script named:

```
/tmp/xfusioncorp.sh
```

However, the script did not have the required executable permissions on **App Server 1**.  
The task was to grant the appropriate permissions so that **all users can execute the script**.

---

## Initial Attempt

First, executable permission was added using:

```bash
sudo chmod +x /tmp/xfusioncorp.sh
```

Verification:

```bash
ls -l /tmp/xfusioncorp.sh
```

Result:

```
--x--x--x
```

Although this provides execute permission to all users, it removes the read permission which may be required for script execution in some environments.  
Therefore, the task validation failed.

---

## Correct Solution

The correct permission was set using:

```bash
sudo chmod 755 /tmp/xfusioncorp.sh
```

Verification:

```bash
ls -l /tmp/xfusioncorp.sh
```

Output:

```
-rwxr-xr-x
```

---

## Permission Breakdown

| Permission | Meaning |
|-------------|---------|
| 7 | Read + Write + Execute |
| 5 | Read + Execute |
| 5 | Read + Execute |

Final permission structure:

```
Owner  → rwx
Group  → r-x
Others → r-x
```

---

## Summary

The script execution issue was resolved by assigning **755 permissions** to the file.  
This allows all users to execute the script while maintaining proper read access and secure write permissions limited to the owner.
