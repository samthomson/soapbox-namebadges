# Soapbox Namebadges

Generate printable `.3mf` conference badges for Bambu Studio + AMS.

![Sample badge](docs/images/badge-sample.png)

## Quick Start

```bash
pip install -r requirements.txt
python generate_badge_2026_oslo.py --members-file team_members.json --member "Sam"
```

Output is written to `output/namebadges/`.

## Batch Generate

```bash
python generate_badge_2026_oslo.py --members-file team_members.json --only-oslo
```

## Conference Script Pattern

Create one primary script per conference and evolve that script over time.

- Naming convention: `generate_badge_<year>_<conference>.py` so files stay ordered
- Current script: `generate_badge_2026_oslo.py`
- Future conferences: copy that file to a new name, for example `generate_badge_2027_tokyo.py`

## Conference Versions

| Conference | Script | Color 1 (Base) | Color 2 (QR Background) | Color 3 (QR Modules) | Color 4 (Text/Logo) |
| --- | --- | --- | --- | --- | --- |
| Oslo 2026 | `generate_badge_2026_oslo.py` | Green | White | Black | Red |
| _TBD_ | `generate_badge_<year>_<conference>.py` | _TBD_ | _TBD_ | _TBD_ | _TBD_ |

## Files

- `generate_badge_2026_oslo.py` - primary Oslo 2026 badge generator
- `badge_qr_mesh.py` - shared QR mesh utility used by conference generators
- `team_members.json` - input data for batch generation
