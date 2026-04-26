# ⚡ Arch Linux Fast Boot Optimization Guide

A minimal, practical checklist to keep Arch system **booting fast (<10s)** without breaking usability.

---

## 🚀 1. Use a Faster Kernel (Zen)

Install and use the **Zen kernel** for better responsiveness:

```bash
sudo pacman -S linux-zen linux-zen-headers
```

👉 Keep default kernel as fallback:

```bash
sudo pacman -S linux linux-headers
```
---

## 🧹 2. Disable Unnecessary Services

Check enabled services:

```bash
systemctl list-unit-files --state=enabled
```

Disable what you don’t use:

```bash
sudo systemctl disable cups.service
sudo systemctl disable bluetooth.service
```

---

## ⚡ 3. Disable Network Wait

This prevents boot delays waiting for internet:

```bash
sudo systemctl disable NetworkManager-wait-online.service
```

---

## 🥾 4. Optimize Bootloader (systemd-boot)

If using **systemd-boot**, reduce timeout:

Edit:

```bash
sudo nano /boot/loader/loader.conf
```

Set:

```text
timeout 1
default arch
```

---

## ⚙️ 5. Enable Parallel Service Startup

Ensure systemd runs services in parallel (default, but verify):

```bash
sudo nano /etc/systemd/system.conf
```

Uncomment or add:

```text
DefaultTimeoutStartSec=10s
DefaultTimeoutStopSec=10s
```

---

## 🧠 6. Analyze Boot Time

Check where time is spent:

```bash
systemd-analyze
```

Detailed breakdown:

```bash
systemd-analyze blame
```

---

## 🔥 7. Disable Unused Kernel Modules (Advanced)

Optional optimization:

```bash
sudo nano /etc/modprobe.d/blacklist.conf
```

Example:

```text
blacklist pcspkr
```

---

## ⚡ 8. Reduce Journal Size

Limit system logs:

```bash
sudo nano /etc/systemd/journald.conf
```

Set:

```text
SystemMaxUse=100M
```

---

## 🧊 9. Avoid Heavy Autostart Apps

In KDE:

* System Settings → Startup & Shutdown → Autostart
* Disable unnecessary apps

---

## 🧠 10. Keep System Clean

```bash
sudo pacman -Sc
```

---
