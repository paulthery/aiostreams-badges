# Install

Everything happens in the AIOStreams app (desktop or web). Badges, quick
filters and custom CSS do not exist in Stremio.

Files used: `badges.json`, `badges.css`, `quick-filters.json`.
Images load from this repository; nothing to host.

## 1. Badges

1. Settings > Playback > Versions > Badges > Edit.
2. Delete every existing badge. Two badges with the same label: the first
   one wins, so old badges would hide the new ones.
3. Open `badges.json`, copy all of it, paste it in Import.
4. Click Import, then Save (white button, bottom right).
5. The Badges row must read `47 badges of your own`. If not, Save was
   skipped: closing with the cross or Cancel discards the import.

## 2. CSS

Required for the image badges. Without it they render small and sit low.

1. Settings > Theme > Custom CSS.
2. Paste `badges.css` at the end of your existing CSS.
3. Click Apply CSS, then Keep within 15 seconds.

The CSS gives text and image badges the same height (1.375rem) and corner
radius (5px), and makes the image fill the frame. Change `5px` to adjust
the radius.

## 3. Quick filters (optional)

1. Settings > Playback > Versions > Quick filters > Edit.
2. Delete existing filters (import appends).
3. Paste `quick-filters.json` in Import, click Import, then Save.

Filters: T1, 4K, HD, SD, HDR, SDR, IMAX, Extended, VF.

## 4. Relaunch

Quit the app completely and open it again so the images load.

## 5. Check

Settings > Playback > Versions > Badges > Edit > Try them. Paste:

    Dune.2021.2160p.UHD.BluRay.REMUX.HDR.DV.HEVC.TrueHD.Atmos.7.1-GRP
    The.French.Revolution.1989.1080p.BluRay.x264-GRP

Expected: HDR+DV and H.265 images on the first, SDR and H.264 images on
the second.

## Badges that need config

Most badges read the file name or the parsed tags and work as is. These
read results from your AIOStreams config:

    T1 T2 T3 LQ    Filters > Stream Expression > Ranked Stream Expressions
                   > Synced URLs, add:
                   https://raw.githubusercontent.com/Vidhin05/Releases-Regex/main/English/expressions.json

    RD TB AD EN    Ranked Stream Expressions, add four, score 0:
                   /* Ready RD */ service(cached(streams), 'realdebrid')
                   /* Ready AD */ service(cached(streams), 'alldebrid')
                   /* Ready TB */ service(cached(streams), 'torbox')
                   /* Ready EN */ service(cached(streams), 'easynews')

Not using a service or the tiers? Delete those badges before importing.

SDR (badge and filter) is detected from the file name: no HDR, DV, DoVi,
HLG or Dolby Vision marker. No formatter text needed.

## Troubleshooting

    Image badges show as text         image URL unreachable; open one in a
                                      browser, it must show the badge
    Old design still shows            app cache; quit and relaunch. When
                                      images change, the ?v=N in the URLs
                                      is bumped: re-import badges.json
    Image badges smaller or lower     badges.css missing or not applied
    Double frame around an image      a custom "border" plus an image that
                                      draws its own frame; use the files
                                      from this repo as they are
    Seam in the corners of the gold   update badges.css (image slides
    block                             under the frame, badge clipped)
    Only 4K, never HD                 the version list is capped (25 on
                                      some instances) and 4K fills it.
                                      Filters > Result Limits > Resolution
                                      = 12, save the config
    Badges row still shows the old    Save was not clicked after Import
    count

## Uninstall

Delete the badges, remove the badge CSS block from Custom CSS, delete the
quick filters.
