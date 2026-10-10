# PredictiveHistory_Subtitles — English Subtitle Archive

**Date: 2026-Oct-10**

## 1. Scope

- **Channel processed:** [Predictive History (@PredictiveHistory)](https://www.youtube.com/@PredictiveHistory) — Professor Jiang Xueqin — channel ID `UC11aHtNnc5bEPLI4jf6mnYg`.
- **Date of execution:** 2026-Oct-10 (all metadata and subtitles retrieved on this date).
- **Videos found on the channel:** 181 public videos (channel "Videos" tab; the channel has no Shorts).
- **Already processed in the previous "Collaborations" playlist task:** 19 videos total, of which **1 video** (`N2GFDDZtGQY`, "Global Meet-Up #2 (Los Angeles)") is on this channel and was therefore **skipped**, as instructed. The other 18 belong to other channels and are out of scope here.
- **Videos processed in this task:** **180**.

## 2. Network/retrieval method

This sandbox's IP is blocked by YouTube (yt-dlp fails with "Sign in to confirm you're not a bot"
on every player client; raw watch pages return a bot-check wall). Retrieval therefore ran through
public YouTube-proxy APIs:

- **Channel video list:** Invidious instance `invidious.f5.si`
  (`/api/v1/channels/{id}/videos?sort_by=newest`, paginated with `continuation` tokens; 60 items/page, 4 pages).
- **Playlists & per-video metadata + subtitles:** Piped instance `pipedapi.dedyn.io`
  (`/playlists/{id}`, `/streams/{id}`, subtitle tracks through the instance proxy).
  Fallback host: `piped-api.codespace.cz`.
- Requests were throttled (~1.3 s apart) with retries/exponential backoff; zero failures remained at completion.

## 3. Subtitle priority rules (applied to every video)

1. Manually created (non-auto-generated) English subtitles — preferred.
2. Auto-generated English subtitles — fallback.
3. If neither exists: `Subtitle: [No English subtitles available]`.
4. No machine translation of other languages; subtitles exported as plain text **without timestamps**
   (one subtitle cue per line, verbatim).

**Result:** All 180 videos have English subtitles. **Manual tracks found: 0.** Auto-generated: 180.
**Videos with no English subtitles: none.**

## 4. Description cleaning criteria

This channel's descriptions are largely subject-focused prose. Removed lines/paragraphs:

- "Please Support…" blocks and donation/subscription CTAs
  (buymeacoffee.com links, predictivehistory.substack.com plugs, "Please consider making a small
  donation…", "Please subscribe to the Predictive History Substack…", "Support my work at…",
  "If you'd like to delve deeper/read more … please read Professor Jiang's Substack post…").
- Social-media link blocks ("Authorized social media links:", x.com/xueqinjiang, x.com/Pred_History,
  bare "Twitter:"/"Substack:" labels).
- Channel boilerplate/community announcements that are not subject matter
  (e.g., the standing "refuse to monetize my YouTube channel / fan channels" notice).
- YouTube link wrappers and invisible Unicode (bidi/zero-width) characters.

**Kept verbatim:** all prose about the lecture's subject, guests and context, and the
"Notes and References"/"References and Recommended Readings" lists (including their URLs —
these are scholarly citations, not promotions), plus mention of format context such as
"answers questions from Substack subscribers". No wording was paraphrased or summarized.

## 5. Standardized .txt file format

```
URL: https://www.youtube.com/watch?v={video id}

Title: {exact video title}

Description: {cleaned video description}

Subtitle:
'''
{full subtitle text with original line breaks}
'''
```

## 6. File naming convention

`{video title}_{publish date}_{video id}.txt`

- Title made filesystem-safe: `/ \ : * ? " < > |` replaced by spaces, whitespace collapsed; titles
  longer than ~90 characters truncated at a word boundary.
- Publish date format `YYYYMMMDD` (e.g. `2024Oct22`), taken from each video's YouTube-reported
  `uploadDate` (per-video metadata; cross-checked for chronological consistency across series).
- Full example: `Game Theory #1 The Dating Game_2026Jan06_hE4l9WyLF3U.txt`

## 7. How playlists were handled

The channel has 7 public playlists (fetched from the channel's playlist tab). Every video belonging
to a playlist went into a folder named after the playlist. No video belonged to more than one
playlist. Folder names are exact playlist titles, sanitized for filesystem compatibility:

| # | Playlist (exact title) | Folder name | Files |
|---|------------------------|-------------|-------|
| 1 | Dante Seminar (June 2026, Beijing) | Dante Seminar (June 2026, Beijing) | 12 |
| 2 | Game Theory | Game Theory | 30 |
| 3 | Great Books | Great Books | 13 |
| 4 | Geo-Strategy Update | Geo-Strategy Update | 8 |
| 5 | Secret History | Secret History | 29 |
| 6 | The Story of "Civilization" | The Story of Civilization (quotes removed) | 62 |
| 7 | Geo-Strategy:  Predicting the Future | Geo-Strategy Predicting the Future (colon removed, spaces collapsed) | 12 |

Playlist total: 166 files.

## 8. How non-playlist videos were grouped

14 channel videos belong to no playlist. 13 were grouped thematically by title/series prefix into `Grouped_Non_Playlist/`:

| Group | Logic | Files |
|-------|-------|-------|
| Global_Meet-Ups | Title starts with "Global Meet-Up" (#1 Tokyo, #3 NYC, #4 Austin, #5 Toronto, #6 Montreal) | 5 |
| Emergency_Discussions | Title starts with "Emergency Discussion" (#1–#3) | 3 |
| Livestreams | Livestream/Q&A recordings ("Live with Predictive History #2", "Substack Live #1", "Substack Founding Members Livestream #2", "Predictive History Founding Members #1") | 4 |
| Great_Books | "Great Books #9: Dante (Re-Upload with Audio Fixed)" — part of the Great Books series but not present in the playlist itself | 1 |

(Note: Global Meet-Up #2 was skipped — already processed in the previous task.)

## 9. Uncategorized

1 video fit no playlist and no thematic group:
- `Jiang Xueqin Teaching Gay Talese Research Method (Introduction)_2023Jun21_Gp9Hv1PXx0o.txt` — a standalone teaching recording.

## 10. Errors, anomalies, and special notes

- **No fetch/processing errors** remained at completion; no private/deleted/unavailable videos were encountered.
- YouTube's playlist-tab counters (via Invidious) showed 9 for "Geo-Strategy Update" and 63 for
  "The Story of Civilization", but only 8/62 playable videos were returned — one item in each is
  likely private or deleted; the returned public items were all processed.
- The 11 "Dante Seminar" videos have **no description text at all** on YouTube; their `Description:`
  field is legitimately empty in the output files.
- Invidious's `published` epoch turned out unreliable on the used instance (uniform fallback date),
  so all dates were taken from authoritative per-video `uploadDate` metadata instead.
- All subtitles are YouTube **auto-generated** English (the channel does not provide manual tracks);
  the manual-first rule was applied and found no manual tracks.
- Subtitle bodies are 100% verbatim transcripts (including spoken sponsor-like remarks, since the
  transcript itself is never edited); only the Description field was cleaned.

## 11. Final folder structure

```
PredictiveHistory_Subtitles/
├── README.md
├── Playlists/
├── Dante Seminar (June 2026, Beijing)/  (12 files)
├── Game Theory/  (30 files)
├── Great Books/  (13 files)
├── Geo-Strategy Update/  (8 files)
├── Secret History/  (29 files)
├── The Story of Civilization/  (62 files)
└── Geo-Strategy Predicting the Future/  (12 files)
├── Grouped_Non_Playlist/
├── Global_Meet-Ups/  (5 files)
├── Emergency_Discussions/  (3 files)
├── Livestreams/  (4 files)
└── Great_Books/  (1 files)
└── Uncategorized/  (1 files)
```

**Totals:** 180 `.txt` files (Playlists: 166, Grouped_Non_Playlist: 13, Uncategorized: 1). All files UTF-8.
