<div align="center">

```
███████╗██╗   ██╗███████╗
██╔════╝╚██╗ ██╔╝██╔════╝
█████╗   ╚████╔╝ █████╗  
██╔══╝    ╚██╔╝  ██╔══╝  
███████╗   ██║   ███████╗
╚══════╝   ╚═╝   ╚══════╝
```

# 👁️ EYE — OSINT Email Intelligence Tool

**An automated, async Python tool for email-based Open Source Intelligence gathering**

![Python](https://img.shields.io/badge/Python-3.8%2B-blue?style=for-the-badge&logo=python)
![License](https://img.shields.io/badge/License-MIT-green?style=for-the-badge)
![Status](https://img.shields.io/badge/Status-Active-brightgreen?style=for-the-badge)
![OSINT](https://img.shields.io/badge/Category-OSINT-red?style=for-the-badge)

</div>

---

## 📌 About

**EYE** is a powerful open-source intelligence (OSINT) tool designed to perform comprehensive email footprinting. Given a target email address, EYE asynchronously queries **10+ platforms** to discover linked accounts, profile data, and potentially leaked information — all from a single command.

Built for cybersecurity researchers, digital forensic analysts, and brand protection investigators.

> ⚠️ **Disclaimer:** This tool is intended for **legal and ethical use only** — authorized investigations, brand protection, fraud research, and cybersecurity education. Do not use this tool against individuals without proper authorization. The author is not responsible for any misuse.

---

## ✨ Features

- 🔍 **Email Reconnaissance** — Discovers accounts across 10+ platforms from a single email
- ⚡ **Async Architecture** — All platform checks run simultaneously using `asyncio` + `httpx` for maximum speed
- 🤖 **Bot Detection Evasion** — Rotates user-agent strings to mimic real browsers
- 💧 **Data Breach Detection** — Checks Pastebin for leaked credential dumps containing the target email
- 🧠 **Facial Recognition** — OpenCV + perceptual hashing to identify and match profile images across platforms
- 📧 **Email Validation** — Regex-based format validation before any queries are made
- 🎨 **Clean Terminal Output** — Color-coded, structured results for quick reading

---

## 🎯 Platforms Investigated

| Platform | What's Checked |
|----------|----------------|
| 🐦 **Twitter / X** | Account existence & profile data |
| 📸 **Instagram** | Account existence & public profile |
| 🐙 **GitHub** | Developer account & public repos |
| 🔒 **ProtonMail** | Secure email account check |
| 📬 **Mail.ru** | Russian email platform registration |
| 🦜 **Duolingo** | Language learning account |
| 🖼️ **Gravatar** | Linked profile picture & username |
| 🖼️ **Imgur** | Image hosting account |
| 😊 **Bitmoji (Snapchat)** | Avatar account check |
| 📋 **Pastebin** | Leaked data & breach exposure |

---

## 🗂️ Project Structure

```
EYE---OSINT-/
│
├── eyes.py                      # Main entry point
├── output.py                    # Result display & orchestration
├── requirements.txt             # Python dependencies
├── useragents.txt               # User-agent rotation list
│
├── lib/
│   ├── cli.py                   # Command-line argument parser
│   ├── maileye.py               # Email decomposition & regex validation
│   └── text.py                  # Terminal color/style utilities
│
├── modules/
│   └── email_modules/           # One module per platform
│       ├── duolingo.py
│       ├── gravatar.py
│       ├── imgur.py
│       ├── protonmail.py
│       ├── bitmoji.py
│       ├── x.py
│       ├── github.py
│       ├── mailru.py
│       ├── pastebin.py
│       └── ig.py
│
├── facial_recognition/          # Face detection & image matching
└── assets/                      # Static assets
```

---

## ⚙️ Installation

### Prerequisites
- Python 3.8 or higher
- pip

### Steps

```bash
# 1. Clone the repository
git clone https://github.com/Yadavpiyush07/EYE---OSINT-.git

# 2. Navigate into the directory
cd EYE---OSINT-

# 3. Install dependencies
pip install -r requirements.txt
```

---

## 🚀 Usage

```bash
python eyes.py --email target@example.com
```

### Example Output

```
###############target@example.com###############

- 🙋 Name   : target
- 🔎 Domain : example.com

[+] ProtonMail  : No account found
[+] Mail.ru     : Account exists
[+] Duolingo    : Account found — username: target_user
[+] Gravatar    : Profile picture linked — https://gravatar.com/...
[+] Imgur       : No account found
[+] Bitmoji     : No account found
[+] Twitter/X   : Account found — @target_handle
[+] GitHub      : Account found — github.com/target
[+] Instagram   : Account found — @target_insta
[~] Paste       :
    ├── https://pastebin.com/xXxXxXxX
    ├── https://pastebin.com/yYyYyYyY
```

---

## 🧩 Dependencies

| Library | Purpose |
|---------|---------|
| `httpx` | Async HTTP client for fast parallel requests |
| `requests` | Synchronous HTTP requests |
| `argparse` | Command-line argument parsing |
| `opencv-python` | Computer vision & facial recognition |
| `imagehash` | Perceptual image hashing for profile photo matching |
| `bs4` | HTML parsing / web scraping |
| `scrape-search-engine` | Automated search engine queries |
| `datetime` | Result timestamping |

Install all at once:
```bash
pip install -r requirements.txt
```

---

## 🧠 How It Works

```
Input Email
     │
     ▼
┌─────────────┐
│ Regex Check │  ← Validates email format
└─────────────┘
     │
     ▼
┌──────────────────┐
│ Email Decompose  │  ← Splits into name + domain
└──────────────────┘
     │
     ▼
┌─────────────────────────────────────────────┐
│         Async Platform Queries              │
│  [ProtonMail] [GitHub] [Instagram] [X]      │
│  [Gravatar] [Imgur] [Duolingo] [Bitmoji]    │
│  [Mail.ru]  [Pastebin]                      │
└─────────────────────────────────────────────┘
     │
     ▼
┌──────────────────┐
│  Formatted       │
│  Terminal Output │
└──────────────────┘
```

All platform queries run **simultaneously** (not sequentially) thanks to Python's `asyncio` library, making investigations significantly faster.

---

## 🛡️ OSINT Tradecraft Features

- **User-Agent Rotation** — Randomly selects browser signatures from `useragents.txt` to avoid bot detection and rate-limiting
- **Async Requests** — Parallel queries reduce total investigation time from minutes to seconds
- **Pastebin Breach Check** — Searches public paste dumps for the target email (common indicator of credential leaks)
- **Perceptual Image Hashing** — Matches profile photos across platforms even if images are resized, cropped, or slightly modified

---

## 🔭 Use Cases

- 🏢 **Brand Protection** — Trace fake seller identities on e-commerce platforms
- 🕵️ **Digital Forensics** — Build identity profiles during cybercrime investigations  
- 🔐 **Security Auditing** — Check your own organization's email exposure
- 📚 **OSINT Research** — Academic and educational threat intelligence work
- 🚨 **Fraud Investigation** — Identify and link fraudulent accounts to real identities

---

## 🔮 Planned Features

- [ ] WHOIS & domain lookup integration
- [ ] Shodan IP/infrastructure check
- [ ] LinkedIn account discovery
- [ ] Telegram username search
- [ ] JSON / CSV export of results
- [ ] Web dashboard UI
- [ ] Batch email investigation mode

---

## 👤 Author

**Piyush Yadav**  
GitHub: [@Yadavpiyush07](https://github.com/Yadavpiyush07)

---


## ⚠️ Legal Notice

This tool is provided for **educational and authorized security research purposes only**.  
Always obtain proper written authorization before investigating any individual or organization.  
Unauthorized use may violate applicable laws including the **IT Act, 2000 (India)** and international cybercrime statutes.  
The developer assumes no liability for misuse of this tool.

---

<div align="center">

*"The eye sees everything, but the wise knows better than to react to all it sees."*

⭐ Star this repo if you found it useful!

</div>
