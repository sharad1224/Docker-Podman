# 🚀 Podman Container Deployment Guide

This guide outlines the steps to build, run, and configure a Podman container for automated service using systemd.

---

## 📥 Step 1: Download the Containerfile

```bash
wget http://content.example.com/deploy_containers/Containerfile
```
```bash
ls
```

---

## 🛠️ Step 2: Build the Podman Image

```bash
podman build -t monitor .
```
```bash
podman images
```

---

## 🧪 Step 3: Run the Container

```bash
podman run -d --name sharad monitor:latest
```
```bash
podman ps
```

---

## 📁 Step 4: Create and Set Permissions for Host Volumes

```bash
sudo mkdir -p /opt/files /opt/processed
sudo chown student:student /opt/files /opt/processed
```

---

## 🐳 Step 5: Run Container with Volume Mounts

```bash
podman run -d --name escti2pdf -v /opt/files:/opt/incoming/:Z -v /opt/processed:/opt/outgoing/:Z monitor:latest
podman ps
```

---

## 🧩 Step 6: Generate systemd Service Unit Files

```bash
mkdir -p /home/student/.config/systemd/user
cd /home/student/.config/systemd/user
podman generate systemd --name escti2pdf --files --new
```

---

## ⚙️ Step 7: Enable User Linger Mode

```bash
loginctl enable-linger student
```

---

## 🔄 Step 8: Reload and Enable systemd Service

```bash
systemctl daemon-reload --user
systemctl enable --now container-escti2pdf.service --user
systemctl status container-escti2pdf.service --user
podman ps
```

---

✅ You have now successfully built, deployed, and configured a persistent Podman container service using `systemd`.
