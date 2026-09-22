# Changelog

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
