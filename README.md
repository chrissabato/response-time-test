# Reaction Time Test

A single-page website that measures how fast you react to a visual and/or audio cue.

- **5 trials per session**, then session stats (mean / median / best / worst / total) with a per-trial breakdown.
- Times are shown in **seconds to three decimals**, e.g. `0.283 s`. The Total stat sums all five trials.
- **Cue modes**, chosen before each run: Visual, Audio, Both at once, Random mix (each trial independently visual / audio / both), or Referee view.
- **Referee view:** a clip stays frozen on its first frame; tap the instant it starts to move. It stays on screen through the trial, plays out, and resets to frame one before the next trial.
- **Input:** click or tap anywhere on the stage.
- Random 2–6 s wait before each cue. Tapping early is flagged as a false start and the trial restarts (not counted).
- No build step, no dependencies, no data stored between visits. Just `index.html`, `whistle.mp3` (the audio cue; a synth tone plays if it can't be loaded), and `StopTheClock.mp4` (the video cue).

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
- Video timing starts on the first painted frame of playback (`requestVideoFrameCallback`,
  falling back to the `playing` event), so it carries the same one-frame latency.
- The whistle is decoded into memory on *Start test* and any leading silence in
  the file is skipped, so playback starts on the first audible sample.
- Audio timing does not compensate for the device's audio output latency, so
  audio-only scores tend to run slightly high compared with visual.
- Results reflect your hardware (display refresh rate, input latency) as much as you.
