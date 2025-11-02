# Swarm Savvy: Transform Mainframe Testing with Open Source Tools

Presentation for Marist Computing Conference 2025 by Adam Munawar Rahman

## About

Modern load testing for IBM Z mainframes using Locust and Grafana k6. This talk covers:
- Bringing cloud-native testing tools to mainframes
- py3270 terminal automation with Locust
- Porting k6 to z/OS for native performance
- Open source contributions and sustainable tooling

## Running the Slides

### Prerequisites
- [Marp CLI](https://github.com/marp-team/marp-cli) or [Marp for VS Code](https://marketplace.visualstudio.com/items?itemName=marp-team.marp-vscode)

### View Slides

**Using Marp CLI:**
```bash
marp slides.md
```

**Using VS Code:**
1. Install the Marp for VS Code extension
2. Open `slides.md`
3. Click "Open Preview to the Side"

### Export to PDF
```bash
marp slides.md --pdf
```

### Export to HTML
```bash
marp slides.md --html
```

## Related Articles

- [Swarming Stressed Servers: Open-Source Load-Testing on z/OS Mainframes with Locust](https://medium.com/@theropod)
- [Go-ing Native: Porting Grafana k6 to z/OS with Go](https://medium.com/@theropod)
- [Ticks by Telnet: Load Testing IBM Z Mainframe Terminals with py3270 and Locust](https://medium.com/@theropod)

## Open Source Contributions

- [grafana/k6 PR #2892](https://github.com/grafana/k6/pull/2892) - z/OS build flags
- [SvenskaSpel/locust-plugins PR #206](https://github.com/SvenskaSpel/locust-plugins/pull/206) - py3270 terminal testing