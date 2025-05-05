---
bg: "tools.jpg"
layout: post
title:  SSH Port Fordwarding
crawlertitle: SSH Port Fordwarding
summary: SSH Port Fordwarding
date:   2022-11-05
categories: posts
tags: [linux]
author: jfdzar
---

I saw in this [Twitter thread ](https://twitter.com/iximiuz/status/1587451857143828481?s=20&t=39hV0-Y0ddEWjCrD9tkZJQ). It is about SSH Port fordwarding which I found interesting and I have needed it a couple of times, so here is a copy and short explanation of it:

If these problems sound familiar:

- A DB server listens on a remote **localhost**, but you want to use a **local GUI client**  
- A dev service runs on your laptop, but you want to **expose it to the Internet**  

…and you don't know the solution, read on 👇

🔐 **SSH Port Forwarding** is the trick.

---

## 🔁 There are 3 main types

### 1. Local Port Forwarding
Tunnel traffic from your **local machine** to a **port on a remote server**.

```bash
ssh -L local_port:remote_host:remote_port user@ssh_server
```

🧠 Example: Forward a remote Postgres DB on port 5432 to your localhost:

```bash
ssh -L 5432:localhost:5432 user@remote
```

Now you can connect your GUI client to `localhost:5432`.

---

### 2. Remote Port Forwarding
Expose a **local service** to a **remote server**.

```bash
ssh -R remote_port:localhost:local_port user@ssh_server
```

🧠 Example: Make a local Flask app (port 5000) reachable from the remote server:

```bash
ssh -R 5000:localhost:5000 user@remote
```

On the remote server, open `http://localhost:5000`.

---

### 3. Dynamic Port Forwarding (SOCKS Proxy)
Create a SOCKS proxy tunnel through SSH.

```bash
ssh -D local_port user@ssh_server
```

🧠 Configure your browser to use `localhost:local_port` as a SOCKS5 proxy to route traffic through SSH — like a mini VPN.

---

## 🛠️ Tips & Tricks

- Use `-N` to skip remote command execution:
```bash
ssh -N -L 5432:localhost:5432 user@remote
```

- Add `-f` to send the command to the background:
```bash
ssh -f -N -L 5432:localhost:5432 user@remote
```

- Combine with `-v` for verbose debugging if things don’t work:
```bash
ssh -v -L 5432:localhost:5432 user@remote
```


Hope this helps demystify SSH tunnels! 🚀