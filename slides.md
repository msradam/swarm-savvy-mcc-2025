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
  content: attr(data-marpit-pagination) ' / 13';
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

## What Are Mainframes?

Every credit card swipe, ATM withdrawal, airline booking.

**30+ billion transactions per day.** 90% of credit card transactions.  
92 of the top 100 banks use IBM mainframes.

**Problem:** Testing tools stuck in the 1980s.

---

## The Gap

**Mainframe Load test tools (TPNS, Jmeter, IBM Workload Simulator):**
- Archaic interfaces, sporadic documentation
- Manually defined configurations
- Limited extensibility and CI/CD integration

**Modern load testing (Locust, k6):**
- Modern scripting, CI/CD native
- Massive communities, excellent docs
- Cross-platform skills

**Can we bring industry-standard tools to mainframes?**

---

## The Bridge: z/OS REST APIs

**z/OS components now expose HTTP endpoints:**

**z/OSMF** - System management (jobs, datasets, consoles)  
**z/OS Connect** - CICS, IMS, Db2, batch programs  
**Zowe API Mediation Layer** - Unified API gateway  
**CICS native** - Direct REST/JSON support in CICS TS

**This means:** If a tool can make HTTP requests, it can drive z/OS for testing.

**The door is open.** Now we just need the right tools.

---

## The Solution: Adapt, Don't Reinvent

**Two proven tools. Two adaptations.**

🐍 **Locust** (Python) - EA/DICE, AWS, Learnosity [1]
   → Extended with py3270 plugin for terminal testing

⚡ **k6** (Go) - GitLab, Carvana, fuboTV, Olo  [2]
   → Ported to run natively on z/OS

**The insight:** Modern tools already exist.  
We just made them work on mainframes.

1.
2.

---

## How This Works: Two Patterns

**Pattern 1: External control node** (Locust, py3270)
```
Your Laptop/Jenkins  --HTTP-->  z/OS (z/OSMF, CICS, Zowe)
                     --Telnet->  z/OS (3270 terminals)
                     --SSH/FTP--> z/OS (Unix System Services)
```

**Pattern 2: Native on z/OS** (k6)
```
z/OS USS (k6 binary)  --localhost-->  z/OSMF, CICS, Zowe
                                      (same LPAR / sysplex)
```

**External:** Run from CI/CD. **Native:** Mainframe tests itself.

**No agents. No mainframe installation for external tools.**

---

## Why These Tools?

**Scale:** Simulate millions of concurrent users [1]
**Flexibility:** Dynamic load shapes that change throughout tests  
**Distributed:** Run across multiple machines for massive load  
**Extensible:** Rich plugin ecosystems for both tools  
**Observable:** Real-time metrics and performance monitoring

**Locust uses 14-30x less memory than Apache JMeter [2]:** Modern, event-driven architecture.
<k6 metrics memory usage>

1. Source?
2. Source ?

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

**Built py3270 plugin** for 3270 terminal testing (locust-plugins PR #206).

---

## k6: Native on z/OS ⚡

**The challenge:** Performance + portability. Run tests 24/7 on the mainframe itself.

**The solution:** Ported k6 to z/OS (added build flags, fixed dependencies).
```javascript
export default function() {
  http.post('https://localhost/zosmf/restjobs/jobs', jobData);
}
```
```bash
$ k6 run test.js --vus 1000 --duration 24h
```

**Compiled Go binary. Runs natively. No external dependencies.**

**Ported upstream** - grafana/k6 PR #2892

---

## Why This Matters

**Your team already knows these tools.**

**Before:**
- $$$/year vendor licenses
- Mainframe specialists only
- Separate CI/CD pipelines

**After:**
- Open source: $0
- Any Python/JavaScript/Go developer
- One pipeline for everything

**The real win:** Transferable skills. Lower costs. No vendor lock-in.

---

## Real-World Impact at IBM Z Test 🎯

**Deployed in production:**
- IBM Wazi as a Service - Locust testing z/OSMF APIs
- System testing - Terminal workflows with py3270
- Customer simulation - k6 running natively on z/OS

**Testing capabilities:**
REST APIs • 3270 Terminals • Batch Jobs • Mixed Workloads • CI/CD Gates

**The proof:** Three production environments. Zero vendor tools.

---

## Try It Yourself

**Install:**
```bash
pip install locust py3270
# or  
brew install k6  # macOS
# or
go install go.k6.io/k6@latest  # Any platform with Go
```

**Read the journey:**
Medium: @msradam
- "Swarming Stressed Servers" (Locust + z/OSMF)
- "Ticks by Telnet" (py3270 plugin)
- "Go-ing Native" (k6 porting process)

**Start small:** Pick one vendor test. Rewrite it. See the difference.

---

## Questions?

**Adam Munawar Rahman**  
Staff Software Developer @ IBM  
M.S. Computer Engineering Student @ NYU Tandon

🌐 adamr.io  
📧 Medium: @msradam  
💻 github.com/msradam

*"Don't reinvent the wheel—install one through pip."*