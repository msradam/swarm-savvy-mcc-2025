---
marp: true
---

<style>
@import url('https://fonts.googleapis.com/css2?family=IBM+Plex+Sans:wght@400;600;700&family=IBM+Plex+Mono:wght@400;600&display=swap');

section {
  background-color: #161616;
  color: #f4f4f4;
  font-family: 'IBM Plex Sans', 'Helvetica Neue', Arial, sans-serif;
  padding: 48px 64px;
}

h1 {
  color: #f4f4f4;
  font-size: 54px;
  font-weight: 600;
  line-height: 1.2;
  margin-bottom: 16px;
  border-bottom: 2px solid #0f62fe;
  padding-bottom: 16px;
}

h2 {
  color: #f4f4f4;
  font-size: 32px;
  font-weight: 600;
  line-height: 1.25;
  margin-bottom: 24px;
  margin-top: 0;
}

h3 {
  color: #c6c6c6;
  font-size: 20px;
  font-weight: 600;
  margin-bottom: 16px;
}

p, li {
  font-size: 18px;
  line-height: 1.5;
  color: #f4f4f4;
}

a {
  color: #78a9ff;
  text-decoration: none;
  border-bottom: 1px solid #78a9ff;
}

a:hover {
  color: #a6c8ff;
  border-bottom-color: #a6c8ff;
}

strong {
  color: #ffffff;
  font-weight: 600;
}

code {
  background-color: #262626;
  color: #78a9ff;
  padding: 2px 8px;
  border-radius: 2px;
  font-family: 'IBM Plex Mono', 'Menlo', 'Courier New', monospace;
  font-size: 16px;
}

pre {
  background-color: #1e1e2e;
  border: 2px solid #45475a;
  padding: 24px;
  border-radius: 8px;
  margin: 20px 0;
}

pre code {
  background-color: transparent;
  padding: 0;
  color: #cdd6f4;
  font-size: 18px;
  line-height: 1.8;
  font-weight: 500;
}

/* Catppuccin Mocha syntax highlighting */
pre code .hljs-keyword,
pre code .language-python .hljs-keyword,
pre code .token.keyword {
  color: #cba6f7 !important;
}

pre code .hljs-string,
pre code .language-python .hljs-string,
pre code .token.string {
  color: #a6e3a1 !important;
}

pre code .hljs-function,
pre code .language-python .hljs-function,
pre code .token.function {
  color: #89b4fa !important;
}

pre code .hljs-class,
pre code .language-python .hljs-class,
pre code .token.class-name {
  color: #f9e2af !important;
}

pre code .hljs-comment,
pre code .token.comment {
  color: #6c7086 !important;
}

ul, ol {
  margin: 16px 0;
  padding-left: 24px;
}

li {
  margin-bottom: 8px;
}

blockquote {
  border-left: 4px solid #0f62fe;
  padding-left: 16px;
  margin: 24px 0;
  color: #c6c6c6;
  font-style: italic;
}

section::after {
  content: attr(data-marpit-pagination) ' / 14';
  position: absolute;
  bottom: 24px;
  right: 64px;
  font-size: 14px;
  color: #8d8d8d;
  font-family: 'IBM Plex Mono', monospace;
}

section em {
  color: #78a9ff;
  font-style: normal;
  font-weight: 600;
}

section mark {
  background-color: #0f62fe;
  color: #ffffff;
  padding: 2px 8px;
  border-radius: 2px;
  font-weight: 600;
  font-size: 14px;
}

section:first-of-type {
  display: flex;
  flex-direction: column;
  justify-content: center;
}

section:first-of-type h1 {
  font-size: 64px;
  border-bottom: 4px solid #0f62fe;
  padding-bottom: 24px;
  margin-bottom: 32px;
}

section:first-of-type p {
  font-size: 20px;
  color: #c6c6c6;
  margin: 8px 0;
}
</style>

# Transform Mainframe Testing with Open Source Tools

**Adam Munawar Rahman**  
Staff Software Developer @ IBM  
Medium: @msradam

Marist Computing Conference 2025

---

## What is Load Testing?

**Simulating real-world traffic at scale to verify system resilience.**

**When inadequate testing causes catastrophic failures:** [1,2]

- **Ticketmaster (Nov 2022)** - Taylor Swift presale: 3.5B system requests (4x previous peak). Site crashed. Testing hadn't accounted for unprecedented traffic spikes.

- **TSB Bank (Apr 2018)** - £330M cost, 6M customers locked out for weeks. IT migration without full-volume testing in production-like environment. IBM identified insufficient performance testing.

**The impact of proper load testing:** [3]  
Teams using modern load testing practices report **45% latency reduction, 2x throughput gains, and 70% faster response times**.

Load testing reveals capacity limits and bottlenecks *before* they impact millions of customers.

<style scoped>
section {
  font-size: 18px;
}
.footnote {
  font-size: 10px !important;
  color: #8d8d8d;
  margin-top: 32px;
  line-height: 1.2;
}
.footnote p {
  font-size: 10px !important;
}
</style>

<div class="footnote">

[1] "Why Load Testing is Important: The Taylor Swift Debacle," TESTINGMIND, Dec. 2022  
[2] "TSB Bank Data Migration Failure," iceDQ, Jan. 2025  
[3] N. Yadav, "Real-World Examples of Performance Testing Failures," Testriq, Sep. 2025

</div>

---

## What Are Mainframes?

The backbone of global commerce and critical systems.

**30+ billion transactions daily. 90% of all credit card transactions. [1]**  
**92 of the top 100 banks run on IBM mainframes. [1]**

**The problem?** Testing tools frozen in the 1980s.

<style scoped>
section {
  font-size: 18px;
}
.footnote {
  font-size: 10px !important;
  color: #8d8d8d;
  margin-top: 32px;
  line-height: 1.2;
}
.footnote p {
  font-size: 10px !important;
}
</style>

<div class="footnote">

[1] IBM, "IBM Mainframe Ushers in New Era of Data Protection," Jul. 2017

</div>

---

## The Gap

| **Legacy Tools**<br>TPNS (1976) • JMeter (1998) • WSim (2002) | **Modern Tools**<br>Locust (2012) • k6 (2016) |
|---|---|
| **Resource efficiency:**<br>Thread-per-user (1MB+ per thread)<br>Few thousand users max [1,2] | **Resource efficiency:**<br>Event-driven: **14-30x less memory**<br>**100K+ users** per machine [1,2] |
| **Developer experience:**<br>GUI config, proprietary scripting (REXX/STL),<br>XML management, complex setup [3,4] | **Developer experience:**<br>**Tests-as-code** in Python/JavaScript<br>`pip install` or single binary [3,4] |
| **CI/CD integration:**<br>Steep learning curve, slow GUI,<br>plugin management, heap tuning [5,6] | **CI/CD integration:**<br>**CLI-native**, pipeline-ready<br>Zero infrastructure [5,6] |
| **Performance at scale:**<br>Resource-constrained, lower RPS [2,7] | **Performance at scale:**<br>**36% higher RPS**, 200ms better p95 [2,7] |

**The breakthrough:** Modern tools + REST APIs = mainframe accessibility.

<style scoped>
section {
  font-size: 16px;
}
table {
  margin-top: 16px;
  width: 100%;
  table-layout: fixed;
}
th {
  background-color: #262626;
  color: #78a9ff;
  font-size: 19px;
  padding: 10px;
  text-align: left;
  border-bottom: 2px solid #0f62fe;
  width: 50%;
}
td {
  padding: 14px 10px;
  vertical-align: top;
  line-height: 1.5;
  width: 50%;
}
tr:nth-child(even) {
  background-color: #1a1a1a;
}
.footnote {
  font-size: 9px !important;
  color: #8d8d8d;
  margin-top: 20px;
  line-height: 1.2;
}
.footnote p {
  font-size: 9px !important;
}
</style>

<div class="footnote">

[1] N. van der Hoeven, "Comparing k6 and JMeter," Grafana Labs, Feb. 2024  
[2] T. Koot, "k6 vs. JMeter - Head2Head," LinkedIn, Oct. 2021  
[3] B. Roy, "JMeter vs k6," TestVagrant Medium, Dec. 2022  
[4] "JMeter vs. Locust," PFLB, Mar. 2025  
[5] S. Mamoru, "Advanced Performance Testing with JMeter," Geek Culture Medium, Jun. 2023  
[6] "LoadRunner vs JMeter," BrowserStack, May 2025  
[7] "Performance Tools Benchmarking," QAInsights, May 2022

</div>

---

## The Bridge: Two Enablers

**1. z/OS REST APIs - The modern interface:**

z/OSMF • z/OS Connect • Zowe API ML • CICS REST  
HTTP requests = mainframe testing

**2. Open-source tooling - The connectivity layer:** [1,2,3,4]

**x3270/c3270/py3270** - 3270 terminal emulation & automation  
**ZOAU** - z/OS automation utilities (Python, shell, Node.js)  
**Galasa** - Integration testing framework (3270, REST, batch, web)  
**tnz** - Python 3270 library for terminal automation

**The breakthrough:**  
Modern tools + modern APIs + open-source bridges = mainframe accessibility

<style scoped>
section {
  font-size: 17px;
}
.footnote {
  font-size: 10px !important;
  color: #8d8d8d;
  margin-top: 32px;
  line-height: 1.2;
}
.footnote p {
  font-size: 10px !important;
}
</style>

<div class="footnote">

[1] "py3270: Python interface to x3270," IBM GitHub, 2025  
[2] "IBM Z Open Automation Utilities," IBM, 2024  
[3] "Galasa - Open Source Testing Framework," Open Mainframe Project, 2024  
[4] "tnz: Tn3270 to Z Python library," IBM GitHub, 2025

</div>

---

## The Solution: Adapt, Don't Reinvent

**Two industry-proven tools. Two strategic adaptations.**

🐍 **Locust** (Python) - Used by EA/DICE, AWS, Learnosity [1]
   → Extended with py3270 for 3270 terminal testing

⚡ **k6** (Go) - Used by GitLab, Carvana, Olo [1]  
   → Ported to run natively on z/OS

**The breakthrough:** Modern tools already exist.  
We just made them work on mainframes.

<style scoped>
section {
  font-size: 18px;
}
.footnote {
  font-size: 10px !important;
  color: #8d8d8d;
  margin-top: 32px;
  line-height: 1.2;
}
.footnote p {
  font-size: 10px !important;
}
</style>

<div class="footnote">

[1] "k6 Testimonials," k6.io, 2025

</div>

---

## Why These Tools?

**Technical advantages:** [1]  
• Scale: Millions of concurrent users  
• Modern architecture: 10-30x more efficient than JMeter  
• Flexibility: Dynamic load patterns, distributed testing  
• Observable: Real-time metrics, rich plugin ecosystems

**Industry adoption & results:** [2,3,4]

**EA/DICE (Locust):** "Mandatory part of development of any large scale HTTP service at DICE"

**Grafana (k6):** "Managed to identify bottlenecks and errors in code before shipping" • "Ensures no performance regression reaches production"

**AWS endorsement:** Published official guides for using Locust on their infrastructure

<style scoped>
section {
  font-size: 17px;
}
.footnote {
  font-size: 10px !important;
  color: #8d8d8d;
  margin-top: 32px;
  line-height: 1.2;
}
.footnote p {
  font-size: 10px !important;
}
</style>

<div class="footnote">

[1] N. van der Hoeven, "Comparing k6 and JMeter," Grafana Labs, Feb. 2024  
[2] "Locust testimonials," Locust.io, 2025  
[3] M. Bergquist, "How we use k6 for developing Grafana," Grafana Labs, Aug. 2021  
[4] "Using Locust on AWS Elastic Beanstalk," AWS DevOps Blog, Jun. 2022

</div>

---

## How This Works: Two Patterns

**Pattern 1: External control** (Locust + py3270)
```
Laptop/CI → HTTP  → z/OSMF, CICS, Zowe
         → Telnet → 3270 terminals (via py3270)
         → SSH    → Unix System Services
```

**Pattern 2: Native execution** (k6)
```
z/OS USS → localhost → z/OSMF, CICS, Zowe
        (same LPAR/sysplex)
```

**External:** Run from anywhere. **Native:** The mainframe tests itself.

**Zero agents. Zero mainframe installation footprint.**

---

## Locust: Python Ecosystem 🐍
```python
class MainframeUser(HttpUser):
    @task
    def submit_job(self):
        response = self.client.put("/zosmf/restjobs/jobs", 
                                    data=jcl)
        assert response.json()["jobid"]
```

**Open source contribution:** Built py3270 plugin for 3270 terminals [1]  
**Merged:** locust-plugins PR #206

<style scoped>
section {
  font-size: 18px;
}
.footnote {
  font-size: 10px !important;
  color: #8d8d8d;
  margin-top: 32px;
  line-height: 1.2;
}
.footnote p {
  font-size: 10px !important;
}
</style>

<div class="footnote">

[1] A. Rahman, "Plugin for Telnet 3270 User," locust-plugins PR #206, Mar. 2024

</div>

---

## k6: Native on z/OS ⚡

**The challenge:** Run performance tests 24/7 on the mainframe itself.

**The solution:** Ported k6 to z/OS—added build flags, fixed dependencies [1]
```javascript
export default function() {
  http.post('https://localhost/zosmf/restjobs/jobs', jobData);
}
```
```bash
$ k6 run test.js --vus 1000 --duration 24h
```

**Compiled Go binary. Native execution. Zero external dependencies.**

<style scoped>
section {
  font-size: 18px;
}
.footnote {
  font-size: 10px !important;
  color: #8d8d8d;
  margin-top: 32px;
  line-height: 1.2;
}
.footnote p {
  font-size: 10px !important;
}
</style>

<div class="footnote">

[1] A. Rahman, "Update ui_unix.go with z/OS build flags," k6 PR #2892, Feb. 2023

</div>

---

## Why This Matters

**Your team already has these skills.**

**Before:**
- $$$/year vendor licenses
- Mainframe specialists only
- Isolated tooling

**After:**
- Open source: $0
- Any Python/JS/Go developer
- Unified CI/CD pipeline

**The win:** Transferable skills. Lower costs. Zero vendor lock-in.

---

## Real-World Impact at IBM Z Test 🎯

**Production deployments:**
- **Wazi as a Service** - Locust + z/OSMF APIs
- **System testing** - py3270 terminal workflows  
- **Customer simulation** - k6 native on z/OS

**Full testing stack:**
REST APIs • 3270 Terminals • Batch Jobs • Mixed Workloads • CI/CD Gates

**The proof:** Three production environments. Zero legacy tools.

---

## Try It Yourself

**Install:**
```bash
pip install locust py3270
# or  
brew install k6  # macOS
# or
go install go.k6.io/k6@latest  # Any platform
```

**Read the journey:**
Medium: @msradam
- "Swarming Stressed Servers" (Locust + z/OSMF)
- "Ticks by Telnet" (py3270 plugin)
- "Go-ing Native" (k6 porting)

**Start:** Pick one legacy test. Rewrite it. See the difference.

---

## Questions?

**Adam Munawar Rahman**  
Staff Software Developer @ IBM  
M.S. Computer Engineering Student @ NYU Tandon

🌐 adamr.io  
📧 Medium: @msradam  
💻 github.com/msradam

*"Radical efficiency."*