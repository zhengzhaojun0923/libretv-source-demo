# libretv-source-demo

A minimal, legally clean Apple CMS (MacCMS) style VOD source, used to test [LibreTV](https://github.com/LibreSpark/LibreTV) end to end.

## Use

In LibreTV: Settings -> Source Management -> VOD Sources -> "+ Add API", fill in:

```
https://raw.githubusercontent.com/zhengzhaojun0923/libretv-source-demo/main/vod.json
```

Or preset it for all users with the `DEFAULT_SOURCES` environment variable.

## Content and license

- `Big Buck Bunny` (c) Blender Foundation, CC-BY 3.0 - https://peach.blender.org/
- `Tears of Steel` (c) Blender Foundation, CC-BY 3.0 - https://tearsofsteel.org/
- HLS streams are public demo endpoints from Mux test-streams and Unified Streaming.

This repository contains no commercial or unauthorised film/TV content. It serves one static JSON file purely to verify the source -> search -> detail -> playback chain.

## Why only one title

GitHub raw ignores query parameters. LibreTV filters the returned list by title on the server side (`filterRelevantResults` in `src/lib/cms-parser.ts`), so keyword search still behaves normally.

But the detail request `?ac=videolist&ids=N` returns the same full list, and `parseDetail` always reads `list[0]`. With multiple titles every title would play the first title's episodes. Hence this demo deliberately contains exactly one title. For a real multi-title source, run a dynamic Apple CMS backend (e.g. `magicblack/maccms10`) on a public host.
