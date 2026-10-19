# neon-rush
Neon Rush: Where the City Fights Back — GAME 220 prototype

A self-contained HTML5 runner prototype for GAME 220. Open index.html in a modern browser, or upload the ZIP to a host that supports browser-playable HTML games.
Game overview: how a run works
Neon Rush: Where the City Fights Back is a fast-paced cyberpunk survival runner. The player automatically races forward along a neon road divided into left, center, and right lanes. The city watches the lane the runner occupies, locks an attack onto that lane, gives a visible warning, and then launches the hazard. The player must react by either changing lanes or staying put and using the correct timed move. The aim is to survive as long as possible, earn points, and learn to read the city's warning signals.
The core loop
1. Read the warning: a glowing magenta marker shows which lane is targeted, and the alert names the recommended action.
2. Choose a response: move to either of the other lanes, or stay in the targeted lane and time the matching action.
3. Resolve the attack: a correct response avoids damage and awards a bonus; a wrong response costs one health pip.
4. Survive and improve: score rises over time, attacks repeat, and the run ends after three hits. Restart to try for a higher score.
The scoring rule: +25 versus +35
Changing lanes earns +25 points. Staying in the targeted lane and successfully countering the attack with the correct move earns +35 points. The higher-value option rewards players who learn the hazard cues and time their moves precisely, rather than always escaping to another lane. The move must be active when the strike reaches the runner.
City attack	Correct counter if you stay in the lane	Alternative safe response	Bonus
Low barrier	Jump (Up / W / Space)	Change lanes	+35 for jump; +25 for lane change
Overhead laser	Slide (Down / S)	Change lanes	+35 for slide; +25 for lane change
Falling debris	Dodge roll (Shift / X)	Change lanes	+35 for roll; +25 for lane change
Road surge	Dodge roll (Shift / X)	Change lanes	+35 for roll; +25 for lane change


For example, if the city marks the center lane with a low-barrier warning, the player can move left or right for +25, or remain in the center and time a jump for +35. If the player stays in the center but slides or rolls instead of jumping, the counter is incorrect and they take damage.
What's playable
- Three-lane movement with lane boundaries and perspective road geometry.
- City Retaliation: the city targets the lane occupied when a warning starts, telegraphs the lane and hazard type, and then attacks after a warning window.
- Four attack types:
  - Low barrier: jump or change lanes.
  - Overhead laser: slide or change lanes.
  - Falling debris: roll or change lanes.
  - Road surge: roll or change lanes.
- Timed jump, slide, and roll actions. Roll has a recharge timer.
- Survival score, dodge/counter bonuses, three health pips, saved best score where browser storage is available, game-over screen, and restart.
- Canvas-drawn low-poly-inspired 2.5D city, neon road, warning shadows/cracks, screen shake, and particles. No external art assets are required.
Controls
Action	Keyboard	On-screen button
Move left / right	Left/Right arrows or A/D	‹ MOVE / MOVE ›
Jump	Up arrow, W, or Space	↑ JUMP
Slide	Down arrow or S	↓ SLIDE
Dodge roll	Shift or X	◉ ROLL
Start / restart	Click the game or press Enter after game over	Click the start/restart button


Core rule: changing away from the marked lane avoids any attack. If you remain in the target lane, use the action named in the warning. The jump/slide/roll needs to be active when the strike reaches the runner, so watch for the attack changing to INBOUND and time the move rather than holding it for the entire warning.
Visual / camera approach
This build is 2.5D, not full 3D. It uses a fixed, behind-the-runner arcade view: the road narrows toward a vanishing point, two perspective lane dividers converge at the horizon, horizontal road marks imply speed, and simple extruded building faces suggest low-poly depth. Geometry is drawn directly on a 2D canvas, keeping the game lightweight and independent of models, textures, or GPU-intensive shaders.
If the project is later migrated to a true 3D engine, use a fixed chase camera looking slightly down the track (roughly 55–65° field of view), simple low-poly building meshes with vertex colors, and three fixed lane center points. Keep the camera and runner stable while the road/obstacles move toward the camera; this keeps hazards easy to read.
Hazard telegraphing rules
1. Capture AttackLane = PlayerLane when a warning begins. The target does not silently follow the player after that.
2. Display a persistent magenta outline around the target lane and a label that names the correct counter-action.
3. Show a growing landing shadow/crack indicator before the hazard arrives.
4. Change the attack label to INBOUND and animate the obstacle moving toward the runner for the final reaction interval.
5. At impact, check lane first, then the matching action. A lane change always works; the matching action is an alternate solution.
6. A successful lane change awards +25; staying in the target lane and timing the correct action (jump/slide/roll for that hazard) awards +35. This rewards precise counter-play. A failed response removes one health pip. Three hits end the run.
The attack types follow a predictable cycle for prototype testing. That is intentional: it lets classmates learn the visual language and give feedback about clarity/fairness before the pattern is randomized or made more adaptive.
Quick test checklist
- [ ] Start screen appears; clicking it begins a run.
- [ ] Left/right controls reach all three lanes and stop at the road edges.
- [ ] Each warning identifies a lane and names the needed action.
- [ ] The hazard visibly enters the target lane after the warning.
- [ ] Switching away from the target lane avoids every hazard.
- [ ] Jump counters the low barrier; slide counters the overhead laser; roll counters debris and road surge.
- [ ] The wrong action in the target lane costs one health pip.
- [ ] Score rises during survival and a successful response adds a bonus.
- [ ] Three hits show the game-over screen; click or Enter restarts the run.
- [ ] Try a laptop keyboard and, where possible, the on-screen buttons on a touch device.
Browser validation performed
The HTML was loaded into a headless Chromium session. The run/start, movement/action inputs, natural game-over lifecycle, and restart were exercised with no JavaScript runtime errors. A targeted test exercised the low, high, debris, and surge counters; health stayed at 3 through the four correct responses. This is a prototype-level test, not a substitute for testing on the classmate devices/browsers you intend to support.
