# Best Sub Bass Notes

**https://chaudepark.github.io/scale-reference/**

A cheatsheet for club-music production: which notes work as a sub-bass root (the E1–G#1 / ~41–52Hz sweet spot), which keys put your sub in that zone, and what to play on top — chords, inversions for a strong sub, pedal notes, modulation targets, kick tuning and 808 slide distances.

This is one half of a two-app pair designed to be used side-by-side in browser split view:

| App | Role |
|---|---|
| **Best Sub Bass Notes** (this repo) | Decide the song's foundation — key, sub note, modulation plan |
| [**Polychord Lab**](https://github.com/chaudepark/polychord-lab) | Refine the colour — extended voicings from stacked triads |

The two apps sync through same-origin `localStorage` (see below), so a key chosen here is picked up live by Polychord Lab in the next tab.

## Features

- Octave-1 keyboard coloured by sub-bass zone (sweet / solid / suboptimal) with fundamental frequencies
- Key reverse-lookup: pick a root + scale (or tap the keyboard) to see usable sub notes, diatonic chords with sub-friendly inversions, pedal (drone) options, and modulation targets ranked by sub strength
- Kick tuning hint (root & 5th, oct1/oct2 Hz) and 808 slide distances for glide basslines
- Ableton Live 12 Root/Scale setting hint
- Chord audition (Web Audio) with an optional **real sub octave** mode (sine at octave 1 — needs monitors/headphones) and a +1 oct layer toggle
- **Sketch loop**: ⇧-click chords to collect up to 8 slots in a bottom bar, loop them at a chosen BPM, and export the progression as a standard MIDI file (drag or download into your DAW). The sketch is shared live with Polychord Lab.
- EN / 日本語, PWA (works offline)

## 日本語

クラブミュージック制作用の早見表です。サブベースのルートとして強く鳴る音（E1–G#1 / 約41–52Hzのスイートスポット）、その音がスイートスポットに入る調、そしてその上に何を乗せるか（コード・サブ向き転回形・ペダル・転調先・キックのチューニング・808スライド距離）をまとめています。

ブラウザのSplit viewで [Polychord Lab](https://github.com/chaudepark/polychord-lab) と並べて使う前提の2アプリ構成です。**こちらで曲の土台（キー）を決め、Polychord Labで響きの色を詰めます。** キー・言語・スケッチループは `localStorage` 経由でリアルタイムに連動します。

コードの⇧クリックで画面下のスケッチループに追加（最大8スロット）。BPM指定でループ再生でき、進行全体を標準MIDIファイルとして書き出してDAW（Ableton等）に持ち込めます。「実オクターブで鳴らす」をONにするとサブが本来のオクターブ1のサイン波で試聴できます（要モニター/ヘッドホン）。

## Development

- Single static file: all data, logic and i18n live in `index.html` (the `SUB_NOTES` / `SCALES` arrays, `STRINGS` for EN/JA). No build step.
- PWA: **bump the `CACHE` version in `sw.js` whenever `index.html` changes**, or returning visitors may get a stale page.
- `localStorage` contract shared with Polychord Lab (same origin):
  - `subbass-key` — `"<rootPc>|<scaleIndex>"`, written on every key change, read live via `storage` events
  - `subbass-lang` — `"en" | "ja"`
  - `subbass-sketch` — JSON `{v, slots:[{label, mids:[midi…]}], bpm}` for the shared sketch loop
