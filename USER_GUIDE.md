# Glance LLM Usage setup and user guide

Glance LLM Usage is a small Windows desktop widget for your own Codex and Claude subscription limits. It shows percentages remaining (or used), progress bars, and reset countdowns. All options are under right-click.

## Requirements

- Windows 10 or 11 on an x64-compatible computer, with Microsoft .NET Framework 4.8 or newer.
- For Codex: the Codex desktop app or `codex.exe`, signed in with your ChatGPT account on this Windows user profile.
- For Claude: the Claude desktop app, signed in on this Windows user profile, with a plan that reports five-hour and weekly usage.
- An internet connection for fresh usage reads.

You can monitor either provider or both. Install the provider apps from their official websites: [Codex](https://openai.com/codex/) and [Claude desktop](https://claude.ai/download). A browser-only Claude sign-in is not enough for this version. No API key, payment information, token, or password is entered into Glance LLM Usage.

## Install

1. Download **Glance-LLM-Usage-v1.0.3-Setup.exe** from the [latest release](https://github.com/Brusko25/Glance-LLM-Usage-Releases/releases/latest).
2. Run the installer. It installs for your Windows account without requiring administrator access, normally in `%LOCALAPPDATA%\Programs\Glance LLM Usage Widget`.
3. Choose optional desktop and Windows sign-in startup shortcuts if wanted.
4. Open Glance LLM Usage from the final installer page or Start menu. Complete Account setup.

The app and installer are unsigned; Windows can identify the publisher as unknown. The release includes `SHA256SUMS.txt` for checking download integrity.

For a portable copy, download **Glance-LLM-Usage-v1.0.3-Windows.zip**, extract all four files to a writable folder, and run `GlanceUsage.exe`. No compiler or developer tools are needed for either download. Avoid protected folders such as Program Files for a portable copy.

## Connect your accounts

On the first launch, **Account setup** appears before any usage request.

**Codex:** leave “Monitor Codex and Spark” checked if you want those limits. Sign in to the Codex app with your ChatGPT account. Glance LLM Usage detects the desktop executable or a `codex.exe` on PATH. If detection fails, use Browse to select your installed `codex.exe`. An API-key-only Codex login does not provide ChatGPT subscription quotas.

**Claude:** first open Claude desktop and sign in. Check “Allow Claude usage reads using my desktop sign-in” only if you want Claude monitoring. This starts unchecked for every fresh download. Checking it authorizes Glance LLM Usage to decrypt that Windows user's saved Claude sign-in locally and use it only with Anthropic's usage endpoint. It never saves a copy of the credential or changes Claude's authentication files. Claude manages sign-in renewal.

Leave both optional paths blank for automatic detection. If using a nonstandard Claude install, browse to its desktop data folder containing `config.json` and `Local State`. Default locations are:

- Microsoft Store: `%LOCALAPPDATA%\Packages\Claude_pzs8sxrjxfjjc\LocalCache\Roaming\Claude`
- Classic desktop install: `%APPDATA%\Claude`

Select **Save & open**. Your selected providers appear in the widget. You can change or revoke either choice later through **right-click → Account setup**. Unchecking Claude stops its reads and removes its row. Each person uses their own Windows account and their own provider apps; the download contains no preconfigured personal account.

## Controls

| Action | How |
| --- | --- |
| Move | Drag anywhere on the widget |
| Keep above other windows | Right-click → Always on top |
| Stop accidental movement | Right-click → Lock position |
| Switch remaining/used | Right-click → Show used percentage |
| Refresh | F5, or right-click → Refresh now |
| Change connections | Right-click → Account setup |
| Change opacity | Right-click → Opacity |
| Hide | Escape, or right-click → Hide to tray |
| Show again | Double-click the tray icon, or launch Glance LLM Usage again |
| Quit | Right-click → Exit |

## Refresh and meaning

Codex defaults to a fresh request every **15 seconds**. Claude uses a minimum of **60 seconds**. Choosing a longer Codex interval also slows Claude when that interval exceeds 60 seconds. The timer starts after a request finishes. Reset labels are recalculated each second and displayed in whole minutes/hours.

Server processing delays and network latency can add lag. The widget shows the last value the provider returned; it does not estimate token use or promise instant readings. Failed requests retry more slowly, and `Retry-After` cooldowns are respected even when Refresh now is clicked.

Each provider updates independently. **STALE** means its previous reading is retained after a failure or delay. **OFFLINE** means there is no successful reading yet. Hover to see connection details, each provider's last successful update, and exact reset dates in your local time zone.

Remaining is `100 − used percentage`. Missing values stay unavailable. A reset countdown reaching zero does not invent a fresh 100% quota; the next successful response must confirm it.

Codex reports the windows available for that account; a weekly-only limit is normal for some accounts. These are Codex limits, not all ChatGPT website message caps or API billing. Claude displays the five-hour window and **overall weekly** allowance, not a model-specific weekly sublimit.

## Troubleshooting

- **Codex offline:** open Codex, check your ChatGPT sign-in and internet connection, then refresh. Use the optional executable path if detection fails.
- **Claude sign-in unavailable or expired:** open Claude desktop and use the signed-in app so it can renew its credential, then allow the next retry. Glance LLM Usage never rotates Claude's tokens itself.
- **Multiple Claude organizations:** the widget will not silently select among multiple eligible organizations. Use the intended account in Claude; multi-organization selection is not supported in this release.
- **Cooldown/stale:** wait for the provider's cooldown. Repeated refresh clicks do not bypass it.
- **Cannot save settings:** move the portable copy to a writable folder, or use the per-user installer.
- **A provider update breaks monitoring:** check this project's releases. Claude's usage endpoint and encrypted desktop cache are internal interfaces, so compatibility may require a widget update.

Advanced environment overrides `GLANCE_CODEX_PATH` and `GLANCE_CLAUDE_DATA_DIR` are supported. Paths saved in Account setup take priority.

## Saved data, updates, and removal

`settings.json` holds position/display preferences and `connections.json` holds enabled providers and optional local paths, beside the executable. No credentials, usage history, or raw API responses are saved. Do not share these personal configuration files.

For an update, exit the widget and run the newer installer, or replace the executable and documents from a newer portable ZIP. The release payload contains no configuration files; upgrades retain yours. Back up the two JSON files if you want to preserve settings before moving the app.

Uninstall through Windows Installed apps. It removes program files and installer-created shortcuts, while retaining your two configuration files. Delete the remaining Glance LLM Usage installation folder yourself if you also want to remove those preferences. Your Codex and Claude accounts are unaffected.

Downloads and support: [Glance LLM Usage Releases](https://github.com/Brusko25/Glance-LLM-Usage-Releases). When reporting a problem, include the app version and the error shown on hover; never include credentials, provider data folders, or tokens.

Version 1.0.2 renames Glance Usage to Glance LLM Usage. Existing installations retain their previous folder and settings; the executable remains GlanceUsage.exe. New installations and shortcuts use Glance LLM Usage Widget to keep them separate from the finance app that was mistakenly branded Glance LLM Usage in version 2.4.0. Use the usage widget installer only for this app. Installer upgrades preserve the existing startup selection.


## Checking for new versions

The app checks its public GitHub releases shortly after startup and daily. Choose **Check for updates** from the widget or tray menu to check immediately. When a newer stable version is available, you can open the release page. Downloads and installation remain manual; update checks send no account credentials or workspace data.
