
# Interactive Dashboard - Mapping the Data

A data dashboard built with Jupyter Notebook for exploring the media dataset on a map.  
Supports **audio, video, and images**, with filtering by type, device, location, date, and media file availability.


Choose a demo:

- {doc}`Static dashboard <static-dashboard>`
- {doc}`Live dashboard (Binder) <dashboard>`

(**How to run**: Click **Lunch Binder** icon below to enable Binder and execute cells in the browser)

[![Launch Binder](https://mybinder.org/badge_logo.svg)](
https://mybinder.org/v2/gh/harryhow/dashboard-data-rainbow/HEAD?labpath=docs/dashboard.ipynb
)

## Quick start
1.	Prepare your media and metadata file
	- Place **sample.zip** alongside **dashboard.ipynb** (or manually extract into designated folder named data/)
	- On the first run the notebook will auto-extract **sample.zip**  into **./data/**.
    - Place **location.csv** and **media.csv** alongside **dashboard.ipynb** too.
2. Launch JupyterLab  
```jupyter lab```
3. Open and run **dashboard.ipynb**

## Environment

We use **conda** with Python 3.11 and the following dependencies:  
  - python=3.11
  - pandas=2.*
  - plotly=5.*
  - folium>=0.15
  - ipykernel
  - jupyterlab
  - ipywidgets>=8
  - ipyleaflet>=0.17
  - leafmap>=0.33
  - ipydatetime>=1.2
  - ipyvuetify>=1.10

Setup the environment by `environment.yml`, then use following command to launch jupyter lab,

```bash
% conda env create -f environment.yml
% conda activate env
% jupyter lab
```

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


> ⚠️ Note: sample.zip is not committed due to size limits.  
Place your media zip file (must be named sample.zip) in the same directory as the notebook.  
On the first run, the dashboard will automatically unzip it into the ./data/ folder.



## Media data and metadata
- **media.csv**: structured metadata describing each media file and its attributes  
- **location.csv**: structured metadata describing geographic locations  

> ⚠️ Note: For the current dashboard, please use the exact file and column names as defined in these metadata files. 



### 1. `media.csv`

This CSV lists all media items.

**Columns:**

| Column        | Type   | Description                                           |
|---------------|--------|-------------------------------------------------------|
| `file_name`   | string | File name (relative to `./data/`)                     |
| `extension`   | string | File extension (e.g., `.wav`, `.mp4`, `.jpg`)         |
| `data_type`   | string | Media type: `audio`, `video`, `image`                 |
| `location_tag`| string | Human-readable location name                          |
| `latitude`    | float  | Latitude (WGS84)                                      |
| `longitude`   | float  | Longitude (WGS84)                                     |
| `date`        | date   | Capture date (ISO `YYYY-MM-DD`)                       |
| `time`        | time   | Capture time (`HH:MM:SS`)                             |
| `device`      | string | Recording/capture device (may be blank)               |
| `duration`    | string | Duration (e.g., `00:00:20.053`) for audio/video       |
| `file_size`   | string | File size (e.g., `3.9 MB`)                            |

**Example (`media.csv`):**

```csv
file_name,extension,data_type,location_tag,latitude,longitude,date,time,device,duration,file_size
MEIL-01_20250630_140925_ss002938.wav,.wav,audio,MagongAnshanPagoda,23.556574,119.574373,2025-06-30,14:09:25,,00:00:19.995,3.8 MB
MEIL-01_20250615_194851_ss001449.wav,.wav,audio,AimenWaterReservoir,23.556731,119.634467,2025-06-15,19:48:51,,00:00:20.053,3.9 MB
MEIL03_20250807_225039_ss001454.wav,.wav,audio,BaishaTongliangBaoanGong,23.656876,119.557356,2025-08-07,22:50:39,,00:00:20.062,3.5 MB
```

### 2. `location.csv`

This CSV defines all recording/capture locations.

**Columns:**

| Column     | Type   | Description                          |
|------------|--------|--------------------------------------|
| `location` | string | Human-readable location name          |
| `longitude`| float  | Longitude (WGS84)                    |
| `latitude` | float  | Latitude (WGS84)                     |

**Example (`location.csv`):**

```csv
location,longitude,latitude
AimenSanShengDianTemple,119.636675,23.561718
AimenWaterReservoir,119.634467,23.556731
BaishaTongliangBaoanGong,119.557356,23.656876
```
---


### 3. Current supported media formats

The dashboard determines media type from the data_type column if available.
If missing, it falls back to the file extension (file_name or extension).

- **Audio**: `wav`, `mp3`, `m4a`, `ogg`, `flac`, `aac`  
- **Video**: `mp4`, `mov`, `m4v`, `webm`  
- **Image**: `jpg`, `jpeg`, `png`, `gif`, `webp`  

