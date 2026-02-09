# Lessons Learned – Azure SOC Honeypot Lab

This document summarizes key observations and takeaways from building and operating a cloud-based SOC honeypot using Microsoft Azure and Microsoft Sentinel.

---

## 1. Exposed Systems Are Discovered Quickly
Once the virtual machine was exposed to the public internet, failed authentication attempts began appearing within hours. The volume and consistency of attempts demonstrate how aggressively automated tools scan cloud IP ranges.

**Takeaway:**  
Any internet-facing system should be assumed hostile by default and protected accordingly.

---

## 2. Authentication Logs Are High-Signal
Windows Security Event ID **4625** (failed logon attempts) proved to be a reliable indicator of brute-force activity. Repeated failures from the same IPs and against common usernames made attack patterns easy to identify.

**Takeaway:**  
Authentication failures are one of the most valuable log sources for early detection in SOC environments.

---

## 3. Most Attacks Are Automated
The majority of observed activity targeted common accounts such as `Administrator`, `admin`, or generic usernames. The frequency and repetition strongly suggest automated brute-force tools rather than manual attackers.

**Takeaway:**  
SOC analysts must focus on patterns and aggregation rather than individual events.

---

## 4. Geolocation Adds Context, Not Attribution
Enriching IP addresses with geographic data helped visualize global attack trends. However, VPNs, proxies, and cloud infrastructure can make geolocation data inaccurate.

**Takeaway:**  
Geographic data is useful for trend analysis and visualization, but should not be used for definitive attacker attribution.

---

## 5. SIEM Value Comes From Filtering and Context
Raw logs alone are overwhelming. Meaningful analysis required filtering, aggregation, and enrichment using KQL queries to highlight actionable information.

**Takeaway:**  
Effective SIEM usage is about reducing noise and adding context, not just collecting logs.

---

## 6. Visualizations Support Investigation, Not Replace It
The Sentinel attack map provided a high-level overview of attack sources, but deeper investigation still required examining raw events and query results.

**Takeaway:**  
Dashboards are most effective when paired with analyst-driven investigation.

---

