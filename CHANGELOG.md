# Changelog

## 2.2.1 — 2026-09-26

- New app icon: purple and mint usage bars on a black tile. It appears on the app, tray, windows, shortcuts and installer. Nothing else changes.

## 2.2.0 — 2026-09-25

- Retired the option that read Codex through the Codex app's own `codex.exe`. It ran whichever helper the Codex app shipped, which Glance could not verify. Codex is now tracked only through **Sign in with ChatGPT**, which uses a pinned, hash-verified official helper. If you used the old option, the Codex row explains how to switch until you sign in with ChatGPT or stop Codex monitoring; nothing else changes and your settings file is not rewritten.
- **Existing desktop connections…** is now **Claude desktop sign-in…** and only contains the Claude option and its data folder.
- The `GLANCE_CODEX_PATH` environment override is no longer used.

## 2.1.3 — 2026-09-25

- Claude checks keep the sign-in token in memory instead of decrypting Claude's saved sign-in every time. Decrypting calls Windows' security service (lsass). The cause of the September 23 LSASS crash is still unconfirmed, but Glance now makes that call about once per token instead of on every check. The token is read again when Claude renews it, when you switch accounts in Claude, when it has five minutes or less left, or if Claude rejects it. It is never written to disk.

## 2.1.2 — 2026-09-25

- Claude no longer shows STALE almost all the time. Claude's usage service rejects frequent checks (HTTP 429), and checking every minute kept hitting that limit. Claude now checks every 5 minutes by default, with 10 and 15 minutes available under Accounts → Refresh timing.
- STALE now means the numbers are actually old (more than two refresh intervals). A single failed check keeps the previous reading without the label; the reason is in the tooltip and Usage details.
- Codex checks every minute by default, with 1, 2, 5 and 10 minutes available. Saved 15- and 30-second settings move to 1 minute.
- Scheduled checks pause while Windows is locked or asleep, and run as soon as you unlock or wake the PC.

## 2.1.1 — 2026-09-23

- Keep one ChatGPT/Codex helper running and ask it for limits on each refresh, instead of starting and force-closing a new helper every time. This removes repeated forced helper termination; the cause of the reported Windows LSASS crash remains unconfirmed.
- Close helpers cleanly: end their input and let them exit on their own; force-close only one that is still running after a grace period.
- Verify the helper's hash once per start instead of on every refresh, and close the idle helper before account sign-in or sign-out.

## 2.1.0 — 2026-09-21

- Snap to compatible Glance Finance and Plex widgets using the shared v1 protocol. Enable or disable attraction in Options → Desktop → Snap to Glance widgets. Preserve locked positions, independent dragging, and saved settings.
- Match Finance's charcoal popup colors, subtle border, hover state and Segoe UI typography.
- Add Lock/Unlock position, Check for updates, and About to both widget and tray menus. Keep position locking synchronized with Desktop settings and show the current version in About.
- Match Glance Finance's 11-pixel corner radius and subtle one-pixel dark gray outline. Keep the usage widget compact, with its window shape and border scaling together.
- Match the Options header and navigation to Glance Finance: a Glance mark, white title, compact subtitle, rounded active tab and underline, and a dark Windows title bar. Retain the Usage mint accent and the existing clean page structure.


## 2.0.1 — 2026-09-21

- Keep right-click and tray menus to Options, Refresh, Show/Hide, and Exit. All settings now live in Options.
- Place used percentages and opacity in Appearance, account setup and refresh timing in Accounts, on-demand usage details in Overview, setup help in Support, and update controls in Updates.
- Remove repeated update buttons, navigation shortcuts, website lists, and explanatory cards. Preserve settings and provider connections.


## 2.0.0 — 2026-09-21

- Remove the repeated page headings below all six Options tabs. The selected tab identifies the page and content starts directly beneath navigation.
- Preserve provider connections, display preferences, and in-app updates.


## 1.2.0 — 2026-09-21

- Add a subscription-first provider hub with optional browser sign-in for ChatGPT/Codex; no Codex desktop app is required.
- Download a pinned official OpenAI helper only when signing in, verify both archive and executable hashes, and isolate the Glance account in Windows Credential Manager.
- Save website shortcuts for ChatGPT, Claude, Gemini, Grok, Perplexity, DeepSeek, Mistral Le Chat, and Microsoft Copilot. Clearly distinguish websites from live usage connections.
- Allow setup to finish before connecting any accounts, with a visible empty widget and no implicit local account access.
- Preserve existing Codex and Claude monitoring choices, display preferences, installer behavior, and self-installing updates.
- ChatGPT live readings cover Codex/Spark quotas, not every ChatGPT model. Browser-only live tracking for the other providers and API billing tracking are not included.


## 1.1.0 — 2026-09-21

- Add a full Options window with Overview, Accounts, Desktop, Appearance, Updates, and Support pages.
- Add live widget sizing, backgrounds, accent colors, monitor placement, startup controls, and desktop shortcut creation.
- Download, verify, install, and restart updates in the app, for installed and portable copies; preserve provider choices and settings.
- Use Glance LLM Usage consistently in the software and shortcuts. Opening the desktop shortcut opens Options.
- Preserve existing settings and use a per-user fallback when a portable app folder is read-only. Recover placement after monitor changes.

- Remove the automatic hover popup so it cannot cover the widget or its menus. Connection details and exact reset times are available through the Usage details menu item.

## 1.0.3 — 2026-09-15

- Detect newer stable releases at startup and daily; add manual update checks and optional links to the product download page.

## 1.0.2 — 2026-09-14

- Renamed the Codex, Spark, and Claude usage widget to Glance LLM Usage. Corrected app branding, installers, documentation, and repository links. Existing settings and provider choices are preserved. Updates remain manual.
- New installations use a distinct Glance LLM Usage Widget folder and shortcuts to avoid the mistakenly named finance 2.4.0 installation. The executable remains GlanceUsage.exe for compatibility.

## 1.0.1 — 2026-09-13

- New mint-and-lavender usage-gauge icon for the application, system tray, Windows shortcuts, and installer.
- The icon is embedded in the executable, so installed and portable copies need no separate icon file.

## 1.0.0 — 2026-09-13

- First public Windows release: compact, borderless widget with a true-black background.
- Codex and Spark limits, plus Claude's five-hour and overall weekly usage.
- Remaining/used percentages, progress bars, and reset countdowns.
- Codex checks every 15 seconds; Claude checks at most once per minute. Failed requests back off and preserve clearly marked stale readings.
- First-run account setup, independent provider selection, optional installation paths, and explicit opt-in for Claude's local sign-in.
- Drag to move; right-click for pinning, position lock, opacity, connections, and refresh options.
- Per-user Windows installer, optional shortcuts/startup, portable ZIP, and SHA-256 checksums.

The application and installer are unsigned. Updates are installed manually. Claude integration uses internal desktop sign-in storage and a usage endpoint that may change after provider updates.
