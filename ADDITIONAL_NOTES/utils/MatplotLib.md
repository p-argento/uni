## Matplotlib tutorial
from https://matplotlib.org/stable/users/explain/quick_start.html#quick-start

![[Pasted image 20240329172459.png]]


### [`Artist`](https://matplotlib.org/stable/api/artist_api.html#matplotlib.artist.Artist "matplotlib.artist.Artist")
Basically, everything visible on the Figure is an Artist (even [`Figure`](https://matplotlib.org/stable/api/figure_api.html#matplotlib.figure.Figure "matplotlib.figure.Figure"), [`Axes`](https://matplotlib.org/stable/api/_as_gen/matplotlib.axes.Axes.html#matplotlib.axes.Axes "matplotlib.axes.Axes"), and [`Axis`](https://matplotlib.org/stable/api/axis_api.html#matplotlib.axis.Axis "matplotlib.axis.Axis") objects). This includes [`Text`](https://matplotlib.org/stable/api/text_api.html#matplotlib.text.Text "matplotlib.text.Text") objects, [`Line2D`](https://matplotlib.org/stable/api/_as_gen/matplotlib.lines.Line2D.html#matplotlib.lines.Line2D "matplotlib.lines.Line2D") objects, [`collections`](https://matplotlib.org/stable/api/collections_api.html#module-matplotlib.collections "matplotlib.collections") objects, [`Patch`](https://matplotlib.org/stable/api/_as_gen/matplotlib.patches.Patch.html#matplotlib.patches.Patch "matplotlib.patches.Patch") objects, etc. When the Figure is rendered, all of the Artists are drawn to the **canvas**. Most Artists are tied to an Axes; such an Artist cannot be shared by multiple Axes, or moved from one to another.

### [`Axes`](https://matplotlib.org/stable/api/_as_gen/matplotlib.axes.Axes.html#matplotlib.axes.Axes "matplotlib.axes.Axes")
An Axes is an Artist attached to a Figure that contains a region for plotting data.

It usually includes two (or three in the case of 3D) [`Axis`](https://matplotlib.org/stable/api/axis_api.html#matplotlib.axis.Axis "matplotlib.axis.Axis") objects (be aware of the difference between **Axes** and **Axis**) that provide ticks and tick labels to provide scales for the data in the Axes.

Each [`Axes`](https://matplotlib.org/stable/api/_as_gen/matplotlib.axes.Axes.html#matplotlib.axes.Axes "matplotlib.axes.Axes") also has a title (set via [`set_title()`](https://matplotlib.org/stable/api/_as_gen/matplotlib.axes.Axes.set_title.html#matplotlib.axes.Axes.set_title "matplotlib.axes.Axes.set_title")), an x-label (set via [`set_xlabel()`](https://matplotlib.org/stable/api/_as_gen/matplotlib.axes.Axes.set_xlabel.html#matplotlib.axes.Axes.set_xlabel "matplotlib.axes.Axes.set_xlabel")), and a y-label set via [`set_ylabel()`](https://matplotlib.org/stable/api/_as_gen/matplotlib.axes.Axes.set_ylabel.html#matplotlib.axes.Axes.set_ylabel "matplotlib.axes.Axes.set_ylabel")).

The [`Axes`](https://matplotlib.org/stable/api/_as_gen/matplotlib.axes.Axes.html#matplotlib.axes.Axes "matplotlib.axes.Axes") class and its member functions are the primary entry point to working with the OOP interface, and have *most of the plotting methods defined on them* (e.g. `ax.plot()`, shown above, uses the [`plot`](https://matplotlib.org/stable/api/_as_gen/matplotlib.axes.Axes.plot.html#matplotlib.axes.Axes.plot "matplotlib.axes.Axes.plot") method)

### Input type
*Common convention is to convert these to [`numpy.array`](https://numpy.org/doc/stable/reference/generated/numpy.array.html#numpy.array "(in NumPy v1.26)") objects prior to plotting.*
Plotting functions expect [`numpy.array`](https://numpy.org/doc/stable/reference/generated/numpy.array.html#numpy.array "(in NumPy v1.26)") or [`numpy.ma.masked_array`](https://numpy.org/doc/stable/reference/generated/numpy.ma.masked_array.html#numpy.ma.masked_array "(in NumPy v1.26)") as input, or objects that can be passed to [`numpy.asarray`](https://numpy.org/doc/stable/reference/generated/numpy.asarray.html#numpy.asarray "(in NumPy v1.26)"). Classes that are similar to arrays ('array-like') such as [`pandas`](https://pandas.pydata.org/pandas-docs/stable/index.html#module-pandas "(in pandas v2.2.1)") data objects and [`numpy.matrix`](https://numpy.org/doc/stable/reference/generated/numpy.matrix.html#numpy.matrix "(in NumPy v1.26)") may not work as intended. Common convention is to convert these to [`numpy.array`](https://numpy.org/doc/stable/reference/generated/numpy.array.html#numpy.array "(in NumPy v1.26)") objects prior to plotting. For example, to convert a [`numpy.matrix`](https://numpy.org/doc/stable/reference/generated/numpy.matrix.html#numpy.matrix "(in NumPy v1.26)")

## PyPlot Tutorial
https://matplotlib.org/stable/tutorials/pyplot.html#sphx-glr-tutorials-pyplot-py

