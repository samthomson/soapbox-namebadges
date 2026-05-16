# Soapbox Namebadges

Generate printable `.3mf` conference badges for Bambu Studio + AMS.

![Sample badge](docs/images/badge-sample.png)

## Quick Start

```bash
pip install -r requirements.txt
python generate_badge.py --members-file team_members.json --member "Sam"
```

Output is written to `output/namebadges/`.

## Batch Generate

```bash
python generate_badge.py --members-file team_members.json --only-oslo
```

## Files

- `generate_badge.py` - main badge generator
- `generate_3d_qr.py` - QR mesh utilities used by badge generator
- `team_members.json` - input data for batch generation
