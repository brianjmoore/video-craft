# Video Craft

A Minecraft-style world made from a stretch of video. Each frame becomes one
layer of blocks, stacked through time, so digging down rewinds the video.
Preview the world from outside, cut it open at any frame, pick a spawn point,
then walk around and dig for hidden caves.

Everything is in `index.html`: plain WebGL2, no libraries, no build step. The
pixel font (Tiny5) loads from Google Fonts and falls back to a monospace font
offline.

## Run

Serve the folder and open it in a browser:

```sh
python3 -m http.server 8000 --bind 0.0.0.0
```

Open `http://localhost:8000/`. A demo world loads on start.

## Menus

The title screen looks out over the current world, slowly turning.

- **Singleplayer** lists your worlds (a demo world is generated on start).
  Each world keeps its blocks, digging, hotbar, album and caves for as long as
  the page is open.
- **Create World from Video…**: name the world, choose a video file, scrub it
  and tap **Start Here** / **End Here**, then set **Layers** (frames) and
  **Width** (blocks across). The size starts at the largest this device can
  hold, and the button says what's missing if it can't be pressed yet.
- **Customize World** comes next (also **Edit World** in the list). The world
  is shown from outside and rebuilds from the captured frames as you change
  settings, without seeking the video again. Drag to orbit, scroll or pinch to
  zoom, tap the world to set your spawn.
  - **Rock** picks which pixels become solid: **Bright**, **Dark**, **Still**
    (the unchanging background; anything that moves digs a tunnel), **Moving**
    (only motion is solid), **Colorful** (saturated pixels), or **Color**: tap
    the frame picture to make the colour under your finger the rock.
  - **Rock Fill**: roughly what share of the world is solid.
  - **Smoothing** blurs across space and time first, for fewer, rounder caves.
  - **Time Runs**: **Upward** stacks frames as layers (first frame at the
    bottom). **Forward** stands each frame up as a wall, so you walk through time.
  - **Time Stretch** gives each frame 1–3 layers, so things that flash by for a
    single frame still leave tunnels tall enough to walk through.
  - **Cut at Frame** hides every later frame so you can look inside.
  - **Hidden Caves** turns the cave hunt on or off; **X-Ray Caves** shows them.
- **Options…** sets FOV, mouse/touch sensitivity, sound and view bobbing
  (saved in the browser).

## Play

The goal is to unearth the video. Blocks you walk next to, dig or blast count
as uncovered, and the map in the corner fills in with the real pixels of the
frame you're standing in. Uncover enough of a frame (200 blocks per layer) and
it's unearthed: you get an advancement and it goes into your **Frame Album**,
which shows every frame as far as you've uncovered it and can play back the
ones you've unearthed. The XP bar is your progress on the current frame and the
green number counts frames unearthed. Digging down goes back in time.

Hold to mine: cracks spread until the block breaks and it goes into your hotbar.
Similar colours stack up to 64, and placing uses them up. The last slot holds
unlimited **TNT**: place it and it lights itself, then blows out a crater after
two seconds, setting off any TNT nearby and knocking you back.

With **Hidden Caves** on, sealed air pockets are hidden in the rock; walking into
one earns an advancement, and cave sense above the hotbar points to the nearest.

Desktop: **WASD** move, **Space** jump, **Shift** sprint, hold **left click**
to mine, **right click** to place, **1–9** or the scroll wheel to pick a slot,
**E** for the Frame Album, **F** to fly, **L** for the headlamp, **F3** for the
debug screen, **Esc** for the Game Menu.

Touch: drag on the left side to move and on the right side to look. Hold still
on the right side to mine, tap to place, tap the hotbar to pick a slot.
**Album** opens the Frame Album and **II** the Game Menu. On phones the game
goes fullscreen where the browser allows it and keeps the screen awake.

You step up one-block ledges automatically. The bottom layer is unbreakable
bedrock.
