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
  dps-maximizer ...... Live: https://keivanmalhani.github.io/dps-maximizer/
  exif-atlas ......... keivanmalhani.github.io/exif-atlas is a sample report, so you can see 
  fireteam-report .... Live: https://keivanmalhani.github.io/fireteam-report/
  gcode-lint ......... Static analysis for sliced 3D printer gcode. It reads the file once an
  goldenhour ......... A command line tool that tells a photographer when and where the light
  guardian-timeline .. keivanmalhani.github.io/guardian-timeline
  lutbox ............. Live at &lt;https://keivanmalhani.github.io/lutbox/>
  mcp-probe .......... Audit an MCP server before you connect an agent to it.
  timecode ........... SMPTE timecode arithmetic for video editors, with drop frame handled t
  weapon-report ...... keivanmalhani.github.io/weapon-report
```

## The tools

| Project | What it does | Stack | Suite |
| --- | --- | --- | --- |
| [shutter-roll](https://github.com/keivanmalhani/shutter-roll) | Put the shooting story back into scanned film. Scans come home with no film stock, no camera, no ISO, and the scan date sitting where the shoot date belongs, so Lightroom files your July roll under October. shutter-roll takes a folder of scans from one roll plus a six-line description and injects the real metadata into every frame, then renders a contact sheet. Local only, backups by default. | Python, exiftool, EXIF / XMP | 31 tests |
| [shutter-cull](https://github.com/keivanmalhani/shutter-cull) | A local-first, non-destructive photo culling engine. Point it at a shoot folder of RAW and JPEG files: it groups burst frames, scores every frame for blur, eye-openness, and aesthetics, picks the keepers, flags the clear rejects, and writes the decisions as XMP sidecar files that Lightroom Classic reads natively. Nothing ever leaves your machine. | Python, OpenCV, ONNX Runtime | 127 tests |
| [shutter-mcp](https://github.com/keivanmalhani/shutter-mcp) | A local, read-only MCP server that lets AI agents inspect and analyze a photo library. Point Claude (or any MCP client) at a folder of RAW and JPEG files and ask it to scan the library, break down cameras and lenses, find duplicates, flag likely-blurry shots, or generate a cull report, all without a single byte leaving your machine. | Python, MCP SDK, FastMCP | 21 tests |
| [shutter-cull-mcp](https://github.com/keivanmalhani/shutter-cull-mcp) | An MCP server that lets an AI agent cull your photo shoot, and cannot run away with it. | Python, MCP, agent safety | 51 tests |
| [shutter-select](https://github.com/keivanmalhani/shutter-select) | A local-first video culling engine. Point it at a folder of raw footage: it transcribes every word spoken, finds the takes, flags dead-quiet and clipped audio, scores sharpness, exposure, and motion, picks the strongest takes and b-roll, and hands your editor a ready-made selects timeline with color markers, plus SRT subtitles of everything said. Nothing ever leaves your machine. | Python, faster-whisper, PySceneDetect | 97 tests |
| [shutter-clip](https://github.com/keivanmalhani/shutter-clip) | Zero-edit social clips straight from a footage drive. Point it at the SSD, get phone-ready files you can AirDrop and post as-is. Nothing is uploaded anywhere and source files are never touched. | Python stdlib, ffmpeg, HEVC / VideoToolbox | 53 tests |
| [shutter-farm](https://github.com/keivanmalhani/shutter-farm) | Point a container at a media volume. It culls the whole archive on a schedule, and never does the same work twice. | Python stdlib, Docker, Kubernetes | 92 tests |
| [printcheck](https://keivanmalhani.github.io/printcheck/) | Try it live - drop an STL, get answers. | TypeScript, Three.js, Vite | 28 tests |
| [spool](https://github.com/keivanmalhani/spool) | Local-first filament inventory and true print cost calculator for 3D printing. | Python stdlib, Klipper / Moonraker, OctoPrint | 370 tests |
| [gearwatch](https://github.com/keivanmalhani/gearwatch) | Used camera gear price tracking from official marketplace APIs. | Python stdlib, OAuth2, eBay Browse API | 220 tests |
| [shutter-warehouse](https://github.com/keivanmalhani/shutter-warehouse) | Batch data engineering over shutter-* photography tool data: PySpark ETL, an RDD MapReduce-paradigm job, and HiveQL-compatible Spark SQL, all running in Spark local mode with a real, CI-tested test suite. No fabricated claims: everything described as "CI-verified" below actually runs in `.github/workflows/ci.yml` on every push. | Python, PySpark, Spark SQL | 17 tests |
| [motion-recipes](https://keivanmalhani.github.io/motion-recipes/) | Most micro-interactions do not need a 70 KB animation library. | TypeScript, Web Animations API, Vite | 103 tests |
| [portfolio-site](https://keivanmalhani.github.io/portfolio/) | A bilingual portfolio site with a WebGL hero. Photographs cross-dissolve through a procedural displacement field, the whole site is one static bundle under 40 KB gzipped, and the interesting parts are unit-tested without a GPU. | TypeScript, WebGL2, GLSL | 68 tests |
| [d2-auth](https://github.com/keivanmalhani/d2-auth) | The sign-in step for the Destiny tools. It is one page that nobody visits on purpose. | TypeScript | 37 tests |
| [dps-maximizer](https://github.com/keivanmalhani/dps-maximizer) | Live: https://keivanmalhani.github.io/dps-maximizer/ | TypeScript, @napi-rs/canvas, @types/node | 1173 tests |
| [exif-atlas](https://github.com/keivanmalhani/exif-atlas) | keivanmalhani.github.io/exif-atlas is a sample report, so you can see what this produces without installing it. The library behind it was generated rather than photographed, and the page says so at the top. | Python | 360 tests |
| [fireteam-report](https://github.com/keivanmalhani/fireteam-report) | Live: https://keivanmalhani.github.io/fireteam-report/ | TypeScript, jsdom | 390 tests |
| [gcode-lint](https://github.com/keivanmalhani/gcode-lint) | Static analysis for sliced 3D printer gcode. It reads the file once and tells you what is going to go wrong before you start a twelve hour print. | Python | 258 tests |
| [goldenhour](https://github.com/keivanmalhani/goldenhour) | A command line tool that tells a photographer when and where the light will be, at any coordinates and on any date, with no network connection and no API key. | Python | 217 tests |
| [guardian-timeline](https://github.com/keivanmalhani/guardian-timeline) | keivanmalhani.github.io/guardian-timeline | TypeScript | 201 tests |
| [lutbox](https://github.com/keivanmalhani/lutbox) | Live at <https://keivanmalhani.github.io/lutbox/> | TypeScript | 253 tests |
| [mcp-probe](https://github.com/keivanmalhani/mcp-probe) | Audit an MCP server before you connect an agent to it. | Python | 221 tests |
| [timecode](https://github.com/keivanmalhani/timecode) | SMPTE timecode arithmetic for video editors, with drop frame handled the way SMPTE ST 12-1 actually defines it. | TypeScript | 338 tests |
| [weapon-report](https://github.com/keivanmalhani/weapon-report) | keivanmalhani.github.io/weapon-report | TypeScript, @napi-rs/canvas, @types/node | 306 tests |

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
