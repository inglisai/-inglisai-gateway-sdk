# INGLIS AI — High-Concurrency Edge Security Gateway & Telemetry Middleware
**Patent Pending — U.S. Patent Application No. 19/853,850 (Filed October 27, 2026)**  
**Inventor & Architect:** Christopher Hughes | Inglis Advanced Infrastructure LLC  
**Official Website:** https://://inglisai.com

---

## Overview
**INGLIS AI** is a single-pass, asynchronous edge API and Layer-1 Web Application Firewall (WAF) middleware architecture engineered to eliminate external cache round-trip latency, floating-point precision drift, and blocking observability overhead in high-throughput financial and industrial telemetry environments.

## Core Architectural Innovations
- **Zero-Allocation O(1) Microsecond Rate Gate:** Uses an in-memory `collections.deque` sliding window driven by monotonic `time.perf_counter()` counters to deflect traffic surges (`>= 30 Req/Sec`) via HTTP `429` in **1.44 µs** before payload deserialization or external network calls occur.
- **Edge Schema & Hardware Validation Vault:** Parses raw JSON numeric literals directly into exact fixed-point `Decimal` types (eliminating IEEE-754 `float64` rounding anomalies) while verifying device-bound `X-Hardware-Security-ID` headers in **4.53 µs**.
- **Length-Prefixed Binary Framing & Keep-Alive Pooling:** Serializes verified payloads into compact 4-byte big-endian binary frames routed over persistent TCP socket connection pools.
- **Out-of-Band Non-Blocking Telemetry:** Decouples microsecond latency profiling via an isolated background worker queue (`put_nowait`) so observability I/O never blocks the critical request path.

---

## Verified Sandbox Benchmarks (50-Request Concurrent Burst)

| Test Scenario | Outcome / HTTP Status | Mean Internal Latency |
| :--- | :--- | :--- |
| **Cleared Concurrent Traffic (`< 30 Req/Sec`)** | `200 OK` (Vault Cleared & Framed) | **79.65 µs** (`0.079 ms`) |
| **Excess Traffic Surge (`>= 30 Req/Sec`)** | `429 Too Many Requests` (Layer-1 Block) | **1.44 µs** (`0.0014 ms`) |
| **Spoofed Hardware Security ID** | `422 Unprocessable Entity` (Vault Reject) | **4.53 µs** (`0.0045 ms`) |
| **Decimal Precision Overflow** | `422 Unprocessable Entity` (Vault Reject) | **42.20 µs** (`0.042 ms`) |

---

## Commercial Subscription Tiers (Self-Hosted Edge Licenses)
All commercial tiers are issued as **Self-Hosted Edge Licenses**, allowing licensees to deploy and operate the gateway inside their own cloud, on-premise, or edge server infrastructure with zero third-party data exposure.

| Tier | Rate | Capacity & Nodes | Support & Action |
| :--- | :--- | :--- | :--- |
| **Sandbox Evaluation** | **Free (14 Days)** | 1 test node · Up to 10,000 test requests | Internal sandbox benchmarking · [Request Trial](https://://inglisai.com) |
| **Growth Tier** | **$150 / Month** | Up to **3** concurrent downstream nodes · **500,000** payloads/mo | Email anomaly diagnosis · **[Subscribe — $150/mo](https://buy.stripe.com/7sYcMYetFdHP59N4j15AQ00)** |
| **Enterprise Tier** | **$1,000 / Month** | Up to **15** concurrent downstream nodes · **5,000,000** payloads/mo | Priority patches & telemetry review · **[Subscribe — $1,000/mo](https://buy.stripe.com/4gM6oAetFbzHau73eX5AQ01)** |
| **Custom Institutional** | **Custom Annual Contract** | **Unlimited** nodes & multi-region clustering | Custom SLAs & hardware ID integration · **[Request Quote](https://://inglisai.com)** |

---

## Request a Sandbox Key or Commercial Lease
Source code is proprietary and protected under **U.S. Patent Application No. 19/853,850**.
- **Project Intake & Licensing Portal:** [://inglisai.com](https://://inglisai.com)
- **Direct Engineering Contact:** flacmh@gmail.com | (352) 585-1266
