# GCP Secure Multi-VPC Architecture with NAT & WordPress

This project demonstrates a **production-style Google Cloud Platform (GCP) network architecture** designed with **security, scalability, and best practices** in mind.

---

##  Architecture Overview

### VPC Design
- **Dev Environment**
  - Auto Mode VPC: `dev-auto-vpc`
  - 1 VM (`dev-vm-1`)

- **Prod Environment**
  - Custom Mode VPC: `prod-vpc`
  - Subnets:
    - `web-sub` (Web servers)
    - `db-sub` (Database)
    - `util-sub` (Utility / Admin)

---

##  Compute Resources

### Dev
- `dev-vm-1`

### Prod
- Web: `prod-web-1`, `prod-web-2`
- DB: `prod-db-1`
- Utility: `prod-util-1`

---

## 🔹 Tasks Implemented

###  1. Internal Communication (Prod)
- All prod VMs communicate internally using **ICMP firewall rules**

###  2. Secure Dev ↔ Prod Connectivity
- **VPC Peering** between Dev and Prod
- SSH allowed only from `util-vm` to `dev-vm`
- Secure file transfer using `scp`

###  3. Public WordPress Deployment
- WordPress installed on Web VM
- HTTP/HTTPS firewall rules configured
- Accessible from the public internet

###  4. Secure Internet Access using Cloud NAT
- Removed external IPs from private VMs
- Configured **Cloud Router + Cloud NAT**
- Private VMs have outbound internet access only

---

##  Security Best Practices
- No external IPs for private workloads
- Least-privilege firewall rules
- Network segmentation via subnets
- NAT for outbound-only internet access

---

##  Tools & Technologies
- Google Cloud VPC
- Compute Engine
- Cloud NAT & Cloud Router
- Firewall Rules
- Apache, PHP, WordPress
- Linux (Debian)

---

##  Outcome
A secure, scalable, and production-ready GCP infrastructure that mirrors real-world enterprise environments.

---


###  Author
**Indresh Pal**  
Cloud / DevOps Engineer  


## Using Terraform and GCLOUD CLI

resource "google_compute_network" "prod_vpc" {
  name                    = "prod-vpc"
  auto_create_subnetworks = false
}

resource "google_compute_subnetwork" "web_sub" {
  name          = "web-sub"
  region        = "us-central1"
  network       = google_compute_network.prod_vpc.id
  ip_cidr_range = "10.10.1.0/24"
}
