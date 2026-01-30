---
id: networking
title: Networking for Beginners
sidebar_label: Networking for Beginners
---

# Data Link Layer

The Data Link Layer is responsible for the reliable transfer of data within a local network. It handles communication between devices that are directly connected on the same network.

## Key Responsibilities
- Uses MAC (Media Access Control) addresses to identify devices on a local network.
- Encapsulates network layer packets into frames.
- Ensures data is delivered to the correct physical device (NIC).
- Works only within the local network (LAN).

**Example:**
When a data packet enters a local network, the Data Link Layer uses the destination MAC address to deliver the data to the correct host.


# Transport Layer

The Transport Layer is responsible for providing end-to-end communication between applications running on different devices. It ensures that data is delivered correctly, in order, and according to the required level of reliability.

## Services Provided by the Transport Layer

### 1. Connection-Oriented Service (TCP)
- A connection is established before data transfer begins.
- Data is transmitted in three phases:
  1. Connection establishment
  2. Data transfer
  3. Connection termination
- The receiver sends acknowledgements (ACKs) for received packets.
- Lost packets are retransmitted.
- Provides reliable, ordered, and error-checked delivery.

**Examples:**
- Web browsing (HTTP/HTTPS)
- File downloads
- Email services

---

### 2. Connection-Less Service (UDP)
- No connection is established before data transmission.
- Data is sent without acknowledgements.
- Faster communication with lower overhead.
- Does not guarantee delivery, order, or error correction.

**Examples:**
- Video and voice calls (VoIP)
- Online gaming
- Live streaming
- DNS queries

---


---

# Summary

- **Transport Layer** focuses on application-to-application communication and reliability.
- **Data Link Layer** focuses on device-to-device communication within a local network using MAC addresses.

# Presentation Layer

The Presentation Layer is also known as the **translation layer**. It is responsible for preparing data received from the Application Layer so that it can be properly transmitted over the network and correctly understood by the receiving system.

## Functions of the Presentation Layer

### 1. Translation
This function converts data from one format to another to ensure compatibility between different systems.

- Different computers may use different data representation formats.
- The Presentation Layer translates data into a common format.

**Example:**
- ASCII and EBCDIC are character encoding formats.
- A system using ASCII can communicate with a system using EBCDIC because the Presentation Layer performs the necessary translation.

---

### 2. Encryption and Decryption
This function ensures data security during transmission.

- **Encryption** converts readable data into an unreadable coded form before transmission.
- **Decryption** converts the encrypted data back into its original readable form at the receiver.

**Example:**
- Secure web communication (HTTPS)
- Passwords and sensitive data are encrypted before being sent over the network.

---

## Summary
- The Presentation Layer handles data formatting and security.
- It ensures that data is readable and secure between communicating systems.
- It acts as a translator and security layer between the Application Layer and lower layers.


# VLAN (Virtual Local Area Network)

**VLAN** stands for **Virtual Local Area Network**.  
It allows you to create multiple **virtual networks** on a single **physical network** without adding extra cables or hardware.

---

## What is VLAN?

- A VLAN separates devices logically into different groups.
- Devices in one VLAN cannot directly communicate with devices in another VLAN unless routing is configured.
- Uses the same physical switches and cables.

**Example:**
- Accounting Department → VLAN 10  
- IT Department → VLAN 20  
- Sales Department → VLAN 30  

Even if all devices connect to the same switch, they act like they are on separate networks.

---

## Advantages of VLAN

1. **Improved Security**  
   - Traffic stays within the VLAN; other groups cannot access it.
2. **Reduced Network Traffic**  
   - Packets are only sent to devices in the same VLAN.
3. **Better Organization**  
   - Logical grouping without changing physical connections.

---

## How VLAN Works

- Requires a **managed switch**.
- Each port on the switch is assigned to a VLAN.
- Devices connected to a port become part of that VLAN.
- The switch ensures packets are delivered only to the correct VLAN members.

# DHCP (Dynamic Host Configuration Protocol)

**DHCP** is a protocol that automatically assigns **IP addresses** and network settings to devices on a network, without manual configuration.

---

## How DHCP Works

1. **Device joins network**  
   - Example: laptop or smartphone connects to Wi-Fi
   - Sends a **DHCP Discover** message: "Hello! I need an IP."

2. **DHCP Server responds**  
   - Sends a **DHCP Offer** with:
     - IP address  
     - Subnet mask  
     - Gateway  
     - DNS server

3. **Device requests the offered IP**  
   - Sends **DHCP Request**: "I accept this IP."

4. **Server confirms**  
   - Sends **DHCP ACK**, finalizing the assignment
   - Device starts using the IP

---

## Key Points

- **Dynamic IP:** The IP may change after the lease time expires.  
- **Lease Time:** Duration for which the IP is valid.  
- **Static IP:** You can also assign a fixed IP manually if needed.

---

## Example in Daily Life

- When your phone connects to Wi-Fi, it automatically gets an IP from the DHCP server in your router.  
- No need to manually type an IP or network info.

---

## Static IP Option

1. **On the device:**  
   - Go to Wi-Fi settings → Advanced → IP settings → Static  
   - Enter desired IP, Gateway, Subnet Mask, and DNS

2. **On the router (DHCP Reservation):**  
   - Assign a fixed IP to the device’s MAC address  
   - Ensures the device always gets the same IP automatically

---

**Summary:**  
- DHCP = automatic IP assignment  
- Makes network setup easy, fast, and reduces errors  
- Static IP can be set for devices needing a permanent address

# NAT & PAT

## NAT (Network Address Translation)

**NAT** is a method that translates **private IP addresses** inside a local network to a **public IP address** for communication on the Internet, and vice versa.

### Why NAT is needed
- Home or office networks use private IPs:  
- Internet requires public IPs.
- NAT acts as a translator between private and public IPs.

### Example
**Home network:**
- Laptop: 192.168.1.10  
- Mobile: 192.168.1.11  
- Router (NAT): 203.0.113.5 ← Public IP  

**Flow:**
1. Laptop requests Google website  
2. NAT translates 192.168.1.10 → 203.0.113.5  
3. Google responds to 203.0.113.5  
4. NAT translates back to 192.168.1.10  

✅ All devices appear as a single public IP on the Internet.

---

## PAT (Port Address Translation)

**PAT** is a type of NAT that translates both **IP addresses and port numbers**, allowing multiple devices to share a single public IP simultaneously.

### Example
| Device | Private IP | Source Port | Public IP | NAT Port |
|--------|------------|------------|-----------|---------|
| Laptop | 192.168.1.10 | 5000 | 203.0.113.5 | 10001 |
| Mobile | 192.168.1.11 | 5000 | 203.0.113.5 | 10002 |

- Internet sees only 203.0.113.5  
- NAT uses different ports to distinguish devices

---

## Current Usage

- ✅ NAT and PAT are **widely used** today:  
- Home routers  
- Office networks  
- Data centers  
- Essential because **public IPs are limited**  

---

## Summary

| Feature | NAT | PAT |
|---------|-----|-----|
| Translates | IP only | IP + Port |
| Purpose | Allow private devices to access the Internet | Allow multiple devices to share a single public IP |
| Usage today | Yes | Yes, supported by all modern devices |

**Daily example:**  
- When your laptop and phone connect to Wi-Fi and browse the Internet simultaneously, NAT and PAT handle all the translation in the background.

