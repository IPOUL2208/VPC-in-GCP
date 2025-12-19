# GCP VPC Architecture with NAT, Peering & WordPress

This project demonstrates a **real-world Google Cloud Platform (GCP) network architecture** using **Auto VPC, Custom VPC, firewall rules, VPC peering, Cloud NAT**, and a **public WordPress deployment**.

---

##  Architecture Overview

### VPCs
- **Dev VPC (Auto Mode)**  
  - Name: `dev-auto-vpc`
  - 1 VM instance

- **Prod VPC (Custom Mode)**  
  - Name: `prod-vpc`
  - Subnets:
    - `web-sub` → Web servers
    - `db-sub` → Database server
    - `util-sub` → Utility server

---

##  VM Instances

### Dev
- `dev-vm-1`

### Prod
- Web: `prod-web-1`, `prod-web-2`
- DB: `prod-db-1`
- Utility: `prod-util-1`

---

##  Tasks Implemented

### ✅ Task 1: Internal Communication (Prod VPC)
- All prod VMs can ping each other using **ICMP firewall rule**

### ✅ Task 2: Secure Dev ↔ Prod Connectivity
- **VPC Peering** between dev and prod
- SSH access from `util-vm` to `dev-vm`
- Secure file transfer using `scp`

### ✅ Task 3: Public WordPress Deployment
- WordPress installed on Web VM
- HTTP/HTTPS access allowed via firewall
- Accessible from public internet

### ✅ Task 4: Secure Internet Access using NAT
- Removed external IPs from private VMs
- Configured **Cloud Router + Cloud NAT**
- Private VMs get outbound internet only

---

## Security Best Practices Used
- Least-privilege firewall rules
- No external IPs for private workloads
- NAT for outbound access
- Network segmentation using subnets

---

##  Tools & Services Used
- Google Cloud VPC
- Compute Engine
- Cloud NAT
- Cloud Router
- Firewall Rules
- Apache, PHP, WordPress

---

## Outcome
A secure, scalable, production-ready GCP network architecture following cloud best practices.

---

###  Author
**Indresh Pal**  
Cloud / DevOps Engineer  
