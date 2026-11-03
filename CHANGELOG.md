# Changelog

## v1.1.1 – 2026-11-03
- **New list item properties for Seren themes:** `aio_imax`, `aio_fel`, `aio_lang` and `aio_nlsubs`, with the text to show as value (`IMAX`, `FEL`/`P7`, `NL`/`MULTI`, `NL-SUBS`). Only set when they apply.
- **Tags in the title are now off by default** on new installs, so titles stay short. Turn *Show IMAX / FEL / language tags in title* on if your theme doesn't show the properties. Existing installs keep their current setting.

## v1.1.0 – 2026-11-03

### ✨ New
- **Tags in the title:** `IMAX`, `FEL` (or `P7` when only P7 is in the name), `NL` and `NL-SUBS`, e.g. `01. [IMAX FEL NL] Movie.2026.2160p.BluRay.REMUX…`. Can be turned off in the settings.
- **Language info for Seren:** `DUAL-AUDIO`, `MULTI-AUDIO`, `MULTI-SUB` and `CACHED` are passed to Seren's info line.
- **Remembers results** for 10 minutes (adjustable, `0` = off), so opening the same title again is instant. Includes a **Clear remembered results** button.
- **Test connection** button in the package settings: checks your manifest URL and runs a test search.
- **Manifest URL is masked** (`*******`) in the settings screen on new installs.
- **AIOStreams template** included in `template/ultra-dv-fel-remux.json`: 4K first, top remux groups, Dolby Vision FEL/P7, IMAX, Atmos/TrueHD/DTS:X scoring, Dutch preferred, failover, next-episode precache, 150 Mbps bitrate cap, and fake remuxes / regrades / upscales / 3D removed.

### 📝 Notes
- Updating keeps your existing settings; the new settings are added.
- Seren can't filter on language itself. The `NL` tags are for display; use the template to put Dutch first.

## v1.0.2 – 2026-11-01
- Seren's built-in update check now works (**Tools → Provider Tools → Check for updates**). Versions before 1.0.2 need one manual install.

## v1.0.1 – 2026-11-01
- 🔒 **Security fix:** a failed request no longer writes the manifest URL (which contains your encrypted config with debrid credentials) to `kodi.log`. (#1, thanks @minhgi)
- Package settings now have English names.

## v1.0.0 – 2026-10-27
- First release.
