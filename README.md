# A^3 University Wi-Fi Network

A Cisco Packet Tracer project that demonstrates the design and configuration of a secure university wireless network with separate network access for Students, Faculty, Administration, and Guests.

The network uses VLAN segmentation, DHCP, Router-on-a-Stick, inter-VLAN routing, WPA2-PSK wireless security, and ACL-based access control.

---

## 1. Project Description

The **University Wi-Fi Network** is designed to provide organized and secure wireless connectivity for different categories of university users.

The network separates:

- Students
- Faculty
- Administration
- Guests
- Servers
- Network Management

Each user group is placed in a separate VLAN and IP subnet.

`CORE-R2` performs inter-VLAN routing using Router-on-a-Stick. A centralized DHCP server provides IP addresses to the user VLANs through DHCP relay.

The main security requirement is to prevent Guest users from accessing the internal Server VLAN.

---

## 2. Problem Statement

A university network contains different types of users with different access requirements.

Students, faculty, administration staff, and guests should not all operate in the same network. If all users are placed in one network, it becomes difficult to manage traffic, apply security policies, and restrict access to sensitive resources.

This project solves the problem by using VLAN segmentation, separate wireless SSIDs, centralized DHCP, inter-VLAN routing, and ACL-based security.

---

## 3. Objectives

The main objectives of this project are:

- Create separate VLANs for different university user groups.
- Provide separate wireless SSIDs for Students, Faculty, Administration, and Guests.
- Configure WPA2-PSK wireless security.
- Configure DHCP for wireless clients.
- Use DHCP relay to connect clients with the centralized DHCP server.
- Configure Router-on-a-Stick for inter-VLAN routing.
- Create a dedicated Server VLAN.
- Create a dedicated Management VLAN.
- Prevent Guest users from accessing internal university servers.
- Document AAA and RADIUS concepts.
- Represent external Internet connectivity using an ISP router.
- Test the network using Packet Tracer.

---

## 4. Features

| Feature | Status |
|---|---|
| VLAN segmentation | Implemented |
| Student wireless network | Implemented |
| Faculty wireless network | Implemented |
| Administration wireless network | Implemented |
| Guest wireless network | Implemented |
| WPA2-PSK | Implemented |
| DHCP | Implemented |
| DHCP Relay | Implemented |
| Router-on-a-Stick | Implemented |
| Inter-VLAN Routing | Implemented |
| Guest-to-Server ACL | Implemented |
| Server VLAN | Implemented |
| Management VLAN 99 | Implemented |
| AUTH-SERVER | Included |
| AAA/RADIUS concept | Documented |
| RADIUS-based Wi-Fi authentication | Not claimed |
| ISP/Internet connectivity | Optional extension |
| DNS/Web/File services | Only if configured in Packet Tracer |

---

## 5. Technologies Used

- Cisco Packet Tracer
- Cisco IOS
- IPv4
- VLAN
- IEEE 802.1Q
- Router-on-a-Stick
- Inter-VLAN Routing
- DHCP
- DHCP Relay
- Access Control List (ACL)
- Wireless LAN
- WPA2-PSK
- AES-CCMP
- AAA
- RADIUS concept
- ISP/Internet connectivity

---

# 6. Network Architecture

The project follows a hierarchical network architecture.

### Core

**CORE-R2**

Responsible for:

- Inter-VLAN routing
- VLAN gateway functions
- ACL enforcement
- DHCP relay

### Distribution Functions

The distribution functions are performed by `CORE-R2`.

Since this is a college-scale project, a separate distribution router is not used.

### Access

The access layer consists of:

- Main Switch
- Wireless Access Points
- Wireless laptops

### ISP

`ISP-R1` represents the external Internet/ISP.

---

# 7. Network Topology

```text
                         ┌─────────────────┐
                         │     ISP-R1      │
                         │  ISP / Internet │
                         └────────┬────────┘
                                  │
                                  │
                         ┌────────▼────────┐
                         │     CORE-R2     │
                         │                 │
                         │ Inter-VLAN      │
                         │ Routing         │
                         │ ACL             │
                         │ DHCP Relay      │
                         └────────┬────────┘
                                  │
                         G0/0 ↔ Fa0/1
                         Copper Straight-
                         Through Trunk
                                  │
                         ┌────────▼────────┐
                         │   Main Switch   │
                         └────────┬────────┘
                                  │
              ┌───────────────────┼───────────────────┐
              │                   │                   │
              ▼                   ▼                   ▼
        Student APs          Faculty APs         Admin APs
        VLAN 10              VLAN 20             VLAN 30
              │                   │                   │
        Student Laptops      Faculty Laptops    Admin Laptops

                                  │
                                  ▼
                             Guest APs
                             VLAN 40
                                  │
                           Guest Laptops

                                  │
                                  ▼
                         ┌─────────────────┐
                         │   Server VLAN   │
                         │     VLAN 50     │
                         │                 │
                         │ DHCP Server     │
                         │ 192.168.50.30   │
                         │                 │
                         │ AUTH-SERVER     │
                         │ 192.168.50.40   │
                         └─────────────────┘

                         Management VLAN 99
