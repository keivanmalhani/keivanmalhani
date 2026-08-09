# Hi, I'm Keivan

I build local-first tools for photographers and filmmakers. 24 of them are here, they all run
entirely on your own machine, and none of them ask for an account.

The through-line: **taking a shoot from memory card to finished post without a subscription and
without uploading a client's work to somebody else's cloud.** Along the way that turned into an
agent safety story, a deployment story, and a few workshop tools built the same way.

```text
PHOTO
  shutter-roll ....... scanned film gets its real stock, camera and shoot date back
  shutter-cull ....... burst clustering, blur and eye scoring, keepers picked
       |
       v
  Lightroom Classic reads the XMP sidecars natively

AGENTS
  shutter-mcp ........ the same library, read-only, exposed to AI agents
  shutter-cull-mcp ... the write side: agents propose, humans confirm, undo always

VIDEO
  shutter-select ..... local transcription, take detection, audio and image scoring
  shutter-clip ....... social re-rank, cut, phone-ready posts
       |
       +--> selects timeline, opens in Resolve or Premiere
       +--> analysis JSON, a versioned contract computed once

ON A SCHEDULE
  shutter-farm ....... the whole archive, nightly, in a container. Never twice.

WORKSHOP
  printcheck ......... drop an STL, see if it will print. Nothing uploads.
  spool .............. filament inventory and the true cost of a print, failures included
  gearwatch .......... is this used lens actually a deal, measured against its own sold history
  shutter-warehouse .. the other tools&#x27; output, aggregated three ways in Spark

BROWSER
  motion-recipes ..... fourteen micro-interactions with no animation library underneath
  portfolio-site ..... the site you are looking at, tested without a GPU
  d2-auth ............ The sign-in step for the Destiny tools. It is one page that nobody vis
  dps-maximizer ...... Sign in with Bungie, pick your class and what you are doing - a generi
  exif-atlas ......... is a sample report, so you can see what this produces without installi
  fireteam-report .... Compare a Destiny 2 fireteam&#x27;s raid and dungeon clears and get a ranke
  gcode-lint ......... Static analysis for sliced 3D printer gcode. It reads the file once an
  goldenhour ......... A command line tool that tells a photographer when and where the light
  guardian-timeline .. Raid Report shows your clears. Destiny Tracker shows your kill to deat
  lutbox ............. Drop a photo and a `.cube` LUT onto the page. The grade is applied at 
  mcp-probe .......... Audit an MCP server before you connect an agent to it.
  timecode ........... SMPTE timecode arithmetic for video editors, with drop frame handled t
  weapon-report ...... light.gg tells you what is good. DIM tells you what you own. This tell
```

## The tools

| Project | What it does | Stack | Suite |
| --- | --- | --- | --- |
| [shutter-roll](https://github.com/keivanmalhani/shutter-roll) | Scanned film comes home with no film stock, no camera, no ISO, and the scan date sitting w | Python, exiftool, EXIF / XMP | 31 tests |
| [shutter-cull](https://github.com/keivanmalhani/shutter-cull) | Point it at a shoot folder. It groups burst frames, scores every frame for blur, eye-openn | Python, OpenCV, ONNX Runtime | 127 tests |
| [shutter-mcp](https://github.com/keivanmalhani/shutter-mcp) | An MCP server that lets Claude and other agents inspect a photo library conversationally:  | Python, MCP SDK, FastMCP | 21 tests |
| [shutter-cull-mcp](https://github.com/keivanmalhani/shutter-cull-mcp) | The write side of the agent story. An agent cannot call a write tool here: it has to produ | Python, MCP, agent safety | 51 tests |
| [shutter-select](https://github.com/keivanmalhani/shutter-select) | Culls raw footage. Transcribes every word locally with Whisper, finds takes by listening r | Python, faster-whisper, PySceneDetect | 97 tests |
| [shutter-clip](https://github.com/keivanmalhani/shutter-clip) | Zero-edit path from a footage drive to posted clips: motion-ranked picks with readable nam | Python stdlib, ffmpeg, HEVC / VideoToolbox | 53 tests |
| [shutter-farm](https://github.com/keivanmalhani/shutter-farm) | Point a container at a media volume and the whole archive gets culled on a schedule, witho | Python stdlib, Docker, Kubernetes | 92 tests |
| [printcheck](https://keivanmalhani.github.io/printcheck/) | Drag an STL onto the page. Overhang faces glow red, thin walls amber, open edges cyan, and | TypeScript, Three.js, Vite | 28 tests |
| [spool](https://github.com/keivanmalhani/spool) | What a 3D print actually costs, which is never just the filament: the failed prints that b | Python stdlib, Klipper / Moonraker, OctoPrint | 370 tests |
| [gearwatch](https://github.com/keivanmalhani/gearwatch) | Used camera gear pricing from the official eBay APIs, never a scraper. It builds a sold-pr | Python stdlib, OAuth2, eBay Browse API | 220 tests |
| [shutter-warehouse](https://github.com/keivanmalhani/shutter-warehouse) | Batch analytics over the data the other shutter-* tools produce. A PySpark DataFrame ETL,  | Python, PySpark, Spark SQL | 17 tests |
| [motion-recipes](https://keivanmalhani.github.io/motion-recipes/) | Fourteen production-ready micro-interactions on the Web Animations API, each with a live d | TypeScript, Web Animations API, Vite | 103 tests |
| [portfolio-site](https://keivanmalhani.github.io/portfolio/) | The public site itself: a bilingual portfolio with a WebGL hero where photographs cross-di | TypeScript, WebGL2, GLSL | 68 tests |
| [d2-auth](https://github.com/keivanmalhani/d2-auth) | The sign-in step for the Destiny tools. It is one page that nobody visits on purpose. | TypeScript | 37 tests |
| [dps-maximizer](https://github.com/keivanmalhani/dps-maximizer) | Sign in with Bungie, pick your class and what you are doing - a generic mode or a specific | TypeScript, @napi-rs/canvas, @types/node | 1173 tests |
| [exif-atlas](https://github.com/keivanmalhani/exif-atlas) | is a sample report, so you can see what this produces without installing it. The library b | Python | 360 tests |
| [fireteam-report](https://github.com/keivanmalhani/fireteam-report) | Compare a Destiny 2 fireteam's raid and dungeon clears and get a ranked list of what to ru | TypeScript, jsdom | 390 tests |
| [gcode-lint](https://github.com/keivanmalhani/gcode-lint) | Static analysis for sliced 3D printer gcode. It reads the file once and tells you what is  | Python | 258 tests |
| [goldenhour](https://github.com/keivanmalhani/goldenhour) | A command line tool that tells a photographer when and where the light will be, at any coo | Python | 217 tests |
| [guardian-timeline](https://github.com/keivanmalhani/guardian-timeline) | Raid Report shows your clears. Destiny Tracker shows your kill to death ratio. light.gg sh | TypeScript | 201 tests |
| [lutbox](https://github.com/keivanmalhani/lutbox) | Drop a photo and a `.cube` LUT onto the page. The grade is applied at full resolution, str | TypeScript | 253 tests |
| [mcp-probe](https://github.com/keivanmalhani/mcp-probe) | Audit an MCP server before you connect an agent to it. | Python | 221 tests |
| [timecode](https://github.com/keivanmalhani/timecode) | SMPTE timecode arithmetic for video editors, with drop frame handled the way SMPTE ST 12-1 | TypeScript | 338 tests |
| [weapon-report](https://github.com/keivanmalhani/weapon-report) | light.gg tells you what is good. DIM tells you what you own. This tells you what you actua | TypeScript, @napi-rs/canvas, @types/node | 306 tests |

**5032 tests across 24 repositories**, and that number is generated rather than written:
`collect.py` builds a clean environment per repo, runs each real suite, and writes the counts to
`verified.json`. The portfolio page and this README are rendered from that file and refuse to print
a count that did not come from a run. It exists because a README once claimed nine tests that were
not there, and that is the cheapest thing in the world for an interviewer to check.

## How I build

- **Local-first is a feature, not a limitation.** Client work should not have to cross a network to
  be useful. Every engine reads from disk, computes on the CPU in front of it, and writes back
  beside the originals.
- **Deployable and private are not opposites.** shutter-farm runs the same engines nightly in a
  container, mounting your volume, on your cluster, with no outbound network.
- **Judgment beats thresholds.** Scores are percentile-ranked within a run, so each shoot is judged
  against itself instead of against a constant that breaks on the next one.
- **Agents propose, humans confirm.** The write-capable MCP server cannot be talked into a write:
  it needs a content-addressed plan token, an exact-phrase confirmation, and a staleness re-check
  at write time. Everything is undoable.
- **Composition over coupling.** Tools call each other's CLIs and read versioned JSON rather than
  importing each other, so the expensive analysis runs once and either side can move.

Every repo is MIT, has CI, and reads in English and Spanish.

Currently looking for customer-facing technical work where the job is turning a hard system into
something a person can actually use.
