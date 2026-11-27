LMU Telemetry - self-hosted copy
=================================

Upload everything in this folder to your web server (any folder, for example
https://yoursite.example/lmu-telemetry/) and open index.html in a browser.

Files
  index.html           the app
  duckdb.mjs           file reader (DuckDB, runs in the browser)
  duckdb-worker.js     file reader worker
  duckdb-eh.gz.wasm    file reader engine (about 8 MB, gzip-packed)
  example-laps.json    example laps shown until you open your own file
  trackmaps/           TinyPedal track maps (.svg) used for real track heights
  trackmaps/index.json the list of maps in that folder
  .htaccess            file types for Apache servers

Adding a track map
  1. In TinyPedal, drive a lap on the track so it saves the map. TinyPedal
     keeps them in its "trackmap" folder, named after the track, e.g.
     Circuit_de_Spa-Francorchamps.svg.
  2. Copy the .svg into the trackmaps/ folder on your server.
  3. Add the file name to trackmaps/index.json, e.g.
        [
         "Circuit_de_la_Sarthe.svg",
         "Your_New_Track.svg"
        ]
     (If your server shows folder listings, the app also finds new .svg files
     without this step, but keeping index.json up to date always works.)
  4. Reload the page. The Help page says how many maps were read.
  The map is matched to a lap by track name and lap length (within 3%).
  Maps in the folder win over the ones built into the app.

Needs
  - A normal web server (http or https). Opening index.html straight from disk
    (file://) only works partly, because browsers block the file reader there.
  - The server must send .mjs as text/javascript.
      Apache: the included .htaccess does this.
      nginx:  add  "text/javascript mjs;"  to the types block in mime.types
              (newer nginx versions already have it).
  - Telemetry files are read in the visitor's browser and never uploaded.
    Laps are not saved: they are gone when the page is closed.
    View settings (light/dark, page, layout, folded charts, ghost, replay
    speed) are kept in one small cookie called "lmu_prefs".
  - Internet access is only used for the Google web fonts. Without it the page
    falls back to system fonts.

Where LMU keeps telemetry
  ...\steamapps\common\Le Mans Ultimate\UserData\Telemetry\*.duckdb
