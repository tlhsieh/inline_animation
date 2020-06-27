# Jupyter Notebook inline animation with Bokeh

Given a 3d array, generates an inline animation of 2d slices along the 0th axis. Requires [Bokeh](https://bokeh.org).

### Example

```python
import numpy as np

import viz

# generate data
xvec = np.linspace(-2, 2, 100)
yvec = np.linspace(-2, 2, 100)
tvec = np.linspace(0, 2*np.pi, 20)
xx, yy = np.meshgrid(xvec, yvec)
data = np.array([np.exp(-((xx - np.cos(t))**2 + (yy - np.sin(t))**2)/(2*0.4**2)) for t in tvec])

# generate movie
viz.movie(data, yvec, xvec, sizefac=4)
```

### Example 2: if input is xarry.DataArray, the x, y axes will be automatically loaded

```python
import numpy as np
import xarray as xr

import viz

# generate data
xvec = np.linspace(-2, 2, 100)
yvec = np.linspace(-2, 2, 100)
tvec = np.linspace(0, 2*np.pi, 20)
xx, yy = np.meshgrid(xvec, yvec)
data = np.array([np.exp(-((xx - np.cos(t))**2 + (yy - np.sin(t))**2)/(2*0.4**2)) for t in tvec])

data = xr.DataArray(data, coords=(tvec, yvec, xvec), dims=('t', 'y', 'x'))

# generate movie
viz.movie(data, xarray=True, sizefac=4)
```
![example](https://github.com/tlhsieh/inline_animation/blob/master/example.gif)


To animate line plots, see https://docs.bokeh.org/en/latest/docs/gallery/slider.html
