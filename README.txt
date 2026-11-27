LMU Telemetry=================================

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

Where LMU keeps telemetry
  ...\steamapps\common\Le Mans Ultimate\UserData\Telemetry\*.duckdb
