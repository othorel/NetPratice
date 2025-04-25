# 🌐 NetPractice - 42

<p align="center">
  <img src="https://github.com/leogaudin/42_project_badges/blob/main/badges/netpractice_bonus.webp"/>
</p>

Welcome to NetPractice, a 42 project designed to sharpen your understanding of computer networks. This project helps you learn how IP addressing, subnetting, and routing work in a hands-on, puzzle-like environment. You'll practice configuring and troubleshooting small virtual networks in a visual interface.

---

## 📋 Project Overview

| **Category**            | **Details**                                                                                      |
|-------------------------|--------------------------------------------------------------------------------------------------|
| **Goal**                | Solve network configuration challenges by connecting devices correctly using IP addressing.      |
| **Tool Used**           | Web-based simulator provided by 42 (via intranet).                                               |
| **Concepts Covered**    | IP Addresses, Netmasks, Gateways, Subnetting, Routing, Network Topology.                         |

---

## 🚀 Key Concepts

1. **IP Addressing & Subnetting**:
   - Understand and assign valid IP addresses and subnet masks.
   - Use CIDR notation to define network ranges.

2. **Network Routing**:
   - Learn how packets travel from one network to another using gateways and routing tables.

3. **Troubleshooting**:
   - Analyze broken networks and fix misconfigurations.
   - Understand common issues like wrong IPs, missing routes, or improper masks.

4. **Visual Learning**:
   - Each level provides a drag-and-drop UI for configuring network devices.

5. **No Code Required**:
   - Purely focused on network logic, not implementation.

---

## 🗂️ File Structure

> This project is web-based and doesn’t require code submission, but you may want to organize your own notes or resources locally:

| **File/Folder**        | **Purpose**                                                                 |
|------------------------|------------------------------------------------------------------------------|
| `solutions/`           | (Optional) Store screenshots or notes for each level.                       |
| `subnet_calc.sh`       | (Optional) Bash script to help calculate subnet ranges quickly.            |
| `README.md`            | Project description and resources.                                          |

---

## 💻 Usage

The project is accessed via the **42 Intranet**:

1. Go to the project page for **NetPractice**.
2. Launch the web-based simulator.
3. Start solving levels by assigning IP addresses, configuring routes, and connecting networks.
4. Click "Validate" once you think the configuration is correct.

---

## 🧪 Tips & Tricks

- Use the **IP/Subnet calculator** (like `ipcalc` or an online tool) for help.
- Remember the basic subnet rules:
  - Devices on the same subnet can communicate directly.
  - Devices on different subnets need a router (gateway).
- Double-check your **default gateways**.
- Validate each level progressively; fix small pieces first.

---

## 📚 Resources

- [IP Subnet Calculator](https://www.subnet-calculator.com/)
- [Cisco Subnetting Tutorial](https://www.cisco.com/c/en/us/support/docs/ip/routing-information-protocol-rip/13788-3.html)
- [CIDR Chart](https://www.ripe.net/about-us/press-centre/understanding-cidr/)

---

<h1 id="NetPractice">
Net Practice
</h1>

<details>
  <summary>Level 1</summary>
  <br>
  
![level01](https://github.com/othorel/NetPratice/blob/main/img/level1.png)

The first exercise on the list is a simple problem of direct communication between each 2 devices. You need to make sure that each two devices that need to communicate between each other are, in fact, in the same network.

For Client A and Client B, who have both have subnet masks of `255.255.255.0` or CIDR `/24`, you need to make sure that the IP Address for A matches the same Network from B, which is `104.94.23.0/24`. That means Client A IP Address can be from range `104.94.23.1` from ``104.94.23.254` (remembering the extremities from the range are reserved for network and broadcast, respectively).

For Client C and Client D, the same rule applies, but now they both have subnet masks of `255.255.0.0` or CIDR `/16`. Therefore, you need to make sure that the IP Address for D matches the same Network fromC, which is `211.191.0.0/16`. That means Client D IP Address can be from range `211.191.0.1` from ``211.191.255.254`.

</details>

---

<details>
  <summary>Level 2</summary>
  <br>

![level02](https://github.com/othorel/NetPratice/blob/main/img/level2.png)

For this level, it's important to keep a few things in mind.

First, it's the necessity for all devices in the same network to have the same mask.

Second, you cannot use reserved IPs for private addresses that are not specific for this use.

For the connection between Client A and Client B, both of them must have the same mask `255.255.255.224`, or CIDR `/27`. Since the IP Address for Client B is already set in `192.168.36.222`, then you can infer that the network range is between `192.168.36.192` and `192.168.36.223`, extremities excluded. Client A can be anywhere within this range.

For CLient C and Client D, however, we have a mask of `255.255.255.252`, or CIDR `/30`. For this mask, we only have 4 IPs in range, and only 2 available for use. When you choose the IPs for them, you must make sure they are not reserved, and that the 2 last bits are not all 0s (first in range) nor all 1s (reserved for broadcast).

</details>

---

<details>
  <summary>Level 3</summary>
  <br>

![level03](https://github.com/othorel/NetPratice/blob/main/img/level3.png)

This is the first contact we have with switches. Its use is quite similar to the previous exercises, the only difference now beeing the possibility of communication between 3 separate devices.

All 3 clients must be on the same network. The mask for Client C is set as `255.255.255.128`, or CIDR `/25`. Therefore, this will be the mask for every other host. And the IP Address for Client A is set on `104.198.73.125`, so we can also infer that the range for this particular network can only be from `104.198.73.0` and `104.198.73.127`, extremities excluded.

</details>

---

<details>
  <summary>Level 4</summary>
  <br>

![level04](https://github.com/othorel/NetPratice/blob/main/img/level4.png)

This exercise introduces the concept of a router. This router in particular has 3 separate interfaces, each with an IP Address and a Subnet Mask.

When choosing the IP Address and Mask for the router R **Interface R1**, you must make sure that there are no overlaps of IP ranges between interfaces.

**Interface R2**, for example, has a range of IPs from `63.12.111.0` and `63.12.111.127`, while **Interface R3** has a range from `63.12.111.192` and `63.12.111.255`. Therefore, you must make sure the mask you choose for this particular network will not cause it to share any of those IPs.

To do so, take a look at the IP Address from Client A, set in `63.12.111.132`. This IP is located exactly in between the ranges previously mentioned. There are only 63 possible addresses in this area (`63.12.111.128` - `63.12.111.191`), so you can use a mask of CIDR `/27` or above. I chose a mask of `255.255.255.240`, or CIDR `/28`, for reassurence.

Applying this mask on the IP Address of Client A, we have the range from `63.12.111.128` to `63.12.111.143`, extremities excluded, all the while making sure there are no overlaps in router R.

</details>

---

<details>
  <summary>Level 5</summary>
  <br>

![level05](https://github.com/othorel/NetPratice/blob/main/img/level5.png)

In this exercise, a Routing Table is introduced for the first time. The idea here is that each host must have a routing table that can connect to the router and each other.

First, let's start stablishing the IP addresses and Mask for each host.

Client A must be located on the same network as Interface R1. To do so, it must share the same mask `255.255.255.128` or CIDR `/25` and must be in the range of Addresses between `74.150.109.0` and `74.150.109.127`, extremities excluded.

Client B must be located on the same network as Interface R2. To do so, it must share the same mask `255.255.192.0` or CIDR `/18` and must be in the range of Addresses between `158.42.64.0` and `158.42.127.255`, extremities excluded.

Now, let's configure the routing tables. For client A, you must set it up in a way that it can allow communication with client B. To do so, you have two options: either you point out the destination IP as the address for client B (`158.42.127.42/18`), or you leave it at **default** (`0.0.0.0/0`).

The next hop for both tables will be the IP address of the respective router R Interface - the closest point of connection will allow for the communication to establish.

</details>

---

<details>
  <summary>Level 6</summary>
  <br>

![level06](https://github.com/othorel/NetPratice/blob/main/img/level6.png)

This level introduces the concept of the Internet.

The Internet is simply a sort-of-router that has many interfaces in which it can connect. The purpose for this exercise is to connect client A all the all to the Internet.

First, let's set all IP Addresses and Masks. For client A and router R's Interface R1, which are in the same local network via switch, we must set them with the same mask `255.255.255.128` or CIDR `/25`.

Interface R1 must have an IP in the range of `45.149.96.128` and `45.149.96.255`, extremities excluded.

Now, for the routing tables, we must have in mind that we must connect client A to the Internet and vice-versa.

Client A route destination must be the **Interface Somewhere on the Net**, witch is `8.8.8.8/16` or **default**. The next hop for this table is the router R's Interface R1 IP, `45.149.96.254`, the next logical step to connect to the Internet.

Internet I route destination must be the Interface A1 IP, which is `45.149.96.227/25`, of simply **default**., since the next hop for this route is the Router R's Interface R2.

The router R routing table, however, has a next hop which doesn't match any Interface IP in the schema, so you can set it's destination to **default**, since it won't impact the other connections.

</details>

---

<details>
  <summary>Level 7</summary>
  <br>

![level07](https://github.com/othorel/NetPratice/blob/main/img/level7.png)

In this level, the concept of overlapping is fundamental to its resolution.

When analyzing the schema, you are able to notice the existence of three separate networks.

- **Network 1**: Between Interface A1 and Interface R11
- **Network 2**: Between Interface R12 and Interface R21
- **Network 3**: Between Interface R22 and Interface C1

Each one of theses networks must have their own range of IPs and can have their own subnet masks. There can be no overlaps of IPs between networks of the same router.

Since the only two IPs from Router R1's Interface are already set, then you must choose the masks of these netwqorks carefully. The easiest way to do this is to choose a mask that can split the network into small-range subnets. I chose a CIDR of `/28` for all the networks, which gives me 16 total IP Addresses each, more than enough for this particular situation.

It's important to notice, though, that you don't need to pick the same mask for all networks. IUt's all up to you, really.

With a mask of `/28` we can then choose the IPs for each host as follows:

- **Network 1**: From `119.198.14.0` to `119.198.14.15` (extremities excluded, as well as Interface R11's own IP of `119.198.14.1`)
- **Network 2**: From `119.198.14.240` to `119.198.14.255` (extremities excluded, as well as Interface R12's own IP of `119.198.14.254`)
- **Network 3**: You can chose the best IPs based on your own criteria. I picked a range from `119.198.14.128` to `119.198.14.143` (extremities excluded).

After setting the appropriate IP Addresses, you need to fill in the routing tables accordingly, considering that client A's destination must be client C's Interface IP, and vice versa. The routers must have their next hops as each other's Interfaces to allow forward and backward communication as well.

</details>

---

<details>
  <summary>Level 8</summary>
  <br>

![level08](https://github.com/othorel/NetPratice/blob/main/img/level8.png)

In this level, you need to establish communication with the internet from two different hosts: client C and client D.

The internet has a routing table with a destination route of `163.14.136.0/26`. That mean that it can send back packets from IPs ranging from `163.14.136.0` to `163.14.136.63`.

That means that all networks on the way to the packets final destination must be within this range, without their IPs overlapping each other.

As the previous exercise, we also have 3 networks to establish:

- **Network 1**: Between Interface C1 and Interface R22
- **Network 2**: Between Interface D1 and Interface R23
- **Network 3**: Between Interface R21 and Interface R13

The easiest solution is to split the total range into 4 using a mask of `/28`.

Considering that the next hop for the router R2's routing table is `163.14.136.62`, this should be the IP Address for the Interface R13.

With those constraints in mind, you can assign the IPs as follows: 

- **Network 1**: From `163.14.136.16` to `163.14.136.30` (extremities excluded)
- **Network 2**: From `163.14.136.0` to `163.14.136.15` (extremities excluded)
- **Network 3**: From `163.14.136.48` to `163.14.136.63` (extremities excluded).

After that, fill in the routing tables considering that Routers R1 and R2's next hops must be each others, and the destination of clients C and D must be default.

</details>

---

<details>
  <summary>Level 9</summary>
  <br>

![level09](https://github.com/othorel/NetPratice/blob/main/img/level9.png)

This level is an aggregation of all concepts previously seen in this exercise list.

To start, as usual, you need to access all the IP Addresses correctly. Keep in mind which Addresses are reserved, and which belong to the same network.

There are 4 configurable networks in this level:

- **Network 1**: Between Interface A1, Interface B1 and Interface R11
- **Network 2**: Between Interface C1 and Interface R22
- **Network 3**: Between Interface D1 and Interface R23
- **Network 3**: Between Interface R13 and Interface R21

For each Network there is a specific mask and IP Adress range. For my resolution, I chose the following settings:

- **Network 1**: Mask `/25`, and IP Adresses ranging from `142.168.31.0` and `142.168.31.127`.
- **Network 2**: Mask `/24`, and IP Adresses ranging from `42.42.42.0` and `42.42.42.244`.
- **Network 2**: Mask `/18` (pre-set), and IP Adresses ranging from `102.155.128.0` and `102.155.128.255` (Interface R23 is already pre-set to the client D routing table next hop IP`102.155.167.244`).
- **Network 2**: Mask `/30` (pre-set), and IP Adresses ranging from `37.219.16.252` and `37.219.16.255`.

After that, we need to set the routing tables to allow access between networks. The most important one is the Internet Routing Table, that must have the *meson* and the *cation* addresses, since they are the two hosts that need to communicate directly to it.

</details>

---

<details>
  <summary>Level 10</summary>
  <br>

![level10](https://github.com/othorel/NetPratice/blob/main/img/level10.png)

This is one of the most straightforward exercises in this list.

The majority of the settings are already pre-configured. All you need to pay attention to is the overlapping. Since the internet has only onr route configured to the Router R1, then all networks must be withing the same range, without overlapping the subnets.

We have here 4 networks:

- **Network 1**: Between Interface H11, Interface H21 and Interface R11
- **Network 2**: Between Interface H31 and Interface R22
- **Network 3**: Between Interface H41 and Interface R23
- **Network 4**: Between Interface R21 and Interface R13
  
For each Network there is a specific mask and IP Adress range. For my resolution, I chose the following settings:

- **Network 1**: Mask `/25`, and IP Adresses ranging from `169.222.32.0` and `169.222.32.127`.
- **Network 2**: Mask `/28`, and IP Adresses ranging from `169.222.32.224` and `169.222.32.239`.
- **Network 2**: Mask `/26`, and IP Adresses ranging from `169.222.32.129` and `169.222.32.129`.
- **Network 2**: Mask `/30`, and IP Adresses ranging from `169.222.32.252` and `169.222.32.255`.

And then, you must configure the routing tables accordingly, having in mind that the internet routing table consists in a single destination of IP `169.222.32.0/24`.

</details>

---

## 🤝 Contributing

This project doesn’t require code, but feel free to share your notes, subnetting cheat sheets, or scripts that help with the logic. You can fork this repo and submit pull requests to improve the documentation or help others with subnetting tools!
