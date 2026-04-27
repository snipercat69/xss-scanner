# 🔬 EdgeIQ XSS Scanner

**Automated XSS vulnerability scanner for security professionals.**

Detect reflected XSS, DOM-based vulnerabilities, and injection vectors across web applications — with 24+ crafted payloads and intelligent context detection.

[![Project Stage](https://img.shields.io/badge/Stage-Beta-blue)](https://edgeiqlabs.com)
[![Python](https://img.shields.io/badge/Python-3.8+-green)](https://python.org)
[![License](https://img.shields.io/badge/License-MIT-orange)](LICENSE)

---

## What It Does

Scans web applications for **reflected XSS** and **DOM-based vulnerabilities** using 24+ crafted payloads across multiple injection contexts. Designed for authorized security auditing of applications you own or have explicit written permission to test.

> ⚠️ **Legal Notice:** Only scan targets you own or have explicit written permission to audit. Unauthorized scanning is illegal.

---

## Key Features

- **24 XSS Payloads** — script tags, event handlers, attribute injection, URL/encoding bypasses, null-byte tricks
- **6 Context Modes** — `html_body`, `html_attr`, `js_string`, `comment`, `css`, `url_param` — auto-detects vulnerable context
- **Crawl Mode** — auto-discovers links up to configurable depth, scans forms and URLs
- **Smart Filtering** — skips JSON/XML API responses automatically to reduce false positives
- **Concurrent Scanning** — multi-threaded with configurable worker count (default: 15)
- **Pure Python** — no external dependencies, no nmap required, works on Linux/WSL and Windows

---

## Prerequisites

- Python 3.8 or higher
- Network access to the target application
- **Written authorization** to test the target (required)

---

## Installation

```bash
# Clone the repo
git clone https://github.com/snipercat69/edgeiq-xss-scanner.git
cd edgeiq-xss-scanner

# No pip install needed — pure stdlib!
```

---

## Quick Start

### Single URL Scan
```bash
python3 scanner.py https://example.com
```

### Scan with Crawl
```bash
python3 scanner.py https://example.com --depth 2 --max-urls 30
```

### Intense Scan
```bash
python3 scanner.py https://example.com --depth 3 --max-urls 50 --workers 10 --follow-external
```

### Output Formats
```bash
python3 scanner.py https://example.com --format discord  # default
python3 scanner.py https://example.com --format json
python3 scanner.py https://example.com --format simple
```

---

## CLI Reference

| Flag | Type | Default | Description |
|------|------|---------|-------------|
| `url` | positional | — | Target URL to scan |
| `--depth` | int | 2 | Crawl depth (0 = no crawling) |
| `--max-urls` | int | 20 | Maximum URLs to scan before stopping |
| `--workers` | int | 15 | Concurrent worker threads |
| `--follow-external` | flag | False | Follow links to external domains |
| `--format` | choice | discord | Output format: `discord`, `json`, `simple` |
| `--burner` | flag | False | Route traffic through rotating proxies |

---

## Output Example

```
🚨 XSS Scan Report — `https://target.com`
> URLs: 14 | Params: 38 | Payloads: 912 | Time: 12.4s

⚠️ High Risk — 1 found
  `GET` `q` → `html_body`
  Payload: `<script>alert(1)</script>`
  Evidence: ...<script>alert(1)</script> reflected in HTML body...

Vulnerabilities found: 1
```

---

## Pricing

| Tier | Price | Features |
|------|-------|----------|
| **Free** | $0 | 24 payloads, crawl depth 2, single target |
| **Pro** | $15/mo | Full crawl with external links, JSON/CSV export, Slack/Telegram delivery, scheduled scans |
| **Lifetime** | $80 one-time | All Pro features, forever |

Get Pro via [EdgeIQ Labs](https://edgeiqlabs.com) — search "XSS Scanner" in ClawHub.

---

## Integration with EdgeIQ Tools

Part of the **EdgeIQ Labs** security toolkit:
- **[EdgeIQ Network Scanner](https://github.com/snipercat69/edgeiq-network-scanner)** — discover live hosts before scanning
- **[EdgeIQ SSL Watcher](https://github.com/snipercat69/edgeiq-ssl-watcher)** — monitor TLS health on discovered services
- **[EdgeIQ API Endpoint Discovery](https://github.com/snipercat69/edgeiq-api-endpoint-discovery)** — map API structure before scanning

---

## Architecture

- **Language:** Python 3 (pure stdlib — no external packages)
- **Dependencies:** None
- **Platforms:** Linux, macOS, Windows (WSL compatible)
- **Concurrency:** `concurrent.futures.ThreadPoolExecutor`
- **Crawl Strategy:** BFS with deduplication and depth tracking

---

## Troubleshooting

**Q: Scanner returns "No live host found" immediately**
A: Check that the URL is reachable. Try `curl -I <url>` first.

**Q: How do I scan a URL with query parameters?**
A: Pass the full URL: `python3 scanner.py "https://example.com/search?q=test"`

**Q: Scanner is slow**
A: Increase workers with `--workers 30` and reduce `--max-urls`.

---

## Legal & Ethical Use

This tool is for authorized security auditing only. Do not use against targets without explicit written permission.

---

## Support

Open an issue at: https://github.com/snipercat69/edgeiq-xss-scanner/issues

---

*Part of EdgeIQ Labs — [edgeiqlabs.com](https://edgeiqlabs.com)*
