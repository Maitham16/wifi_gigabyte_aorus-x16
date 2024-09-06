
# Instructions to Fix WiFi and Bluetooth on Debian

## Update and Install Firmware
- Ensure your package lists are updated:
  ```bash
  sudo apt update
  ```
- If necessary, reinstall the relevant firmware for iwlwifi:
  ```bash
  sudo apt install --reinstall firmware-iwlwifi
  ```

## Unload and Reload Kernel Modules
- Unload dependent modules before unloading `iwlwifi`:
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
