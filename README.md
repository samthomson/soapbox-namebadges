# Treasure Codes

Generate multi-color **3MF** models for **Bambu Studio + AMS**:

- **QR plate** — flat plate with raised QR code
- **Container** — bayonet-mount box with QR on the lid
- **Badge** — landscape name badge with QR + profile text

## Setup

```bash
pip install -r requirements.txt
```

Uses **CadQuery** for rounded corners and embossed text.

## One URL — `generate_3d_qr.py`

Writes `output/treasure_qr_<hash>.3mf` unless you pass `-o`.

```bash
python generate_3d_qr.py "https://treasures.to/naddr1qfjunkaaaqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqujunkaaa"
python generate_3d_qr.py "https://treasures.to/naddr1qfjunkbbbqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqujunkbbb" -o ./out/plate.3mf
python generate_3d_qr.py "https://treasures.to/naddr1qfjunkcccqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqujunkccc" -s large --style inlay -o ./out/inlay.3mf
```

**`-s`**: `small` (40mm) · `medium` (50, default) · `large` · `xlarge` · or a number in mm.  
**`--style`**: `raised` (default) · `inlay`.  
More options: `python generate_3d_qr.py --help`.

## Batch — `generate_all.py`

Same generator as above, but **only** via a text file: **one URL per line** (lines starting with `#` are comments). Outputs `qr_01.3mf`, `qr_02.3mf`, … into `output/` unless you pass `-d`.

Same shape as `urls_example.text` in this repo (junk `naddr` placeholders — swap for real links).

```bash
cp urls_example.text urls.txt
# edit urls.txt …
python generate_all.py urls.txt
python generate_all.py urls.txt -d ./out -s medium --style raised
```

`python generate_all.py --help`

## Container with QR lid — `generate_container.py`

Combines a bayonet-mount container template with a QR code on its lid. Two variants: `large` (76mm) and `small` (70mm). QR auto-sizes to fit the lid.

```bash
python generate_container.py "https://treasures.to/naddr1qfjunkaaaqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqujunkaaa"
python generate_container.py "https://treasures.to/naddr1qfjunkbbbqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqujunkbbb" -v small -o ./out/box.3mf
```

**`-v`**: `large` (default) · `small`.  
**`-s`**: override QR size in mm.  
**`-t`**: use a different container template 3MF.  
`python generate_container.py --help`

## Name badges — `generate_badge.py`

Landscape badge with:

- big QR on the left
- name / shape / company / city on the right
- optional right-edge notch accent

Single badge:

```bash
python generate_badge.py "https://ditto.pub/follow/npub1yzfm42rzr3dj2h50flpvdl0uzrv22kv2y4ghve804w5xqu6lzqcqkyfxu5" --name "Sam" --shape "🏔️" --event-line "NOSTR WEEK // OSLO 2026" --company-font "Arial"
```

From team JSON:

```bash
python generate_badge.py --members-file team_members.json --member "Sam"
python generate_badge.py --members-file team_members.json --only-oslo
```

`python generate_badge.py --help`

## Print

Open any `.3mf` in Bambu Studio, map green / white to AMS slots, slice, print.

## Layout

| File | Role |
| ---- | ---- |
| `generate_3d_qr.py` | One URL → QR plate `.3mf` |
| `generate_all.py` | Batch plates from a URL list file |
| `generate_container.py` | One URL → container with QR lid `.3mf` |
| `generate_badge.py` | One/batch people → badge `.3mf` |
| `containers/bayonetbox.3mf` | Container template (bundled) |
| `team_members.json` | Team profile list used for badge batch generation |
| `urls_example.text` | Example URL list; copy to `urls.txt` |

Generated files go in `output/` (gitignored). Keep your real URL list in `urls.txt` (gitignored).

## Tuning

QR plate geometry defaults live in `generate_3d_qr.py`; for width only, use **`-s`**. Container QR auto-sizes to ~75% of the lid diameter by default.
