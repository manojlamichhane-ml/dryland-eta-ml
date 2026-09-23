# Data

The raw data are not tracked in git because of their size. The eddy covariance and field data
come from the USDA-ARS Central Great Plains Research Station and are available on request
(see the paper's data availability statement).

## Folder layout expected by the notebooks

```
data/
├── raw/
│   ├── eddy_covariance/
│   │   ├── ASP/<YYYY>/<MM>/*.zip          one EddyPro (SMARTFlux) output per half hour
│   │   └── BAU/<YYYY>/<MM>/*.zip
│   ├── hls/
│   │   ├── Landsat/L<YYYY-MM-DD>/*.tif    HLS L30 bands (B02, B04, B05, B06) + Fmask
│   │   └── Sentinel/S<YYYY-MM-DD>/*.tif   HLS S30 bands (B02, B04, B8A, B11) + Fmask
│   ├── climate/
│   │   └── CoAgMet_Climatic_Data.csv      daily weather, Akron CoAgMet station
│   └── shapefiles/
│       ├── footprint_160m/{ASP,BAU}_footprint.shp
│       ├── study_extent/ET_Extent_Akron.shp
│       └── crop_fields/Crop_types_2019_2025.shp   field polygons with Year_2019 ... Year_2025 crop codes
├── processed/          written by notebooks 01-05
└── model_input/        written by notebook 06, used by notebooks 07-09
    ├── ASP_model_input.csv
    └── BAU_model_input.csv
```

HLS v2.0 data can be downloaded from NASA Earthdata (https://hls.gsfc.nasa.gov/hls-data/).
CoAgMet data are available from https://coagmet.colostate.edu/.

## Sites

| Code | Tower | Rotation | Tower location |
|---|---|---|---|
| ASP | EC-1 | wheat-corn-millet-fallow (aspirational) | 40.1585 N, 103.132 W |
| BAU | EC-2 | wheat-fallow (business as usual) | 40.1503 N, 103.145 W |

## Model input table (`model_input/<SITE>_model_input.csv`)

One row per day with a tower ETa value.

| Column | Description | Unit |
|---|---|---|
| `date` | day | YYYY-MM-DD |
| `ETa` | daily actual evapotranspiration from the EC tower (target) | mm/day |
| `<IDX> Mean`, `<IDX> Median` | footprint mean / median of NDVI, EVI, SAVI, MSAVI, NDWI, MSI, SR, linearly interpolated between HLS overpasses | - |
| `DOY` | day of year | - |
| `Tavg`, `Tmax`, `Tmin` | air temperature | °C |
| `RHmax`, `RHmin` | relative humidity | fraction |
| `Rs` | incoming solar radiation | W/m² |
| `Precipitation` | precipitation on the day (Pcp in the paper) | mm |
| `3-d pcp` ... `10-d pcp` | precipitation over the preceding 3-10 days, excluding the current day | mm |
| `U` | wind speed | m/s |
| `ASCE ETr` | ASCE standardized reference ET (alfalfa) | mm/day |
| `Ts` | soil temperature | °C |

Only the column names are fixed; additional weather columns in the CoAgMet export are carried through and ignored by the models.
