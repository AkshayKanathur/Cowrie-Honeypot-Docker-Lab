# 🪤 Cowrie Honeypot — Docker Lab

A short hands-on lab demonstrating **Cowrie** (an SSH/Telnet honeypot) deployed with **Docker**.
This exercise shows how an attacker-like interaction is captured by the honeypot and how to pull the container logs for analysis — great practice for anyone building SOC skills or learning adversary behavior.

---

## 🎯 Objective

Deploy Cowrie in a container, interact with it over SSH to generate realistic attacker activity, and collect the honeypot logs for later analysis.

---

## 🧩 Lab Setup

* **Tool:** Cowrie (honeypot)
* **Platform:** Docker (host machine)
* **Access method:** SSH client (from host or another machine)
* **What I generated:** simple shell interactions and a dummy malicious file (`malicious.sh`) to create log entries

---

## ⚙️ Task 1: Pull & Run Cowrie in Docker

> (I used a Docker-based Cowrie image and ran it as a container. Replace placeholder values below with your chosen image or compose file if you prefer.)

```bash
# pull a Cowrie image (example)
docker pull cowrie/cowrie:latest

# run Cowrie (example)
docker run -d --name cowrie -p 2222:2222 cowrie/cowrie:latest

# verify the container is running
docker ps
```

**Result:** Cowrie container started and listening for SSH connections.

---

## ⚙️ Task 2: Connect to the Honeypot via SSH

```bash
# SSH into the honeypot (adjust port/host as needed)
ssh -p 2222 user@<host-ip>
```

**Result:** Connected to the honeypot’s fake shell and obtained an interactive prompt (note: this is the honeypot environment, not a real system).

---

## ⚙️ Task 3: Simulate Attacker Commands

While connected I ran a couple of commands to emulate attacker behaviour:

```bash
whoami
touch malicious.sh
```

**Result:** The honeypot accepted and recorded each command. `malicious.sh` was created in the honeypot’s filesystem (fake environment).

---

## ⚙️ Task 4: Collect Container Logs

To see the recorded activity from the container:

```bash
sudo docker logs cowrie
```

**Result:** The SSH session, commands, and other relevant interaction data were visible in the container logs — ready for parsing or ingestion to a SIEM.

---

## 🖼 Screenshots

**SSH Session (interactive shell)**
`![SSH session screenshot](Screenshot 2025-11-06 114745.png)`

**Docker logs showing captured commands**
![docker logs screenshot](<img width="1920" height="1020" alt="Screenshot 2025-11-06 114758" src="https://github.com/user-attachments/assets/54d1dc0f-a565-49bf-b068-ad6d1448f109" />
)

---

## 🧾 Notes & Tips

* Keep the honeypot isolated from production networks and data. Treat it as a controlled lab environment.
* Cowrie records a lot of telemetry — consider parsing logs into a SIEM (Splunk/ELK) for pattern analysis and alerting.
* If you want richer telemetry, look into mounting Cowrie’s `log` directory to the host or forwarding logs via a log shipper.

---

## 🙌 Acknowledgment

Thanks to the Cowrie project for providing a valuable honeypot for research and learning.

---

## 🏁 Conclusion — What I learned

* How to deploy a honeypot in a containerized environment.
* How attacker-like SSH interactions are captured by Cowrie.
* How to quickly retrieve captured activity using `docker logs` for triage or deeper analysis.
* A practical next step is parsing the logs, extracting indicators, and feeding them into a detection pipeline.

---

## 🔖 Tags

`#Cowrie` `#Honeypot` `#Docker` `#SOC` `#ThreatHunting` `#CyberSecurity` `#HandsOnLearning`
