# Website Capture (GIF / WebP)

Capture a webpage as an animated **GIF** or **WebP** for READMEs and docs (`PabloLec/website-to-gif`).

## What it can do
- Scroll down a webpage and record frames into a GIF or WebP
- Capture static (non-scrolling) animations (`no_scoll: true`)
- Resize output (`final_width`, `final_height`) and control frame timing (`time_per_frame`, `scroll_step`)

## Key Inputs
- `url` *(required)* — webpage URL to capture
- `save_path` (default: `/`) — must already exist in repo
- `file_format` (default: `GIF`, or `WebP`)
- `file_name` (default: `demo`, without extension)
- `window_width` (`1920`), `window_height` (`1080`)
- `final_width` (`640`), `final_height` (`360`)
- `scroll_step` (`25`), `time_per_frame` (`100`), `start_y` (`0`), `stop_y`, `start_delay` (`0`)
- `no_scoll` (`false`), `time_between_frames` (`100`), `number_of_frames` (`20`)

## Example

```yaml
name: Generate demo file
on: push

jobs:
  generate-gif:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4

      - name: Website to GIF
        uses: PabloLec/website-to-gif@2.1.5
        with:
          url: "https://docs.github.com/en/get-started"
          save_path: "/docs/images/"
          file_name: "demo"
          file_format: "GIF"

      - name: Commit file
        run: |
          git config --global user.name "github-actions[bot]"
          git config --global user.email "41898282+github-actions[bot]@users.noreply.github.com"
          git add .
          git commit -m "Update demo gif"
          git push
```
