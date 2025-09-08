# Monitoring Tools Setup

This repository contains installation and configuration instructions for monitoring tools used in the infrastructure: **Alloy**, **Grafana**, and **Loki**. Below are the details and steps for each tool.

---

## 📦 Alloy Installation

### ✅ Description
Alloy is a vendor-agnostic OpenTelemetry Collector distribution with programmable pipelines used for observability and monitoring.

### ✅ Installation Steps
1. Add Grafana’s repository GPG key:
    ```bash
    sudo mkdir -p /etc/apt/keyrings/
    wget -q -O - https://apt.grafana.com/gpg.key | gpg --dearmor | sudo tee /etc/apt/keyrings/grafana.gpg > /dev/null
    ```

2. Add the repository:
    ```bash
    echo "deb [signed-by=/etc/apt/keyrings/grafana.gpg] https://apt.grafana.com stable main" | sudo tee /etc/apt/sources.list.d/grafana.list
    ```

3. Update and install Alloy:
    ```bash
    sudo apt update
    sudo apt install alloy -y
    ```

4. Enable and start Alloy service:
    ```bash
    sudo systemctl enable alloy.service
    sudo systemctl start alloy
    ```

5. Check the service status:
    ```bash
    sudo systemctl status alloy
    ```

6. Edit configuration:
    ```bash
    sudo vi /etc/default/alloy
    ```
    Example:
    ```bash
    CONFIG_FILE="/etc/alloy/config.yaml"
    CUSTOM_ARGS="--server.http.listen-addr=0.0.0.0:12345"
    ```

---

## 📊 Grafana Installation

### ✅ Description
Grafana is an open-source platform for monitoring and observability dashboards.

### ✅ Installation Steps
1. Update your system:
    ```bash
    sudo apt update
    ```

2. Install dependencies:
    ```bash
    sudo apt install -y software-properties-common apt-transport-https wget
    ```

3. Add Grafana’s GPG key:
    ```bash
    wget -q -O - https://packages.grafana.com/gpg.key | sudo gpg --dearmor -o /usr/share/keyrings/grafana.gpg
    ```

4. Add the repository:
    ```bash
    echo "deb [signed-by=/usr/share/keyrings/grafana.gpg] https://packages.grafana.com/oss/deb stable main" | sudo tee /etc/apt/sources.list.d/grafana.list
    ```

5. Install Grafana:
    ```bash
    sudo apt update
    sudo apt install grafana -y
    ```

6. Enable and start Grafana service:
    ```bash
    sudo systemctl enable grafana-server
    sudo systemctl start grafana-server
    ```

7. Check status:
    ```bash
    sudo systemctl status grafana-server
    ```

8. Allow Grafana through firewall:
    ```bash
    sudo ufw allow 3000/tcp
    sudo ufw reload
    ```

9. Access Grafana in the browser:
    ```
    http://<your-server-ip>:3000
    ```
    **Default credentials:**  
    Username: `admin`  
    Password: `admin`  

    ⚙ You will be prompted to change the password on first login.

---

## 📂 Loki Server Setup

### ✅ Description
Loki is a log aggregation system optimized for efficiency and scalability.

### ✅ Notes
- The file `loki_local.conf.md` contains the configuration template.
- The server setup and service file are provided.

---

## 📂 Stage Server – Alloy Configuration

### ✅ Notes
- The file `slowquery.alloy` contains configuration related to slow query monitoring.

---

## 📝 Notes

- All configurations should be validated and permissions applied correctly.
- Ensure firewalls allow required ports (`3000` for Grafana, etc.).
- Services must be enabled and started to ensure they run on system boot.

---

## 📂 Files in this Repository

| File Name             | Description                           |
| ------------------- | ------------------------------------ |
| alloy installation.md | Instructions for installing Alloy     |
| grafana installation.md | Instructions for installing Grafana  |
| loki_local.conf.md   | Loki configuration template          |
| slowquery.alloy      | Stage server configuration for Alloy |
| README.md           | This documentation file              |

---

## 📌 Final Remarks

This setup provides an observability stack for infrastructure monitoring using Grafana, Alloy, and Loki. Follow each step carefully and customize the configuration files as per your environment.

---

