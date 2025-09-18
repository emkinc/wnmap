# wnmap

**wnmap** is a terminal-based network analysis suite — *nmap-style workflow with a Windows-first experience*, plus cross‑platform support when run as a Python script. It’s designed to be simple for new users and powerful for pros.

**Documentation:** **[WNMAP Documents](https://wnmapdocuments.pages.dev/)**

> ⚠️ Only scan hosts and networks you are **explicitly authorized** to assess.

---

## ✨ Features

- Windows-first binary, works anywhere via Python (no UI, **terminal only**)
- **Self-setup to PATH**: `wnmap setup`
- **50+ commands** across TCP/UDP scans, HTTP/TLS, service probes, discovery, DNS/routing, and utilities
- **Concise reports** (text by default, optional `--json`)
- No ASCII banners — just **answers and good quality output**

---

## 🚀 Quick Start

### Option A — Windows (recommended)
1) Download or build `wnmap.exe`.
2) In a terminal:
   ```cmd
   wnmap setup
   ```
   This installs wnmap into `%USERPROFILE%\AppData\Local\Programs\wnmap\` and adds it to your **User PATH**.
3) Open a **new terminal** and run:
   ```cmd
   wnmap sysinfo
   ```

### Option B — Cross‑platform (Python)
```bash
python wnmap.py sysinfo
```
(Optional) Build a Windows console binary:
```bash
py -m PyInstaller --onefile --console wnmap.py
```

---

## 🧠 Usage

**Syntax**
```txt
wnmap <command> [arguments]
```

**Examples** (placeholders only)
```txt
wnmap scan HOST PORT
wnmap range HOST START-END
wnmap devices SUBNET/CIDR
wnmap httpget HOST [PORT]
wnmap httpsinfo HOST [PORT]
```

**JSON output**
```txt
wnmap --json scan HOST PORT
```

---

## 📄 Output Style

WNMAP prints clean reports (no banners), typically including:
- `target`, `ip`, `port`, `status`, `rtt_ms`
- `banner` / `data` when available
- TLS details (version, SANs, validity) for HTTPS endpoints

---

## 🧩 Commands

<details>
<summary><strong>Core TCP/UDP Scans</strong></summary>

```
setup
scan HOST PORT
range HOST START-END
allports HOST
top100 HOST
udp HOST PORT
banner HOST PORT
tcping HOST PORT
multi HOST P1,P2,P3
openonly HOST START-END
closedonly HOST START-END
```
</details>

<details>
<summary><strong>HTTP(S) & Service Probes</strong></summary>

```
httphead HOST [PORT]
httpget HOST [PORT]
httpsinfo HOST [PORT]
tlsver HOST [PORT]
robots HOST [PORT]
sitemap HOST [PORT]
ssh_banner HOST
ftp_banner HOST
smtp_banner HOST
pop3_banner HOST
imap_banner HOST
mysql_banner HOST
postgres_banner HOST
rdp_check HOST
smb_check HOST
vnc_check HOST
redis_check HOST
memcached_check HOST
mongodb_check HOST
elastic_check HOST
rabbitmq_check HOST
kafka_check HOST
docker_daemon HOST
rtmp_check HOST
ntp_check HOST
snmp_check HOST
coap_check HOST
stun_check HOST
```
</details>

<details>
<summary><strong>Discovery, DNS, Routing</strong></summary>

```
devices SUBNET/CIDR
ping HOST
tracert HOST
resolve NAME
reverse HOST
dnslookup NAME
mxlookup NAME
txtlookup NAME
ptrlookup IP
```
</details>

<details>
<summary><strong>Profiles & Utilities</strong></summary>

```
profile_fast HOST
sysinfo
whoami
time
save FILE {JSON...}
load FILE
--json <command> [...args]
```
</details>

---

## 🧪 Example Reports

**TCP port closed**
```txt
target: HOST
ip: 203.0.113.10
port: 8080
status: closed
```

**TCP port open with banner**
```txt
target: HOST
ip: 198.51.100.25
port: 80
status: open
rtt_ms: 22
banner: HTTP/1.0 200 OK
Server: ExampleServer/1.2
...
```

**TLS information**
```txt
target: NAME
ip: 203.0.113.20
port: 443
tls: TLSv1.3
rtt_ms: 31
subject: example.com
issuer: Example CA R3
notBefore: MMM DD HH:MM:SS YYYY GMT
notAfter:  MMM DD HH:MM:SS YYYY GMT
san:
- www.example.com
- example.com
```

**UDP probe (no response)**
```txt
target: HOST
ip: 203.0.113.55
port: 161
status: no-response (open|filtered?)
```

---

## 🧰 Troubleshooting

- **Command not found after `setup`:** open a **new terminal** so the updated PATH is loaded.
- **Firewall blocks:** ports can appear `closed`/`filtered` when a firewall or ACL drops packets.
- **High latency:** RTT can vary; re-run to confirm.
- **TLS/SNI:** for accurate TLS info, prefer the service **name** over raw IP.

---

## 🛡️ Responsible Use

Use WNMAP only on networks and systems where you have **explicit authorization**. You are responsible for complying with all applicable laws and policies.

---

## 🤝 Contributing

Issues and PRs are welcome. Please avoid submitting any scans or data from networks you do not control.

---

## 📜 License

Choose a license (e.g., MIT/Apache-2.0) and place it in `LICENSE`. Update this section accordingly.
