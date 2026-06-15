# Grafana Installation Guide on Ubuntu

This guide explains how to install and configure Grafana on Ubuntu 22.04/24.04.

## Prerequisites

Update the system packages before installation:

```bash
sudo apt update
sudo apt upgrade -y
```

Verify the Ubuntu version:

```bash
lsb_release -a
```

---

## Step 1: Install Required Packages

Install the packages required to add external repositories:

```bash
sudo apt install -y software-properties-common wget apt-transport-https gnupg2
```

---

## Step 2: Add Grafana GPG Key

Download and install the Grafana repository signing key:

```bash
wget -q -O - https://apt.grafana.com/gpg.key | sudo gpg --dearmor -o /usr/share/keyrings/grafana.gpg
```

Verify the key installation:

```bash
ls -l /usr/share/keyrings/grafana.gpg
```

---

## Step 3: Add Grafana Repository

Create the Grafana repository configuration:

```bash
echo "deb [signed-by=/usr/share/keyrings/grafana.gpg] https://apt.grafana.com stable main" | sudo tee /etc/apt/sources.list.d/grafana.list
```

Update the package index:

```bash
sudo apt update
```

---

## Step 4: Install Grafana

Install Grafana OSS:

```bash
sudo apt install grafana -y
```

Verify the installation:

```bash
grafana-server -v
```

Expected output:

```text
Version x.x.x (commit: xxxxxxx)
```

---

## Step 5: Enable and Start Grafana Service

Enable Grafana to start automatically on system boot:

```bash
sudo systemctl enable grafana-server
```

Start the Grafana service:

```bash
sudo systemctl start grafana-server
```

Check the service status:

```bash
sudo systemctl status grafana-server
```

Expected output:

```text
Active: active (running)
```

---

## Step 6: Verify Grafana is Running

Check if Grafana is listening on port **3000**:

```bash
sudo ss -tulpn | grep 3000
```

Expected output:

```text
tcp LISTEN 0 4096 *:3000
```

Alternatively:

```bash
curl http://localhost:3000
```

---

## Step 7: Configure Firewall (Optional)

If UFW is enabled, allow Grafana traffic:

```bash
sudo ufw allow 3000/tcp
sudo ufw reload
```

Verify firewall rules:

```bash
sudo ufw status
```

---

## Step 8: Access Grafana Web Interface

Open your browser and navigate to:

```text
http://<SERVER-IP>:3000
```

Example:

```text
http://192.168.1.100:3000
```

---

## Step 9: Login to Grafana

Default credentials:

| Field    | Value |
| -------- | ----- |
| Username | admin |
| Password | admin |

> **Note:** Grafana will prompt you to change the password during the first login.

---

## Step 10: View Grafana Logs

Monitor Grafana logs in real time:

```bash
sudo journalctl -u grafana-server -f
```

Log file location:

```text
/var/log/grafana/grafana.log
```

View log file:

```bash
sudo tail -f /var/log/grafana/grafana.log
```

---

## Common Service Commands

### Start Grafana

```bash
sudo systemctl start grafana-server
```

### Stop Grafana

```bash
sudo systemctl stop grafana-server
```

### Restart Grafana

```bash
sudo systemctl restart grafana-server
```

### Reload Configuration

```bash
sudo systemctl reload grafana-server
```

### Check Status

```bash
sudo systemctl status grafana-server
```

---

## Configure Prometheus Data Source

If Prometheus is already installed:

1. Log in to Grafana.
2. Navigate to **Connections → Data Sources**.
3. Click **Add Data Source**.
4. Select **Prometheus**.
5. Configure the URL:

```text
http://localhost:9090
```

or

```text
http://<PROMETHEUS-IP>:9090
```

6. Click **Save & Test**.

---

## Import Node Exporter Dashboard

Navigate to:

```text
Dashboards → Import
```

Use Dashboard ID:

```text
1860
```

This imports the popular **Node Exporter Full Dashboard** for monitoring Linux servers.

---

## Troubleshooting

### Grafana Service Not Starting

```bash
sudo journalctl -xeu grafana-server
```

### Port 3000 Already in Use

```bash
sudo lsof -i :3000
```

### Repository Update Errors

```bash
sudo apt clean
sudo apt update
```

### Verify Grafana Configuration

```bash
sudo grafana-server --config=/etc/grafana/grafana.ini
```

---

## Verification Checklist

* [x] Grafana package installed
* [x] Grafana service running
* [x] Port 3000 listening
* [x] Web UI accessible
* [x] Admin login successful
* [x] Prometheus data source connected
* [x] Dashboard imported

---

## Grafana URLs

### Local Access

```text
http://localhost:3000
```

### Remote Access

```text
http://<SERVER-IP>:3000
```

---

## Useful Directories

| Path                  | Description                 |
| --------------------- | --------------------------- |
| `/etc/grafana/`       | Grafana configuration files |
| `/var/lib/grafana/`   | Grafana data directory      |
| `/var/log/grafana/`   | Grafana log files           |
| `/usr/share/grafana/` | Grafana application files   |

---

**Grafana installation is now complete and ready to visualize Prometheus metrics and dashboards.**
