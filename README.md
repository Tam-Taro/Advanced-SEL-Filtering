# SEL-Filtering-and-Sorting
Since beta of the current v2 AIOStreams, I always wanted the perfect config that would show only the best results, not just for myself, but for my family and friends too. Some prefer lower quality/resolution streams for their lower end TV, while I prefer the latest remuxes. An all-in-one config that I could share. We didn't want to see dozens of results we would never use anyway. This balancing act was finally possible with the release of [Stream Expressions Language (SEL)](https://github.com/Viren070/AIOStreams/wiki/Stream-Expression-Language) capability in AIOStreams.  

After months of tinkering, always finetuning my setup, testing newest features and bugs, and exchanging numerous tips with you all over at the AIOStream discord, I will use this space to share some of that with you. You will find a guide to my personal config that I'm happy with and importable templates for AIOStreams, with a heavy focus on SEL as the filtering tool. It is tailored to my preference, but has broadened over time so that most of you should find it as a good starting point, if not the final piece to your stremio puzzle.

Consider using my setup template as is if you:
- Don't want to see too many results, but also don't want to miss out on any high quality streams that may be removed by simple filtering like `Exclude Uncached` or `Result Limits`
- Want a config that will adjust its filtering strictness based on how many results are found. Dont want those old 480p cartoons filtered out? But don't want to see 720p streams when there are a bunch of 1080p & 4K present already? This setup got you covered. 
- Prioritize certain streams and have sorted your results accordingly in `Filters` and `Sort Order` (Cached & Uncached), optionally with [Vidhin's regex patterns](https://github.com/Vidhin05/Releases-Regex/blob/main/README.md)

Lastly, you can find my config for AIOMetadata at the end for all your metadata and catalog  management needs.

---

## ⚙️ What’s Included for AIOStreams

These are setup templates to use with AIOStreams. If you're not sure which AIOStreams instance to start with, check out the list of trusted public instances [here](https://status.dinsden.top/status/stremio-addons).

| Template | Description |
|-----------|--------------|
| **Complete Setup** | Complete configuration with filters, sort orders, streaming addons, and formatter. |
| **Without Addons** | Keeps your existing add-ons while applying the complete setup config. |
| **Without Addons & Formatter** | Applies the complete set up but keeps both your add-ons and formatter untouched. |
| **Complete Setup for P2P** | Complete setup, with p2p/http addons and sort order tailored for those without debrid service |
| **SEL Only** | Imports only the Excluded Stream Expressions (smart filters). | 
| **Formatter Only** | Imports only the custom formatter used in the template for stream display. |

---

## 📥 How to Import

1. **AIOStreams → Save & Install 💾 → Import** 
2. Click **Import Template**
3. Copy & Paste the URL to "Tamtaro-All-Templates-for-AIOStreams"
```text
https://raw.githubusercontent.com/Tam-Taro/SEL-Filtering-and-Sorting/refs/heads/main/Tamtaro-All-Templates-for-AIOStreams.json
```
4. "Confirm Import" to import all templates available from me.  This will save them into your browser cache for future use. If you already imported previously, this will refresh them to the latest version. 
5. Select one of the templates as you wish to use. I recommend to start with "Complete SEL Setup" as it has the most of my configs shared here.
6. Follow the prompt to configure your debrid credentials (optional if you chose the P2P template). API Keys already configured inside AIOStreams will be prefilled.
7. Enter your TMDB/TVDB credentials for Title Matching and various other features. Use `t0-free-rpdb` for RPDB key.
8. Load Template, Save your AIOStreams and enjoy!

  > [!NOTE]
  > Remember to personalize your imported config by going to `Filters` -> `Language`. Select all the languages you may be watching on Stremio as `Required Languages`. Then copy those same ones into `Preferred Languages`, then sort/rank at the bottom according to your preference. **Keep `Dubbed, Dual Audio, Multi, Unknown` in these two lists** as they may contain streams of your preferred languages. You should also select your subtitle languages in SubHero addon - by default only English is selected.
> To further enhance your sorting and filtering, I highly recommend importing Vidhin's regex which tags streams based on the quality of the release group. Scroll down for more information.

## 🧩 Recommended Setup
This is my recommended setup that should work for most of you. If you just want a finished template, then import & use one of the templates described above. Otherwise read on to customize your current AIOStreams instance.

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

## 🎚️ Filtering
- Define `Preferrence Order` in each of `Resolution, Quality, Encode, Stream Type, Visual Tag, Audio Tag` and `Language`. 
  - This is important for our Sort Order to work.
> [!NOTE]
> You will have to edit this section to your personal preference.
  - Under `Language` -> `Required Language`, select all your required languages there. This is ensure streams of the language you watch will be included in the results.
  - Set `Preferred Languages` to be the same as your `Required Languages`, reorder/rank them to your preferrence. 
  - By default my setup has the following languages: `English, Japanese, Korean, Dubbed, Dual Audio, Multi, Unknown`. Regardless of your choice, do not remove `Dubbed, Dual Audio, Multi, Unknown` from either lists, as some streams of your language may fall under these language tags.

- Default is recommended in the rest of the filters. If not sure, check my AIOStreams template json for how I configured them 
  - `Quality`: Remove default items in `Excluded` since my SEL will remove CAM/TS/etc when necessary
  - `Visual Tag`:  If your device doesn't support DV add `DV Only` into `Excluded`. Same for 3D. 
  -   `Encode`: `Exclude H-OU, H-SBS` for non 3DTV
 - Optional: Import [Vidhin's json for merged anime regexes](https://github.com/Vidhin05/Releases-Regex/blob/main/README.md) into `Regex → Preferred Regex Patterns → Import from url icon` 
 ```text
https://raw.githubusercontent.com/Vidhin05/Releases-Regex/main/merged-anime-regexes.json
```
   - This regex labels all streams with tier rankings based on reputation/quality of release groups per [TRaSH Guides](https://trash-guides.info/). You will need to reimport the regex occassionally whenever Vidhin pushes an update to the regex because many AIOStreams instances will only allow the use of his latest update regex. 
 - Optional: Under `Matching`, enable `Season/Episode Matching` and `Title Matching`  with `Match Year (1 Year Tolerance)` and `Exact Matching Mode` selected. I suggest boosting the `Similarity Threshold` from `0.85 to 1`. Adjust these settings as needed.
 - Under `Deduplicator`, select all 3 `Detection Methods`. Set to `Aggressive` for `Multi-Group Behaviour`. Leave everything else as default (Single Result). 

> [!IMPORTANT]
> Leave all remainder filters setting, `Excluded` `Included` and `Required` boxes empty. As tempting as it sounds to select `Exclude Uncached` or set your `Result Limits`, my SEL will do that for you. This is the first troubleshooting step if your sort/filter looks off!

## 🎚️🤖 Filtering with Stream Expression Language (SEL)

- All filtering (besides title match and dedupe) can be done with stream expressions. My setup leaves the language filtering to AIOStreams basic language filter (altho can be done using SEL - just think the basic filter is good enough).
- There are two schools of thought with regards to SEL Filtering:
  - using it to filter during fetching stage via `Dynamic Group Exit Condition` or,
  - using it after all initial filtering has been done by AIOStreams via  `Excluded Stream Expressions` (ESE) 
- My setup has been fine-tuned using the second method for over 3 months now with feedback from users. I may incorporate the first method into my setup in the future, however for now heavy work of filtering is done using my three lines of ESE. Copy-paste the codes below into `AIOStreams -> Excluded Stream Expressions` or import them using the SEL-only template json at the top of this page.
  <p>
    <details>
        <summary>First line into ESE: Core Filters & Low-res fallback</summary>
  
    ```text
  /*Uncached low-seeder filter (except usenet or good regex-matched uncached)*/
  count(type(streams,'debrid','usenet')) > 0? 
  ( count(type(cached(streams),'debrid','usenet')) < 10 ? [] :  merge(count(regexMatched(streams)) > 0 ? seeders(merge(regexMatched(negate(uncached(type(streams,'usenet')), uncached(streams)),'','Bad'), type(streams,'p2p')),0,10) : seeders(merge(negate(uncached(type(streams,'usenet')), uncached(streams)), type(streams,'p2p')),0,10),
  /*Uncached resolution filter*/
  count(resolution(cached(streams),'2160p','1440p')) > 10 ? resolution(uncached(streams),'720p','576p','480p','360p','240p','144p','Unknown') :  
  count(resolution(cached(streams),'2160p','1440p','1080p')) > 10 ? slice(resolution(uncached(streams),'720p','576p','480p','360p','240p','144p','Unknown'), 5) : 
  count(resolution(cached(streams),'2160p','1440p','1080p','720p')) > 10 ? slice(resolution(uncached(streams),'576p','480p','360p','240p','144p','Unknown'), 5) : [] ) ): 
  /*P2P low-seeder filter*/	
  count(type(streams,'p2p')) < 10 ? [] : 
  count(seeders(type(streams,'p2p'), 50)) > 20? seeders(type(streams,'p2p'), 0,50) : count(seeders(type(streams,'p2p'),25)) > 20? seeders(type(streams,'p2p'), 0,25) : count(seeders(type(streams,'p2p'), 10)) > 10? seeders(type(streams,'p2p'),0,10) : count(seeders(type(streams,'p2p'), 1)) > 10? seeders(type(streams,'p2p'), 0,1) : []
     ```   
    </details>
  </p>
  <p>
    <details>
        <summary>Second line into ESE: Trimming high quality streams (Bluray REMUX, Bluray, WEB-DL)</summary>
  
    ```text
  /*High quality & resolution filter*/
  merge(count(resolution(quality(streams,'Bluray REMUX'),'2160p')) > 3 ? slice(resolution(quality(streams,'Bluray REMUX'),'2160p','Unknown'), 3) : [], 
  count(resolution(quality(streams,'Bluray REMUX'),'1440p','1080p')) > 3 ? slice(resolution(quality(streams,'Bluray REMUX'),'1440p','1080p','Unknown'), 3) : [], 
  count(resolution(quality(streams,'Bluray REMUX'),'720p')) > 3 ? slice(resolution(quality(streams,'Bluray REMUX'),'720p','Unknown'), 3) : [], 
  count(resolution(quality(streams,'Bluray'),'2160p')) > 3 ? slice(resolution(quality(streams,'Bluray'),'2160p','Unknown'), 3) : [], 
  count(resolution(quality(streams,'Bluray'),'1440p','1080p')) > 3 ? slice(resolution(quality(streams,'Bluray'),'1440p','1080p','Unknown'), 3) : [], 
  count(resolution(quality(streams,'Bluray'),'720p')) > 3 ? slice(resolution(quality(streams,'Bluray'),'720p','Unknown'), 3) : [], 
  count(resolution(quality(streams,'WEB-DL'),'2160p')) > 3 ? slice(resolution(quality(streams,'WEB-DL'),'2160p','Unknown'), 3) : [], 
  count(resolution(quality(streams,'WEB-DL'),'1440p','1080p')) > 3 ? slice(resolution(quality(streams,'WEB-DL'),'1440p','1080p'), 3) : [], 
  count(resolution(quality(streams,'WEB-DL'),'720p')) > 3 ? slice(resolution(quality(streams,'WEB-DL'),'720p','Unknown'), 3) : [],
  count(resolution(quality(streams,'WEBRip'),'2160p')) > 3 ? slice(resolution(quality(streams,'WEBRip'),'2160p','Unknown'), 3) : [], 
  count(resolution(quality(streams,'WEBRip'),'1440p','1080p')) > 3 ? slice(resolution(quality(streams,'WEBRip'),'1440p','1080p','Unknown'), 3) : [], 
  count(resolution(quality(streams,'WEBRip'),'720p')) > 3 ?  slice(resolution(quality(streams,'WEBRip'),'720p','Unknown'), 3) : [], 
  count(resolution(quality(streams,'HDRip','HC HD-Rip','DVDRip','HDTV'),'1080p')) > 3 ? slice(resolution(quality(streams,'HDRip','HC HD-Rip','DVDRip','HDTV'),'1080p','Unknown'), 3) : [], 
  count(resolution(quality(streams,'HDRip','HC HD-Rip','DVDRip','HDTV'),'720p')) > 3 ? slice(resolution(quality(streams,'HDRip','HC HD-Rip','DVDRip','HDTV'),'720p','Unknown'), 3) : [], 
  count(resolution(quality(streams,'Unknown'),'2160p')) > 3 ? slice(resolution(quality(streams,'Unknown'),'2160p','Unknown'), 3) : [], 
  count(resolution(quality(streams,'Unknown'),'1440p','1080p')) > 3 ? slice(resolution(quality(streams,'Unknown'),'1440p','1080p','Unknown'), 3) : [], 
  count(resolution(quality(streams,'Unknown'),'720p')) > 3 ? slice(resolution(quality(streams,'Unknown'),'720p','Unknown'), 3) : [] )

        )
    ```
    </details>
  </p>
  <p>
    <details>
        <summary>Third line into ESE: Trimming low quality streams</summary>
  
    ```text
  /*Low quality, resoution & "Bad" regex filter*/
  merge(count(quality(streams,'Bluray REMUX','Bluray','WEB-DL','WEBRip')) > 10 ? quality(streams,'HDRip','HC HD-Rip','DVDRip','HDTV','CAM','TS','TC','SCR','Unknown'):
  count(quality(streams,'Bluray REMUX','Bluray','WEB-DL','WEBRip','HDRip','HC HD-Rip','DVDRip','HDTV')) > 10 ? quality(streams,'CAM','TS','TC','SCR','Unknown') : [], 
  count(resolution(streams,'2160p','1440p','1080p')) > 9 ? resolution(streams,'720p','576p','480p','360p','240p','144p','Unknown'):
  count(resolution(streams,'2160p','1440p','1080p')) > 4 ? slice(resolution(streams,'720p','576p','480p','360p','240p','144p','Unknown'),5):  
  count(resolution(streams,'2160p','1440p','1080p','720p')) > 9 ? resolution(streams,'576p','480p','360p','240p','144p','Unknown') : 
  count(resolution(streams,'2160p','1440p','1080p','720p')) > 4 ? slice(resolution(streams,'720p','576p','480p','360p','240p','144p','Unknown'),5) : [],
  count(negate(regexMatched(streams,'Bad'), regexMatched(streams))) > 4 ? regexMatched(streams,'Bad') : [] )

    ```
    </details>
  </p>

---

## ⚙️ What’s Included for AIOMetadata
These are setup configs to use with AIOMetadata. It is a powerful tool for all things metadata and catalogs. If you're not sure where to start, pick a AIOMetadata instance from [the list of trusted public instances](https://status.dinsden.top/status/stremio-addons) or use the [Elfhosted instance](https://aiometadata.elfhosted.com/configure/). You can't go wrong with either choice.

| Complete config | Description |Download|
|-----------|--------------|---|
| **With Anime Catalogs** | Complete configuration with anime metadata preset, tv, movies and anime catalogs. Huge props to Cedya, Snoak & Mr Professor for their awesome lists!|[Direct Link](https://raw.githubusercontent.com/Tam-Taro/SEL-Filtering-and-Sorting/refs/heads/main/AIOMetadata%20Configs/AIOMetadata-config-with-anime.json)|
| **Without Anime Catalogs** | Complete configuration for tv and movies catalogs. No anime. |[Direct Link](https://raw.githubusercontent.com/Tam-Taro/SEL-Filtering-and-Sorting/refs/heads/main/AIOMetadata%20Configs/AIOMetadata-config-without-anime.json)|

## 📥 How to Import
AIOMetadata setup configuration [For Meta/Catalogs]

- Pick one of these two json files to import into AIOMetadata following the instructions below:

   1. Integrations tab -> Obtain and enter your TMDB, TVDB, and MDBLists APIs . Use `t0-free-rpdb` for RPDB. Fanart.tv API Key is optional. Hit the `Test All Keys` button to ensure they're all ️:white_check_mark:.
   2. Configuration tab -> Import Configuration -> Import one of my json files. Feel free to edit/hide/delete various catalogs in Catalogs tab to your liking.
   3. Configuration tab -> Save Configuration -> Enter a password to save your configuration (if you haven't made an account before) -> Install the addon directly into Stremio. Note: if you encounter `AddonsPushedToAPI - Max descriptor size reached` error, try step
   4. Copy your `Install URL`. Go to [Stremthru Side Kick](https://stremthru.13377001.xyz/stremio/sidekick/), log in there using your stremio account and use the Install button there to install the addon with the AIOMetadata URL. This *may help to* bypass the `AddonsPushedToAPI - Max descriptor size reached` error, otherwise disable some catalogs to reduce size. 
- For best compatibility with AIOMetadata, go to https://cinebye.dinsden.top, load up your account and remove all three Cinemeta features (Search, Catalogs, and Meta). Then scroll down to the bottom of cinebye and re-order your addons so that AIOMetadata is top spot.  Finally, save the changes by clicking `Sync to Stremio`.
- You can change your default Display Language inside AIOMetadata under General tab. Note that if you notice tv series not displaying any episode information in your language, try to upload the episodes overview for your show via tvdb directly. Alternatively you can switch the TV Series metadata provider to TMDB as it may have the missing information in your language.
