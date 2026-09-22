# Glance LLM Usage setup and user guide

Glance LLM Usage brings live subscription limits and saved provider websites into one small Windows desktop app. It shows available percentages and reset countdowns without estimating missing quotas.

## Requirements

- Windows 10 or 11 on an x64-compatible computer, with Microsoft .NET Framework 4.8 or newer. macOS and Linux are not supported.
- Internet access and a browser for provider websites and ChatGPT sign-in.
- A ChatGPT account with Codex access for live Codex/Spark limits. You do not need the Codex desktop app when using browser sign-in.
- Optional legacy connections: an existing signed-in Codex executable, or Claude desktop signed in on the same Windows account.

No API key or developer billing setup is needed. Chat subscriptions and developer API billing are separate; this release focuses on subscriptions. Website access does not install provider apps or run models locally.

## Install

1. Download **Glance-LLM-Usage-v2.0.1-Setup.exe** from the [latest release](https://github.com/Brusko25/Glance-LLM-Usage-Releases/releases/latest).
2. Run the installer. It installs for your Windows account without requiring administrator access, normally in `%LOCALAPPDATA%\Programs\Glance LLM Usage`.
3. Choose optional desktop and Windows sign-in startup shortcuts if wanted.
4. Open Glance LLM Usage from the final installer page or Start menu. Complete Account setup.

The app and installer are unsigned; Windows can identify the publisher as unknown. The release includes `SHA256SUMS.txt` for checking download integrity.

For a portable copy, download **Glance-LLM-Usage-v2.0.1-Windows.zip**, extract all four files to a writable folder, and run `GlanceUsage.exe`. No compiler or developer tools are needed for either download. Avoid protected folders such as Program Files for a portable copy.

## Connect your accounts

On first launch, **Manage providers** appears before any usage request. You can choose **Save and continue** with no connections and sign in later. Open **Options → Accounts → Account setup** whenever you are ready.

### ChatGPT / Codex browser sign-in

1. Select **Sign in with ChatGPT**. On first use Glance downloads an official OpenAI account helper (about 73 MB, approximately 225 MB extracted on x64). Both the ZIP and executable must match pinned SHA-256 hashes before execution. This helper is not a model download.
2. Complete sign-in on the official OpenAI page in your default browser. Allow the browser's localhost callback. Glance waits up to ten minutes; Cancel stops the helper and pending callback.
3. After confirmation, select **Save and continue**. The widget reads the Codex/Spark limits available to your ChatGPT plan. It does **not** show every ChatGPT website model's message allowance.

The helper stores this Glance sign-in using Windows Credential Manager under a separate account profile. It does not read or replace your Codex desktop account. Browser passwords and tokens are never entered into Glance settings. The helper handles renewal. **Stop monitoring** disables readings when you save; **Sign out of Glance** removes this separate sign-in and saves the disconnected state immediately. Other apps retain their own sign-in.

The helper is pinned to OpenAI Codex app-server 0.155.1 in this release. App updates can change the supported helper version. Downloads happen only when you initiate sign-in, not when you open Accounts or launch the widget. Normal reads do not send prompts or create API usage charges.

### Other provider websites

Select the providers you use: **ChatGPT, Claude, Google Gemini, Grok, Perplexity, DeepSeek, Mistral Le Chat, and Microsoft Copilot**. Save these choices to put their buttons on Overview. **Open** launches the provider's official website in your browser; sign in there and check limits where the provider exposes them.

These are website shortcuts, not connected accounts. They do not scrape browser sessions, read usage automatically, or display invented percentages. Browser-only automatic subscription tracking for providers other than ChatGPT/Codex is not available in this version. API usage/spending integration is not included.

### Existing desktop connections (optional)

**Existing desktop connections…** retains the previous integrations and optional custom paths:

- **Codex:** enable the existing installation option to use its signed-in `codex.exe`. This replaces Glance's browser connection for monitoring. An API-key-only login cannot provide ChatGPT subscription quotas. Blank paths use automatic detection.
- **Claude:** open Claude desktop and sign in, then explicitly enable **Allow Claude usage reads using my desktop sign-in**. This authorizes local decryption of the signed-in Windows user's saved credential and its use only with Anthropic's usage endpoint. Glance does not save a copy or change Claude's authentication files. Claude handles renewal. Access starts off on a fresh install and can be disabled here.

Custom Claude paths must contain `config.json` and `Local State`. Default locations are `%LOCALAPPDATA%\Packages\Claude_pzs8sxrjxfjjc\LocalCache\Roaming\Claude` for the Store version and `%APPDATA%\Claude` for classic installs. Claude's desktop cache and usage endpoint are internal interfaces and may require compatibility updates.

Existing installations keep their saved monitoring choices. Every fresh installation starts with all local account access off.

## Controls

The widget and tray share a short menu: **Options**, **Refresh now**, **Hide to tray / Show widget**, and **Exit**. Settings and help stay in Options.

| Action | How |
| --- | --- |
| Move | Drag anywhere on the widget |
| Keep above other windows | Options → Desktop → Always on top |
| Stop accidental movement | Options → Desktop → Lock widget position |
| Switch remaining/used | Options → Appearance → Show used percentage |
| Refresh | F5, or right-click → Refresh now |
| Change connections | Options → Accounts → Account setup |
| Change opacity | Options → Appearance → Opacity |
| Hide | Escape, or right-click → Hide to tray |
| Show again | Double-click the tray icon, or launch Glance LLM Usage again |
| Quit | Right-click → Exit |

## Refresh and meaning

Codex defaults to a fresh request every **15 seconds**. Claude uses a minimum of **60 seconds**. Choosing a longer Codex interval also slows Claude when that interval exceeds 60 seconds. The timer starts after a request finishes. Reset labels are recalculated each second and displayed in whole minutes/hours.

Server processing delays and network latency can add lag. The widget shows the last value the provider returned; it does not estimate token use or promise instant readings. Failed requests retry more slowly, and `Retry-After` cooldowns are respected even when Refresh now is clicked.

Each provider updates independently. **STALE** means its previous reading is retained after a failure or delay. **OFFLINE** means there is no successful reading yet. Choose **Options → Overview → Usage details** to see connection details, each provider's last successful update, and exact reset dates in your local time zone.

Remaining is `100 − used percentage`. Missing values stay unavailable. A reset countdown reaching zero does not invent a fresh 100% quota; the next successful response must confirm it.

Codex reports the windows available for that account; a weekly-only limit is normal for some accounts. These are Codex limits, not all ChatGPT website message caps or API billing. Claude displays the five-hour window and **overall weekly** allowance, not a model-specific weekly sublimit.

## Troubleshooting

- **ChatGPT/Codex offline:** open Manage providers and sign in again. Check internet access, available disk space for the helper, localhost browser callbacks, and Windows Credential Manager access. A helper download failure leaves existing monitoring choices unchanged. For a legacy desktop connection, check the Codex app sign-in and optional executable path.
- **Claude sign-in unavailable or expired:** open Claude desktop and use the signed-in app so it can renew its credential, then allow the next retry. Glance LLM Usage never rotates Claude's tokens itself.
- **Multiple Claude organizations:** the widget will not silently select among multiple eligible organizations. Use the intended account in Claude; multi-organization selection is not supported in this release.
- **Cooldown/stale:** wait for the provider's cooldown. Repeated refresh clicks do not bypass it.
- **Cannot save settings:** check disk space and permissions. Read-only portable folders automatically use a per-user settings folder; find it under Options → Support. Updates still require write access to the application folder.
- **A provider update breaks monitoring:** check this project's releases. Claude's usage endpoint and encrypted desktop cache are internal interfaces, so compatibility may require a widget update.

Advanced environment overrides `GLANCE_CODEX_PATH` and `GLANCE_CLAUDE_DATA_DIR` are supported. Paths saved in Account setup take priority.

## Saved data, updates, and removal

`settings.json` holds position/display preferences and `connections.json` holds enabled providers, connection mode, saved website IDs, and optional local paths, beside the executable when writable, otherwise in a separate per-user folder under LocalAppData. Options → Support → Open settings folder opens the active location. No credentials, usage history, or raw API responses are stored in these settings files. Browser authentication is retained by the official helper in Windows Credential Manager. Its isolated profile and verified executable live under `%LOCALAPPDATA%\Glance LLM Usage\CodexAccount` and `Runtime`. Do not share these personal configuration files.

For an update, choose Options → Updates → Check for updates, then Install update. The app downloads the matching package, verifies its checksum, saves settings, installs, and restarts. You can still install a downloaded release manually. The release payload contains no configuration files; upgrades retain yours. Back up the two JSON files if you want to preserve settings before moving the app.

Uninstall through Windows Installed apps. It removes program files and installer-created shortcuts, while retaining your two configuration files. Delete the remaining Glance LLM Usage installation folder yourself if you also want to remove those preferences. Sign out of Glance before uninstalling if you also want its separate browser credential removed. The helper/profile folders are retained on uninstall and may be removed manually afterward. Your other Codex and Claude apps retain their own sign-ins.

Downloads and support: [Glance LLM Usage Releases](https://github.com/Brusko25/Glance-LLM-Usage-Releases). When reporting a problem, include the app version and the error shown in **Usage details**; never include credentials, provider data folders, or tokens.

The application and shortcuts are named **Glance LLM Usage**. Existing installations retain their folder and settings; the executable remains GlanceUsage.exe. The installer rejects folders containing Glance Finance.

## Options window

Open Options from the desktop/Start menu shortcut, right-click → Options, double-click the widget, or press Ctrl+O while the widget has focus. Closing Options keeps monitoring running; Quit app exits both.

- **Overview:** live readings, Refresh usage, expandable Usage details, and saved provider websites.
- **Accounts:** Account setup for browser sign-in, saved websites and optional desktop connections; Codex refresh timing. A website shortcut never indicates a live connection.
- **Desktop:** always on top, position lock, monitor selection, reset position, startup and desktop shortcut controls.
- **Appearance:** 75–200% widget sizing, Black/Graphite/Midnight backgrounds, Mint/Lavender/Amber Codex accents, 70–100% opacity, used/remaining percentages.
- **Updates:** automatic-check preference and in-app update installation.
- **Support:** setup guide, issues, settings folder, and keyboard shortcuts.

Controls are scrollable on smaller displays and scale with Windows display settings. Provider requests still honor minimum intervals and server cooldowns.

## Checking for new versions

Automatic checks run shortly after startup and daily, and can be disabled in Options. They only notify; installation starts when you choose **Install update**. Downloads are limited to this product's GitHub release URLs and verified against SHA-256 metadata before any app files change. Downloads can be cancelled before installation. The app saves settings before handing off, waits for the old process to exit, and reopens after installing. Portable replacement failures roll back the old files.

Installed copies update in their existing folder and retain startup choices. Portable copies need a writable application folder. No administrator rights are required for normal per-user installations. Existing v1.0.3 users need to install this release once using the downloaded installer; subsequent updates use the in-app installer.

This remains a Windows application: Windows 10/11 on x64-compatible systems with .NET Framework 4.8. macOS and Linux are not supported. Provider subscription eligibility still applies; only optional legacy connections require provider desktop apps.
