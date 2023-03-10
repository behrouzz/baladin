**Author:** Behrouz Safari<br/>
**Website:** [AstroDataScience.Net](http://astrodatascience.net/)<br/>

# baladin
*Pythonic tool to work with Aladin Lite*


## Installation

Install the latest version from [PyPI](https://pypi.org/project/baladin/):

    pip install baladin

The only requirement is *pandas*.


*For more information, check these links:*<br/>
* [Build an interactive sky map with Aladin Lite](https://aladin.cds.unistra.fr/AladinLite/doc/tutorials/interactive-finding-chart/)<br/>
* [Image surveys](http://aladin.unistra.fr/hips/list)<br/>
* [REST api example](https://aladin.cds.unistra.fr/AladinLite/v3-beta/?fov=0.06&ra=151.7573568&dec=-40.4364251&baseImageLayer=CDS%2FP%2FunWISE%2Fcolor-W2-W1W2-W1&overlayImageLayer=https%3A%2F%2Falasky.cds.unistra.fr%2FJWST%2FCDS_P_JWST_Southern-Ring-Nebula_NIRCam&cooFrame=ICRS)<br/>


## Example 1 : add surveys and markers

```python
from baladin import Aladin

a = Aladin(target='270.6003707 -23.0224839')

buttons = [
    ('P/2MASS/color', 'bs 2MASS'),
    ('P/GLIMPSE360', 'bs GLIMPSE 360'),
    ]

markers = [
    (270.332621, -23.078944, 'PSR B1758-23', 'Object type: Pulsar'),
    (270.63206,  -22.905550, 'HD 164514',    'Object type: Star in cluster'),
    (270.598121, -23.030819, 'HD 164492',    'Object type: Double star'),
    ]

a.add_survey_buttons(buttons)
a.add_markers(markers)

a.create()
a.save('index.html')
```


## Example 2 : add SIMBAD and VizieR layers

```python
from baladin import Aladin

a = Aladin(target='270.6003707 -23.0224839')

a.add_simbad()

a.add_vizier('I/239/hip_main')

a.create()
a.save('index.html')
```

You can pass optional arguments *target* and *radius* to both *add_simbad* and *add_vizier* methods.


## Example 3 : *Southern-Ring-Nebula* from JWST as overlay layer

```python
from baladin import Aladin

a = Aladin(target='151.75735684271, -40.43642515362001', fov=0.1)

buttons = [
    ('P/2MASS/color', '2MASS'),
    ('P/DSS2/color', 'DSS'),
    ]

a.add_survey_buttons(buttons)

hips_id = 'CDS/P/JWST/Southern-Ring-Nebula/NIRCam'
hips_name = 'Southern-Ring-Nebula'
hips_base_url = 'https://alasky.cds.unistra.fr/JWST/CDS_P_JWST_Southern-Ring-Nebula_NIRCam'
hips_max_ord = 14

a.add_image_overlayer(hips_id, hips_name, hips_base_url, hips_max_ord, slider=True)

a.create()
a.save('index.html')
```

See more at [astrodatascience.net](https://astrodatascience.net/)
