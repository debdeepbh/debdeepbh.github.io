---
title: 3D plots in python
tags: python plot matplotlib
---

Python library `matplolib` does a pretty good job.

## 3D scatter plot

* Note that we use `ax.scatter` instead of `plt.scatter` (as for 2d plots with `import matplotlib.pyplot as plt`)

```python
from mpl_toolkits.mplot3d import Axes3D

fig = plt.figure()
ax = Axes3D(fig)
ax.scatter(X, Y, Z, s = 10,  linewidth = 1 )
ax.text(X, Y, Z, str(99))
```

* **Aspect ratio:** the 3d plot messes up the aspect ratio. We _cannot_ set the aspect ratio to be equal using `ax.set_aspect('equal')`  (even though we should be able to).
This feature is not implemented yet (what?), so we add the following snippet to make it happen:

```python
extents = np.array([getattr(ax, 'get_{}lim'.format(dim))() for dim in 'xyz'])
sz = extents[:,1] - extents[:,0]
centers = np.mean(extents, axis=1)
maxsize = max(abs(sz))
r = maxsize/2
for ctr, dim in zip(centers, 'xyz'):
    getattr(ax, 'set_{}lim'.format(dim))(ctr - r, ctr + r)

ax.set_box_aspect((1, 1, 1))
```

Alternatively, set x, y, and z ranges manually so that the length of the ranges are the same and do  `ax.set_box_aspect((1, 1, 1))`:

```python
 XYZlim = [-3e-3, 3e-3]
 ax.set_xlim3d(XYZlim+1e-3)
 ax.set_ylim3d(XYZlim - 0.2e-3)
 ax.set_zlim3d(XYZlim + 3e-3)
 ax.set_aspect('equal')
ax.set_box_aspect((1, 1, 1))
```

[Source](https://stackoverflow.com/questions/8130823/set-matplotlib-3d-plot-aspect-ratio/19933125)
This snippet applies to `ax`, so we can convert it into a function `def fix_aspect(ax):` and call it.

* In 2D, the aspect ratio can be set using

```python
plt.axis('scaled')
```

and specify the axes limits using 

```python
plt.xlim(a, b)
plt.ylim(c, d)
```

**Caution:** `plt.axis('scaled')` goes _before_ setting `plt.xlim()` and `plt.ylim()` for the boundaries to remain faithful.


## Plotting a bunch of lines

Plotting each line using a `for` loop is too slow. Use `LineCollection` and `Line3DCollection` instead.
The format of the data has to be in the following format:

```python
[
 [ [start_x_1, start_y_1, start_z_1], [end_x_1, end_y_1, end_z_1] ], 
 [ [start_x_2, start_y_2, start_z_2], [end_x_2, end_y_2, end_z_2] ], 
 [ [start_x_3, start_y_3, start_z_3], [end_x_3, end_y_3, end_z_3] ], 
...
 [ [start_x_N, start_y_N, start_z_N], [end_x_N, end_y_N, end_z_N] ]
]
```

where there are `N` lines that start with `start` and ends at `end`. 
Note that The array has rank 3.

Example of such construction:
Given two `(N,3)` arrays `P_start` and `P_end`, to draw `N` lines between `P_start[i]` and `P_end[i]` in 3D, construct

```python
ls = [ [p_start, p_end] for p_start, p_end in zip(P_start, P_end) ]
```


* Plot using

```python
import matplotlib.pyplot as plt
from matplotlib.collections import Line3DCollection

lc = LineCollection3D(ls, linewidths=0.5, colors='b')

ax = plt.gca()
ax.add_collection(lc)

plt.show()
```

** Caution: ** For 2D plotting with `LineCollection`, you **must** add a scaling command like

```python
ax.autoscale()
```

for the plots to show. Otherwise, no line will be printed. (weird bug?)

**Note:** that the collection added to `ax` (and not to `plt`).
