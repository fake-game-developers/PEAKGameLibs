# FakeGameDevelopers PEAKGameLibs

Fork of [loco-choco/PEAKGameLibs](https://github.com/loco-choco/PEAKGameLibs): stripped and publicized PEAK Managed assemblies for mod CI.

NuGet package id: **`FakeGameDevelopers.PEAKGameLibs`** (the original `PEAKGameLibs` id on nuget.org is owned by Locochoco and cannot be updated from this fork).

Current libs: **PEAK 2.5.a** → package version **2.5.0**.

## Consume (GitHub Packages)

```bash
dotnet nuget add source "https://nuget.pkg.github.com/fake-game-developers/index.json" \
  --name fake-game-developers \
  --username YOUR_GITHUB_USERNAME \
  --password YOUR_GITHUB_PAT \
  --store-password-in-clear-text
```

Then reference `FakeGameDevelopers.PEAKGameLibs` 2.5.0, or unzip the `.nupkg` `lib/` folder for `-p:ManagedDir=`.

CI also uploads the `.nupkg` as a workflow artifact on every push to `main`.

## Regenerate after a PEAK update

1. Start from a clean PEAK install (no extra/modded Managed DLLs).
2. Drag `PEAK.exe` onto `strip-assembiles.bat` (uses `tools/NStrip.exe`).
3. Set `<version>` in `package/GameLibs.nuspec` to match the game (`version.txt`).
4. Push to `main` — Actions packs and publishes.

`strip-assembiles.bat` strips with [NStrip](https://github.com/BepInEx/NStrip) and publicizes `Assembly-CSharp.dll` / `Assembly-CSharp-firstpass.dll`.

## nuget.org (optional)

Add repo secret `NUGET_KEY` to also push to nuget.org. Without it, only GitHub Packages + the artifact are published.
