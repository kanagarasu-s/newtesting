# Application Monitoring Tools Setup

This repository contains installation and configuration instructions for monitoring tools used for infrastructure observability: **Alloy**, **Grafana**, and **Loki**. Below are the details for each tool.

---

## 📦 Alloy Installation

### ✅ Description
Alloy is a vendor-agnostic OpenTelemetry Collector distribution with programmable pipelines used for observability and monitoring.

### ✅ Notes
- Alloy collects metrics and traces from various sources.
- Configuration can be customized via `/etc/default/alloy` and service files.
- Ensure permissions and environment settings are configured correctly.

---

## 📊 Grafana Installation

### ✅ Description
Grafana is an open-source platform for monitoring and observability dashboards.

### ✅ Notes
- Grafana provides visualization and alerting for metrics from multiple data sources.
- After installation, access the interface at `http://<your-server-ip>:3000`.
- The default username and password are both `admin`, and a password change is required at first login.

---

## 📂 Loki Server Setup

### ✅ Description
Loki is a log aggregation system optimized for efficiency and scalability.

### ✅ Notes
- The file `loki_local.conf.md` contains the configuration template.
- The server setup and service file are provided to integrate with Grafana and Alloy.

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
| alloy installation.md | Notes and references for Alloy setup |
| grafana installation.md | Notes and references for Grafana setup |
| loki_local.conf.md   | Loki configuration template          |
| slowquery.alloy      | Stage server configuration for Alloy |
| README.md           | This documentation file              |

---

## 📌 Final Remarks

This setup provides an observability stack for infrastructure monitoring using Grafana, Alloy, and Loki. Follow each note carefully and customize the configuration files as per your environment.

---
