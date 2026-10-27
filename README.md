# AIOStreams Scraper for Seren

A provider package for the Kodi add-on **[Seren](https://github.com/nixgates/plugin.video.seren)** that gets its sources from your own **[AIOStreams](https://github.com/Viren070/AIOStreams)** setup.

AIOStreams does the heavy lifting. It searches all your add-ons (Comet, StremThru, Easynews and more), filters out the junk and sorts the results. Seren shows the list and plays the stream.

---

## Features

- **One source for everything:** every add-on, debrid service and Easynews account you set up in AIOStreams comes into Seren through a single provider.
- **Keeps the AIOStreams order:** each title gets a number (`01.`, `02.`, …), so Seren lists streams in exactly the order AIOStreams sorted them. For example, 4K REMUX with Dolby Vision and Atmos stays on top.
- **Full stream details:** resolution, Dolby Vision, HDR, HYBRID, REMUX, BluRay, WEB, Atmos, TrueHD, DTS:X, DTS-HD MA, DD+, 7.1/5.1 and codec (HEVC/AVC/AV1) come straight from AIOStreams. Seren can filter and sort on them too.
- **File size included:** Seren's size filter works as normal.
- **Only playable streams:** uncached streams are hidden by default. You can turn them on in the settings.
- **Clear source labels:** for example `AIO|TORBOX` or `AIO|EASYNEWS`.
- **Movies and TV shows:** uses IMDb IDs, with TMDB IDs as a fallback.
- **Fails safely:** if AIOStreams can't be reached, Seren carries on with your other providers.

## How it works

1. You pick a movie or episode in Seren.
2. The scraper asks your AIOStreams instance for streams:
   `https://<your-aiostreams>/stremio/<your-config>/stream/movie/tt1234567.json`
3. AIOStreams searches, filters and sorts using your settings or template.
4. The scraper converts the response into Seren sources of type **direct**.
5. When you pick a source, Seren plays the AIOStreams link directly, and AIOStreams handles the debrid link behind the scenes.

The scraper asks AIOStreams for its extra stream metadata (`streamData`). That way Seren gets the details AIOStreams already parsed and doesn't have to guess them from the file name.

## Requirements

- Kodi with **Seren 3.x**
- A working **AIOStreams** configuration (public instance or self-hosted)
- A debrid service (e.g. TorBox, Real-Debrid) and/or **Easynews**, configured in AIOStreams
- Your AIOStreams **manifest URL**

---

## Installation

### Step 1: Download the package
Download `seren-aiostreams-provider.zip` from [Releases](../../releases). Do **not** unzip it.

### Step 2: Copy it to your device
Put the zip on the device that runs Kodi, for example:
- **Fire TV / Android TV:** use the *Send Files to TV* app or a USB stick
- **PC:** leave it in your Downloads folder

### Step 3: Install it in Seren
1. Open **Seren**.
2. Go to **Tools → Provider Tools → Install Package**.
3. Choose **Browse...** and select `seren-aiostreams-provider.zip`.
4. Confirm with **Install**.

> If you already have a package named `aiostreams`, this one replaces it.

### Step 4: Copy your manifest URL from AIOStreams
1. Open your AIOStreams configuration page.
2. Click **Save**.
3. Copy the **manifest URL**. It looks something like this:
   `https://your-aiostreams.com/stremio/xxxx/yyyy/manifest.json`

### Step 5: Enter the URL in Seren
1. Go to **Tools → Provider Tools → Manage Provider Packages → aiostreams**.
2. Select **AIOStreams manifest URL** and paste your URL.

> 💡 **Tip:** typing a long URL with a remote is a pain. With the **Kore** or **Yatse** app on your phone you can paste text straight into Kodi.

### Step 6: Configure Seren (recommended)
Go to **Seren → Settings → Sort & Filter**:

| Setting | Value | Why |
|---|---|---|
| **Sort Level 1** | `None` | Seren keeps the AIOStreams order |
| **Movie File Size limit** | `100` (GB) | Otherwise Seren hides large 4K remuxes |
| **Episode File Size limit** | `40` (GB) or higher | Same, for episodes |

Done! Search for a movie and the AIOStreams sources show up in the list.

---

## Package settings

You'll find these under **Tools → Provider Tools → Manage Provider Packages → aiostreams**.

| Setting | Default | Description |
|---|---|---|
| AIOStreams manifest URL | *(empty)* | Your personal manifest URL. Required. |
| Show uncached streams | Off | Turn on to also show streams that still need to download. |
| Keep AIOStreams order (numbering) | On | Puts numbers in front of titles so Seren follows the AIOStreams order. |
| Timeout (seconds) | 30 | How long the scraper waits for AIOStreams at most. |

---

## Tip: pair it with a good AIOStreams setup

This scraper shows exactly what AIOStreams returns. To get the best streams on top (4K REMUX, Dolby Vision P7/FEL, IMAX, Atmos, TrueHD, DTS:X), set that up in your AIOStreams sorting:

- Under *Sorting*, put **Resolution** at the top so 4K always comes before 1080p.
- Use *Ranked Stream Expressions* to give REMUX, Dolby Vision, Atmos and IMAX extra points.

---

## Troubleshooting

| Problem | Fix |
|---|---|
| No AIOStreams sources in the list | Check that the manifest URL is correct and the provider is **enabled** under Manage Provider Packages. |
| Large remuxes are missing | Raise the **File Size limit** in Seren (Step 6). |
| Order looks wrong | Set **Sort Level 1** to `None` and check your sorting in AIOStreams. |
| Only 1080p, no 4K | Check that **Max Resolution** is set to `4K` under Seren → Sort & Filter. |
| Stream won't start | Try the same stream in Stremio or Nuvio. If it fails there too, the problem is AIOStreams or your debrid service. |
| Finding errors | Turn on debug logging in Kodi and search the log for `[AIOStreams]`. |

---

## Limitations

- Plain **P2P torrents** without debrid are skipped. Only streams that play directly are passed through.
- There's no automatic update check. To update, install the new version through *Install Package*.

---

## File structure

```
seren-aiostreams-provider.zip
├── meta.json                          # package name, version and settings
├── providers/aiostreams/
│   └── en/
│       ├── __init__.py                # registers the provider as 'direct'
│       └── direct/aiostreams.py       # Seren hook (movie / episode)
└── providerModules/aiostreams/
    └── core.py                        # fetches from AIOStreams and converts to Seren sources
```

---

## Privacy

Your manifest URL contains your **encrypted AIOStreams configuration**, which gives access to your debrid and Easynews accounts. **Never share it**, and never post it in an issue or screenshot.

## Disclaimer

This package does not host or distribute any content. It only requests links from your own AIOStreams configuration. You are responsible for how you use it and for following the law and the terms of the services you use.

This project is not affiliated with Seren, AIOStreams, Kodi or any debrid service.
