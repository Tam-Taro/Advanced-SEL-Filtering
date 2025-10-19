# SEL-Filtering-and-Sorting
Since the rewrite of AIOStreams v2, I've been an avid tinkerer, always finetuning my setup, testing newest features and bugs, and exchanging numerous tips with you all over at  AIOStream discord. Now I will use this space to share some of those tips for you to use in your own stremio setup. Here you will find my personal setup and templates for AIOStreams, with a heavy focus on SEL as the filtering tool. It is tailored to my preference, but has broadened over time so that most of you should find it as a good starting point, if not the final piece to your stremio puzzle. You can find my config for AIOMetadata too, for metadata and catalog management.

---

## ⚙️ What’s Included

| Template | Description |
|-----------|--------------|
| **Complete Setup** | Complete configuration with filters, sort orders, streaming addons, and formatter. |
| **Without Addons** | Keeps your existing add-ons while applying the complete setup config. |
| **Without Addons & Formatter** | Applies SEL sorting/filtering only. Keeps both your add-ons and formatter. |
| **SEL Only** | Imports only the Excluded Stream Expressions (smart filters). |
| **Formatter Only** | Imports only the custom formatter used in the template for stream display. |

---

## 📦 How to Import

1. **AIOStreams → Save & Install 💾 → Import** 
2. Click **Import Template**
3. Paste the URL of the template you want to import:

```text
https://raw.github.com/Tam-Taro/SEL-Filtering-and-Sorting/main/Complete-setup-template.json
```
```text
https://raw.github.com/Tam-Taro/SEL-Filtering-and-Sorting/main/Setup-without-addons-template.json
```
```text
https://raw.github.com/Tam-Taro/SEL-Filtering-and-Sorting/main/Setup-without-addons-or-formatter-template.json
```
```text
https://raw.github.com/Tam-Taro/SEL-Filtering-and-Sorting/main/Excluded-SEL-only-template.json
```
```text
https://raw.github.com/Tam-Taro/SEL-Filtering-and-Sorting/main/Formatter-only-template.json
```
4. Configure your debrid credentials (optional). If you already configured inside AIOStreams, you can skip.
5. Enter your TMDB credentials for Title Matching feature. TMDB/TVDB APIs are optional.
6. Load Template

> [!NOTE]
> Personalize your imported config by going to `Filters` -> `Language`. Select all the languages you may be watching on Stremio as `Required Languages`. Then copy those same ones into `Preferred Languages`, then sort/rank them according at the bottom according to your preference. Keep `Dubbed, Dual Audio, Multi, Unknown` in these two lists as they may contain the language you want.

## 🧩 Recommended Setup
This is my recommended setup that should work for most of you. If you just want a finished template, then import the aiostreams json linked above. Otherwise read on to customize your current aiostreams instance.

If you're not sure which AIOStreams instance to use, check out [the list of trusted public instances here.](https://status.dinsden.top/status/stremio-addons)

### **Sorting**
- __Global Sort Order Type:__  `Cached`
  - We put `Cached` here since we want our results to show cached before uncached
  - If `Cached` is first item, the sort algorithm automatically goes to Cached & Uncached Sort Order, nothing else after `Cached` matters in Global Sort Order
- Cached Sort Order Type: `Resolution → Library → Quality → Regex Patterns → Stream Type → (if p2p only, Seeders here) → Visual Tag → Audio Tag → Encode → Language → Size → Seeders`
  - There is a lot of flexibility here, re-arrange to your preference as to what your top results should prioritize
  - Note that p2p is considered cached and therefore p2p sorting uses this sort order, so if you're using a p2p setup, move `Seeders` up
- Uncached Sort Order Type: `Resolution → Library → Stream Type → Seeders → Regex Patterns → Quality → Language → Size`
  - Generally the same as `Cached Sort Order` except Seeders is higher 
  - There should be very little to no uncached streams in your results (unless you're using usenet which are mostly uncached), therefore you don't need an exclusive list in this uncached sort order

> [!NOTE]
> If your first filter in `Global Sort Order` is `Cached` and you left `Cached/Uncached Sort Order` blank, your sort/filter may not work properly.

## **Filtering**
- Define `Preferrence Order` in each of `Resolution, Quality, Encode, Stream Type, Visual Tag, Audio Tag` and `Language`. 
  - This is important for our Sort Order to work.
> [!NOTE]
> You will have to edit this section to your personal preference.
  - Under `Language`
  - `Required Language`, select all your required languages there. This is ensure streams of the language you watch will be included in the results.
  - Set `Preferred Languages` to be the same as your `Required Languages`, reorder/rank them to your preferrence. 
  - By default my setup has the following languages: `English, Japanese, Korean, Dubbed, Dual Audio, Multi, Unknown`. Regardless of your choice, do not remove `Dubbed, Dual Audio, Multi, Unknown` from either lists, as some streams of your language may fall under these language tags.

- Default is recommended in the rest of the filters. If not sure, check my AIOStreams json for how I configured them 
  - `Quality`: Remove default items in `Excluded` since my SEL will remove CAM/TS/etc when necessary
  - `Visual Tag`:  If your device doesn't support DV add `DV Only` into `Excluded`. Same for 3D. 
  -   `Encode`: `Exclude H-OU, H-SBS` for non 3DTV
 - Optional: Import [Vidhin's json for merged anime regexes](https://raw.githubusercontent.com/Vidhin05/Releases-Regex/main/merged-anime-regexes.json) into `Regex → Preferred Regex Patterns`  
   - This regex labels all streams with tier rankings based on reputation/quality of release groups per Trash Guide. You will need to reimport the regex occassionally whenever Vidhin pushes an update to the regex because many AIOStreams instances will only allow the use of the latest update. 
 - Optional: Under `Matching`, enable `Season/Episode Matching` and `Title Matching`  with `Match Year (1 Year Tolerance)` and `Exact Matching Mode` selected. I suggest boosting the Similarity Threshold from 0.85 to 1. Adjust these settings as needed.
 - Under `Deduplicator`, select all 3 `Detection Methods`. Set to `Aggressive` for `Multi-Group Behaviour`. Leave everything else as default (Single Result). 

> [!IMPORTANT]
> Key information users need to know to achieve their goal.Leave all remainder filters setting, `Excluded` `Included` and `Required` boxes empty. As tempting as it sounds to select `Exclude Uncached` or set your `Result Limits`, my SEL will do that for you. This is the first troubleshooting step if your sort/filter looks off!
