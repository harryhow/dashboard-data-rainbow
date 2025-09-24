# Data Rainbow — Dashboard

Jupyter dashboard for exploring the Data Rainbow media dataset on a map. Supported media including audio, video and images, with filtering by type, device, location, date, and media file availability.

## File structure
```
.
├── dashboard.ipynb      # Run this notebook to launch the dashboard
├── environment.yml      # Conda env spec (Python + ipyleaflet/leafmap + widgets)
├── location.csv         # Locations metadata
├── media.csv            # Media metadata 
├── README.md
└── sample.zip           # (NOT checked in) zip of media files
```

⚠️ `sample.zip` is referenced but intentionally not committed (due to gitgub's large file limitation). 
Put it next to the notebook locally; on first run it will auto-unzip into a `data/` folder. 

## Quick start
(TBD)