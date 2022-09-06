# canopy-app
Repository for low-level, stand-alone/column canopy parameterizations for testing and application to gridded atmospheric composition/air quality models.

Author(s):

Patrick Campbell, Zachary Moon, and Wei-Ting Hung

Compile, edit namelist, and run canopy model:
- `make`
- `namelist.canopy`
- `./canopy`

Canopy is parameterized by foliage distribution shape functions and parameters for different vegetation types.

- `canopy_parm_mod.F90`

Current Canopy-App components:

1.  In-Canopy Winds and Wind Adjustment Factor (WAF) for wildland fire spread and air quality applications.

    Namelist Option = `ifcanwind`

    - `canopy_wind_mod.F90`
    - `canopy_waf_mod.F90`

2.  In-Canopy vertical diffusion (i.e., eddy diffusivity adjustment) for air quality applications.

    Namelist Option = `ifcaneddy`

    - `canopy_eddyx_mod.F90`

3.  In-Canopy vertical photolysis attenuation for air quality applications.

    Namelist Option = `ifcanphot`

    - `canopy_phot_mod.F90`

Current Canopy-App inputs:

1.  Typical 2D gridded atmospheric model input variables in 1st layer above canopy (e.g., `input_variables.txt`).

    - `LAT`   : Latitude  (degrees)
    - `LON`   : Longitude (degrees)
    - `FH`    : Forest canopy height (m)
    - `WS`    : Wind speed at reference height (m/s), e.g., 10 m
    - `CLU`   : Forest clumping index (dimensionless)
    - `LAI`   : Leaf area index (m2/m2)
    - `VTYPE` : Vegetation type (dimensionless), e.g., VIIRS
    - `FFRAC` : Forest fraction (dimensionless)
    - `UST`   : Friction velocity (m/s)
    - `CSZ`   : Cosine of the solar zenith angle (dimensionless)
    - `Z0`    : Total surface roughness length (m)
    - `MOL`   : Monin-Obukhov Length (m)
    - `FRP`   : Total Fire Radiative Power (MW/grid cell)

2.  Generic 1D canopy profile specifications (e.g., `input_profile.txt`).

    - `CANLAY` : Canopy layer number (integer)
    - `ZK`     : Canopy layer resolution (m)

Main Citations (further references contained within):

Katul, G.G., Mahrt, L., Poggi, D., and Sanz, C. (2004). One- and two-equation models for canopy turbulence. Boundary-Layer Meteorol. 113: 81–109. https://doi.org/10.1023/B:BOUN.0000037333.48760.e5

Massman, W. J., J.M. Forthofer, and M.A. Finney. (2017). An improved canopy wind model for predicting wind adjustment factors and wildland fire behavior. Canadian Journal of Forest Research. 47(5): 594-603. https://doi.org/10.1139/cjfr-2016-0354

Makar, P., Staebler, R., Akingunola, A. et al. The effects of forest canopy shading and turbulence on boundary layer ozone. Nat Commun 8, 15243 (2017). https://doi.org/10.1038/ncomms15243


## Development

After cloning the repository,
set up the pre-commit hooks by invoking
```
pre-commit install --install-hooks
```
within the repository (after [installing `pre-commit`](https://pre-commit.com/#installation)).
This only has to be done once.
The [current configuration](./.pre-commit-config.yaml) applies
[`findent -i4`](https://www.ratrabbit.nl/ratrabbit/findent/) to fix indentation
and strips trailing whitespace.
Using pre-commit saves you time/energy and reduces diffs.
