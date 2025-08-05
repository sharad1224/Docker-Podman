# Podman Systemd Container Workflow

*Generated on 2025-08-05*

This document provides a step-by-step explanation of commands used to configure and manage Podman containers with systemd integration.

### Step 1
```bash
sudo -i
```
**Description**: Switch to the root shell.

### Step 2
```bash
history
```
**Description**: Displays the command history.

### Step 3
```bash
wget http://content.example.com/deploy_containers/Containerfile
```
**Description**: Downloads the Containerfile.

### Step 4
```bash
podman login registry.lab.example.com
```
**Description**: Logs into the specified Podman registry.

### Step 5
```bash
mkdir -p .config/containers && cd .config/containers/
```
**Description**: Creates and navigates to the Podman config directory.

### Step 6
```bash
vi registries.conf
```
**Description**: Edits the registries.conf file.

### Step 7
```bash
podman info
```
**Description**: Displays Podman system information.

### Step 8
```bash
podman images
```
**Description**: Lists all local container images.

### Step 9
```bash
podman build -t monitor .
```
**Description**: Builds a container image with the tag 'monitor'.

### Step 10
```bash
podman run -d --name sharad monitor:latest
```
**Description**: Runs a container in detached mode named 'sharad'.

### Step 11
```bash
podman stop 49dd33809e17
```
**Description**: Stops the container with the specified ID.

### Step 12
```bash
podman ps
```
**Description**: Shows running containers.

### Step 13
```bash
podman ps -a
```
**Description**: Shows all containers (running and stopped).

### Step 14
```bash
mkdir -p /opt/files /opt/processed
```
**Description**: Creates directories for input and output.

### Step 15
```bash
chown student:student /opt/files /opt/processed
```
**Description**: Changes ownership of the directories to the user 'student'.

### Step 16
```bash
podman run --name escti2pdf -v /opt/files:/opt/processed/incoming/:Z monitor:latest
```
**Description**: Runs container with a volume mount (SELinux context enforced).

### Step 17
```bash
podman run --name escti2pdf -v /opt/files:/opt/incoming/:Z -v /opt/processed:/opt/outgoing/:Z monitor:latest
```
**Description**: Runs container with two volume mounts.

### Step 18
```bash
mkdir -p ~/.config/systemd/user
```
**Description**: Creates directory for user-level systemd unit files.

### Step 19
```bash
cd ~/.config/systemd/user
```
**Description**: Navigates to the systemd user unit directory.

### Step 20
```bash
podman generate systemd --name escti2pdf --files --new
```
**Description**: Generates a systemd unit file for the container.

### Step 21
```bash
systemctl --user daemon-reexec
```
**Description**: Reexecutes the systemd user daemon.

### Step 22
```bash
systemctl --user daemon-reload
```
**Description**: Reloads the systemd user daemon.

### Step 23
```bash
systemctl enable container-escti2pdf.service --user
```
**Description**: Enables the container service to start on boot.

### Step 24
```bash
systemctl start container-escti2pdf.service --user
```
**Description**: Starts the container as a systemd service.

