
## ggplot2

![[Pasted image 20240306164941.png]]

Notice that `jitter` can be a geom itself (i.e. `geom_jitter()`), an argument in `geom_point()` (i.e. `position = "jitter"`), or a position function, (i.e. `position_jitter()`).

Shape attribute values.
![[Pasted image 20240306162838.png|300]]

An internal variable called `density` can be accessed by using the `..` notation, i.e. `..density..`

*Positions in histograms*
Here, we'll examine the various ways of applying positions to histograms. [`geom_histogram()`](http://www.rdocumentation.org/packages/ggplot2/functions/geom_histogram), a special case of [`geom_bar()`](http://www.rdocumentation.org/packages/ggplot2/functions/geom_bar), has a `position` argument that can take on the following values:
- `stack` (the default): Bars for different groups are stacked on top of each other.
- `dodge`: Bars for different groups are placed side by side.
- `fill`: Bars for different groups are shown as proportions.
- `identity`: Plot the values as they appear in the dataset.

> I highly discourage dynamite plots.

Remember, the reason you want to use `position=position_dodge(width=0.1)` (and `position=position_jitter(width=0.1)`) is to specify _how much_ dodging (or jittering) you want. (instead of `position="jitter"` or `position="dodge"`)

![[Pasted image 20240306165145.png]]