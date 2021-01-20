# gpx_interpolate.py

Python script to interpolate GPX files using linear or spline interpolation.

Interpolate latitude, longitude, elevation and speed at any spatial resolution.

Forked from https://github.com/remisalmon/gpx_interpolate

Note:
* The speed and time interpolation need investigation; how realistic are they?
* Written GPX files need to have some sort of indication in the data that they are interpolated, non-original data - i.e. using gpx-extensions or steganographic code in decimal places, or something.
* Output file needs to be specifiable instead of just appending _interpolated.
* Interpolated points do not include the _original_ points.
* Default resolution changed to 50 (1 far too small for aircraft tracks).

## Usage

### Script
```
usage: gpx_interpolate.py [-h] [-d DEG] [-r RES] [-n NUM] [-s] FILE [FILE ...]

interpolate GPX files using linear or spline interpolation

positional arguments:
  FILE               GPX file

optional arguments:
  -h, --help         show this help message and exit
  -d DEG, --deg DEG  interpolation degree, 1=linear, 2-5=spline (default: 1)
  -r RES, --res RES  interpolation resolution in meters (default: 1)
  -n NUM, --num NUM  force point count in output (default: disabled)
  -s, --speed        save interpolated speed
```

### Module
```python
from gpx_interpolate import gpx_interpolate

gpx_data = {'lat':lat,
            'lon':lon,
            'ele':ele,
            'tstamp':tstamp,
            'tzinfo':tzinfo}

gpx_data_interp = gpx_interpolate(gpx_data, num = 0, res = 1.0, deg = 3)
```

where:
* `lat`, `lon` are the trackpoints latitude and longitude (in degree)
* `ele` (optional) is the trackpoints elevation (in meter)
* `tstamp` (optional) is the trackpoints timestamps (in second)
* `tzinfo` (optional) is the trackpoints timezone as a `datetime.tzinfo` subclass instance (`None` for UTC)
* `num` (optional) is the number of trackpoints of the interpolated data: `0` to disable (default)
* `res` (optional) is the interpolation resolution in meters: disabled if `num > 0`
* `deg` is the interpolation in degree: `1` for linear interpolation (default) or `2-5` for spline interpolation

`ele`, `tstamp` and `tzinfo` are optional and in that case must be set to `None`

### Example
:black_circle: = input GPX data, :red_circle: = interpolated GPX data  
![plot.png](plot.png)

## Requirements
```
gpxpy==1.4.2
scipy==1.5.4
numpy==1.19.4
```
