# Video Craft

A Minecraft-style world made from a stretch of video. Each frame becomes one
layer of blocks, stacked through time, so digging down rewinds the video.
Preview the world from outside, cut it open at any frame, pick a spawn point,
then walk around and dig for hidden caves.

Everything is in `index.html`: plain WebGL2, no libraries, no build step.

## Run

Serve the folder and open it in a browser:

```sh
python3 -m http.server 8000 --bind 0.0.0.0
```

Open `http://localhost:8000/`. A demo world loads on start.

## Make a world

1. **Open video**, scrub the preview, and tap **Set start** / **Set end**.
2. Choose **Frames** (layers) and **Width** (blocks across), then tap
   **Build world**.
3. Shape the terrain. These settings rebuild the world from the captured
   frames without seeking the video again:
   - **Rock is**: **Bright** or **Dark** picks which pixels become solid.
     **Still** makes the unchanging background solid, so anything that
     moves digs a tunnel.
   - **Rock fill**: roughly what share of the world is solid, whatever the
     footage looks like.
   - **Smoothing** blurs across space and time before thresholding. Higher
     values give fewer, rounder caves.
   - **Time runs**: **Upward** stacks frames as layers (first frame at the
     bottom). **Forward** stands each frame up as a wall, so you walk through
     time.

## Preview

- Drag to orbit, scroll or pinch to zoom.
- **Cut at frame** hides every later frame. The thumbnail shows the frame at
  the cut.
- **X-ray caves** shows every sealed cave glowing through the rock.
- Click or tap the world to set your spawn (the yellow marker). Cut away time
  first to spawn somewhere inside.

## Play

Desktop: click to capture the mouse. **WASD** to move, **Space** to jump,
**Shift** to sprint, left click to dig, right click to place the last block
you dug, **F** to fly (Space up, Shift down), **L** for the headlamp, **Esc**
for the menu.

Touch: drag on the left side to move. Drag on the right side to look and tap
it to dig, or to place in **Place** mode.

You step up one-block ledges automatically. The bottom layer is unbreakable
bedrock.

The HUD shows the frame you're standing in, with a red dot for your position.

## Caves

A cave is a pocket of air that can't be reached from the sky: something that
appeared and then disappeared within the clip. A dark ball rolling through a
bright scene, for example, becomes a sealed tube of air in Bright mode. Caves
are counted when the world is built.

- **Cave sense** in the HUD says how far the nearest undiscovered cave is and
  which way (warm and cold), and the bar fills as you get closer.
- Walk into a cave to discover it. You'll see its size and the stretch of the
  video it came from.
- Underground is dark, so bring the headlamp.

## Limitations

- Frames are captured by seeking once per frame, so 64 frames take a couple
  of seconds.
- Worlds are capped at 4M blocks (1.5M on touch devices).
- Caves are counted once per build. Digging into one discovers it, but
  pockets you make or seal yourself don't count.
- Edits are lost when you change terrain settings or reload.
- Supported video formats depend on the browser.
