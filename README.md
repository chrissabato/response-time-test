# Reaction Time Test

A single-page website that measures how fast you react to a visual and/or audio cue.

- **5 trials per session**, then session stats (mean / median / best / worst) with a per-trial breakdown.
- **Cue modes**, chosen before each run: Visual, Audio, Both at once, or Random mix (each trial independently visual / audio / both).
- **Input:** click or tap anywhere on the stage.
- Random 2–6 s wait before each cue. Tapping early is flagged as a false start and the trial restarts (not counted).
- No build step, no dependencies, no data stored between visits. Just `index.html` and `whistle.mp3` (the audio cue; a synth tone plays if it can't be loaded).

## Run locally

Open `index.html` in a browser, or serve the folder:

```sh
python3 -m http.server
# then visit http://localhost:8000
```

## Deploy to GitHub Pages

1. Create a repo and push these files to the default branch:

   ```sh
   git init
   git add .
   git commit -m "Reaction time test"
   git branch -M main
   git remote add origin git@github.com:<you>/<repo>.git
   git push -u origin main
   ```

2. On GitHub: **Settings → Pages → Build and deployment**, set **Source** to
   *Deploy from a branch*, branch `main`, folder `/ (root)`, and save.
3. The site publishes at `https://<you>.github.io/<repo>/` within a minute or two.

## Accuracy notes

- Visual timing starts on the animation frame after the green paint, so it includes
  one frame of display latency (~8–16 ms) — consistent across trials.
- The whistle is decoded into memory on *Start test* and any leading silence in
  the file is skipped, so playback starts on the first audible sample.
- Audio timing does not compensate for the device's audio output latency, so
  audio-only scores tend to run slightly high compared with visual.
- Results reflect your hardware (display refresh rate, input latency) as much as you.
