# Target System Setup (BeagleBone)

This section walks through preparing the BeagleBone for remote builds using CLion.

---

## 🖥️ Target Boot Environment

```
Debian GNU/Linux 12 BeagleBone ttyS0

BeagleBoard.org Debian Bookworm IoT Image 2023-10-07
Support: https://bbb.io/debian
default username:password is [debian:temppwd]

Web console: https://BeagleBone.localdomain:9090/ or https://192.168.0.86:9090/
```

---

## 🔧 Step 1: Update Packages

```bash
debian@BeagleBone:~$ sudo apt update && sudo apt upgrade -y
```

---

## 🌐 Step 2: Confirm Network Access

Check that the target is assigned an IP address and has internet access:

```bash
debian@BeagleBone:~$ sudo ifconfig
```

Look for a valid `inet` entry under `eth0` (e.g., `192.168.x.x`).

---

## 🔑 Step 3: Enable SSH Access (Passwordless)

Generate SSH keys on your **host**, if not done already:

```bash
fred@eng-ai1:~$ ssh-keygen
```

Copy the public key to the BeagleBone:

```bash
fred@eng-ai1:~$ ssh-copy-id debian@192.x.x.x
```

You'll see something like:

```
/usr/bin/ssh-copy-id: INFO: attempting to log in with the new key(s)...
Number of key(s) added: 2
```

Verify it works without a password:

```bash
fred@eng-ai1:~$ ssh debian@192.x.x.x
```

---

## 🧱 Step 4: Install Required Packages (CMake)

```bash
debian@BeagleBone:~$ sudo apt install cmake
```

Verify the version:

```bash
debian@BeagleBone:~$ cmake --version
cmake version 3.25.1
```

You will reference this version when configuring the toolchain in CLion.

---

## 🧪 Step 5: Final Test

Ensure you can SSH from the host into the target **without a password**.

Once that’s working, you’re ready to launch CLion and set up the remote toolchain.
