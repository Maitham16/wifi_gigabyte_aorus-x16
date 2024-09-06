
# Instructions to Fix WiFi and Bluetooth on Debian

## Update and Install Firmware
- Ensure your package lists are updated:
  ```bash
  sudo apt update
  ```
- Reinstall the relevant firmware for iwlwifi:
  ```bash
  sudo apt install --reinstall firmware-iwlwifi
  ```

## Download and Copy Firmware from Repository
- Clone the Linux firmware repository to get the latest files:
  ```bash
  git clone https://git.kernel.org/pub/scm/linux/kernel/git/firmware/linux-firmware.git
  cd linux-firmware
  ```
- Copy the necessary firmware files to `/lib/firmware`:
  ```bash
  sudo cp iwlwifi-*-ucode /lib/firmware/
  ```

## Unload and Reload Kernel Modules
- Ensure all related modules are unloaded:
  ```bash
  sudo modprobe -r iwlmvm
  sudo modprobe -r iwlwifi
  ```
- Reload the `iwlwifi` module:
  ```bash
  sudo modprobe iwlwifi
  sudo modprobe iwlmvm
  ```

## Restart Network Services
- Restart NetworkManager to ensure it recognizes the changes:
  ```bash
  sudo systemctl restart NetworkManager
  ```

## Check the Operation
- Check that everything is loaded correctly and no errors are reported:
  ```bash
  dmesg | grep iwlwifi
  ```
- Ensure the network interface is up and can scan for networks:
  ```bash
  ip link set dev wlan0 up
  iw dev wlan0 scan
  ```

---

# Debian Repository Configuration

## Main, contrib, and non-free repositories
```
deb http://deb.debian.org/debian/ bookworm main contrib non-free
deb-src http://deb.debian.org/debian/ bookworm main contrib non-free
```

## Security updates
```
deb http://security.debian.org/debian-security bookworm-security main contrib non-free
deb-src http://security.debian.org/debian-security bookworm-security main contrib non-free
```

## Stable updates
```
deb http://deb.debian.org/debian/ bookworm-updates main contrib non-free
deb-src http://deb.debian.org/debian/ bookworm-updates main contrib non-free
```

## Backports
```
deb http://deb.debian.org/debian/ bookworm-backports main contrib non-free
deb-src http://deb.debian.org/debian/ bookworm-backports main contrib non-free
```

## Debian Sid (Unstable)
```
deb http://deb.debian.org/debian/ unstable main contrib non-free
```
