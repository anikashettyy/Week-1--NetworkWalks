# 🔐 NetworkWalks Cybersecurity Lab — Week 1

### Kali Linux Setup, VirtualBox Networking & Connectivity Verification

![Platform](https://img.shields.io/badge/Platform-Kali%20Linux-557C94?logo=kalilinux&logoColor=white)
![Virtualization](https://img.shields.io/badge/Virtualization-Oracle%20VirtualBox-183A61?logo=virtualbox&logoColor=white)
![Focus](https://img.shields.io/badge/Focus-Network%20Configuration-blue)
![Week](https://img.shields.io/badge/NetworkWalks-Week%2001-gold)

## 📌 Project Overview

This repository documents my **Week 1 cybersecurity lab setup** as part of my NetworkWalks learning journey. The objective was to prepare a Kali Linux virtual machine in Oracle VirtualBox, configure a private NAT Network, apply network settings, test connectivity, verify the availability of Nmap, and create a VirtualBox snapshot as a recovery point.

The lab provides a controlled environment for learning Linux basics, virtual networking, connectivity troubleshooting, and foundational cybersecurity workflows. The screenshots in this repository record the setup and the tests performed.


## 🎯 Objectives

- Set up and launch Kali Linux in Oracle VirtualBox.
- Configure a dedicated VirtualBox NAT Network.
- Configure Kali Linux with an IPv4 address, subnet prefix, gateway, and DNS server.
- Inspect the VM's network interfaces and IP configuration.
- Test connectivity to the virtual gateway.
- Test external IP connectivity and DNS resolution.
- Check whether Nmap is installed and working.
- Create a VirtualBox snapshot to preserve a recovery point.
- Document the process with screenshots and command outputs.

## 🧰 Tools & Technologies

| Tool / Component | Purpose |
| --- | --- |
| Oracle VirtualBox | Runs and manages the Kali Linux virtual machine |
| Kali Linux | Linux environment for networking and cybersecurity practice |
| VirtualBox NAT Network | Provides a virtual network for lab machines |
| NetworkManager | Manages Kali Linux network connections |
| Nmap | Network discovery and port-scanning utility |
| `ping` | Tests IP reachability using ICMP echo requests |
| `nslookup` | Checks DNS name resolution |
| VirtualBox Snapshots | Saves a VM state that can be restored later |

## 🖥️ Lab Environment

| Setting | Configuration shown in the lab |
| --- | --- |
| Host operating system | Windows |
| Virtualization platform | Oracle VirtualBox |
| Guest operating system | Kali Linux (Debian 64-bit VM) |
| VM memory | 2048 MB |
| Virtual CPU allocation | 2 processors |
| Virtual network type | NAT Network |
| NAT Network name used for the Kali configuration | `NatNetwork1` |
| IPv4 network prefix | `10.0.0.0/24` |
| Kali IPv4 address configured | `10.0.0.2/24` |
| Default gateway configured | `10.0.0.1` |
| DNS server configured | `8.8.8.8` |
| Snapshot name | `week 1 snapshot` |

The VirtualBox Network Manager screenshot also shows another NAT Network named `NatNetwork` with prefix `10.0.2.0/24`. The Kali network settings shown in the screenshots use `NatNetwork1` and `10.0.0.0/24`.
](url)
## 🗺️ Network Layout

```text
                  Windows Host
                       |
                Oracle VirtualBox
                       |
              VirtualBox NAT Network
                  NatNetwork1
                 10.0.0.0/24
                       |
                Kali Linux VM
                 10.0.0.2/24
                       |
                Gateway: 10.0.0.1
                       |
               External connectivity
```

This is a conceptual layout based on the configured addresses. A successful gateway ping confirms reachability to `10.0.0.1`; separate tests are required to confirm Internet access and DNS resolution.

## ⚙️ Setup & Configuration

### 1. Launch Kali Linux

Kali Linux was imported into Oracle VirtualBox and launched successfully. The desktop screenshot shows the Kali Linux graphical environment.


### 2. Configure the VirtualBox NAT Network

In VirtualBox Network Manager, the `NatNetwork1` network is shown with the IPv4 prefix `10.0.0.0/24` and DHCP enabled.

![VirtualBox NAT Network configuration](screenshots/02-nat-network.jpeg)

**Configuration details:**
- Network name: `NatNetwork1`
- IPv4 prefix: `10.0.0.0/24`
- DHCP server: enabled in the shown VirtualBox network settings

If using a manually configured IP inside Kali, ensure the address is compatible with the selected network and is not already in use. Avoid assigning the same address to multiple machines.

### 3. Configure Kali Linux IPv4 settings

The Kali network connection editor shows a manual IPv4 configuration:

| Field | Value |
| --- | --- |
| Method | Manual |
| Address | `10.0.0.2` |
| Prefix / netmask | `/24` |
| Gateway | `10.0.0.1` |
| DNS server | `8.8.8.8` |

Save the settings and reconnect the network connection if necessary. Because the screenshot shows both DHCP enabled on the NAT Network and a manual guest IP, check that the guest address does not conflict with the DHCP pool or another device.

### 4. Verify the network interface and IP address

Run:

```bash
ip a
```

Review the active network interface and confirm that the expected IPv4 address (`10.0.0.2/24`, if the configuration has been applied) is present.

**Evidence status:** The supplied screenshots show the manual configuration.

### 5. Test gateway connectivity

Run:

```bash
ping -c 4 10.0.0.1
```
The supplied terminal screenshot shows successful replies from `10.0.0.1`, with four or more ICMP echo responses visible. This indicates that Kali can reach the configured gateway at the time of the test.

### 6. Test external IP connectivity

Run:

```bash
ping -c 4 8.8.8.8
```

Replies indicate IP-level reachability to that destination. If the command fails, check the NAT Network, default route, firewall rules, and whether ICMP traffic is permitted.


### 7. Test DNS resolution

Run:

```bash
nslookup networkwalks.com
```

A successful lookup should return DNS response information and one or more IP addresses. A timeout or resolution error can indicate DNS configuration or connectivity issues.

### 8. Verify Nmap

Use the correct version flag:

```bash
nmap --version
```

```

Only run Nmap scans against systems you own or have explicit permission to test.

### 9. Create a VirtualBox snapshot

A snapshot named **`week 1 snapshot`** is visible in VirtualBox's Snapshots view.

The snapshot preserves a recovery point for the VM at the time it was taken. Before future labs, consider creating another snapshot after confirming that the network configuration and tools are working as expected.

## ✅ Verification Checklist

| Test | Command / action | Expected result | Evidence status |
| --- | --- | --- | --- |
| Kali VM launch | Start the VM | Kali desktop opens | Shown in screenshot |
| NAT Network | VirtualBox Network Manager | `NatNetwork1`, `10.0.0.0/24` | Shown in screenshot |
| IPv4 configuration | Network connection editor | `10.0.0.2/24` and gateway `10.0.0.1` | Settings shown; `ip a` output still needed |
| Gateway connectivity | `ping -c 4 10.0.0.1` | Replies from gateway | **Successful replies shown** |
| External IP connectivity | `ping -c 4 8.8.8.8` | Replies from destination | Output screenshot still needed |
| DNS resolution | `nslookup networkwalks.com` | DNS response and resolved address | Output screenshot still needed |
| Nmap installation | `nmap --version` | Nmap version information | Initial command was incorrect; rerun required |
| Snapshot | VirtualBox Snapshots view | `week 1 snapshot` listed | Shown in screenshot |

## 🧯 Troubleshooting Notes

### Nmap returned “Failed to resolve 'version'”

The screenshot shows `nmap version`, which is not the version-check syntax. Use two hyphens:

```bash
nmap --version
```

### Gateway ping works, but Internet access does not

A successful gateway ping does not by itself prove that external Internet access or DNS is working. Check the configured default route, VirtualBox NAT Network, and connectivity to `8.8.8.8` separately.

Useful commands:

```bash
ip a
ip route
ping -c 4 10.0.0.1
ping -c 4 8.8.8.8
```

### DNS lookup fails

Confirm the DNS server configured for the active connection, then run:

```bash
cat /etc/resolv.conf
nslookup networkwalks.com
```

A DNS failure and an IP connectivity failure are different problems; test both independently.

### Static IP and DHCP

The VirtualBox screenshot shows DHCP enabled for `NatNetwork1`, while the Kali connection editor uses a manual address. Ensure the manually assigned IP is not allocated to another VM and does not conflict with the DHCP pool. For a multi-VM lab, use a documented address plan or a DHCP reservation where appropriate.

## 📚 Key Learnings

- How a virtual machine is launched and managed in Oracle VirtualBox.
- How a NAT Network provides a virtual network for lab machines.
- How IPv4 addresses, subnet prefixes, gateways, and DNS servers fit together.
- How to use `ip a`, `ping`, and `nslookup` to troubleshoot network configuration.
- Why a gateway test, an external IP test, and a DNS test verify different things.
- How to check a security tool's version using the correct command-line syntax.
- Why VM snapshots are useful recovery points before practical exercises.
- Why test results should be documented accurately with reproducible commands and screenshots.

## 🔒 Security & Ethical Use

This environment is intended for **education and authorized cybersecurity testing only**. Only scan devices, networks, and applications that you own or have explicit permission to assess. Keep experimental targets inside a controlled lab and follow applicable laws and course rules.

```

## 🏁 Conclusion

Week 1 established the initial Kali Linux virtual lab, configured the NAT Network and guest IPv4 settings, verified gateway reachability, and created a named VirtualBox snapshot. 
---

**Program:** NetworkWalks  
**Week:** 01  
**Project:** Cybersecurity Lab Setup  
**Environment:** Kali Linux + Oracle VirtualBox
