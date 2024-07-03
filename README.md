# gramm


 [![View gramm on File Exchange](https://www.mathworks.com/matlabcentral/images/matlab-file-exchange.svg)](https://mathworks.com/matlabcentral/fileexchange/54465-gramm-data-visualization-toolbox)

Gramm is a Matlab toolbox that enables the rapid creation of complex, publication-quality figures. Its design philosophy focuses on a *declarative* approach, where users specify the desired end result, as opposed to the traditional *imperative* method involving for loops, if/else statements, etc.

The Matlab implementation of `gramm` is inspired by the "grammar of graphics" principles ([Wilkinson 1999](http://www.springer.com/de/book/9781475731002)) and the ([ggplot2](http://ggplot2.tidyverse.org/)) library for R by Hadley Wickham. As a reference to this inspiration, gramm stands for **GRAM**mar of graphics for **M**ATLAB. A similar library called [Seaborn](https://seaborn.pydata.org) also exists for Python.

Gramm has been used in many publications from varied fields, but is particularily suited for neuroscience, from human movement psychophysics ([Morel et al. 2017](https://doi.org/10.1371/journal.pbio.2001323)), to electrophysiology ([Morel et al. 2016](https://doi.org/10.1088/1741-2560/13/1/016002); [Ferrea et al. 2017](https://doi.org/10.1152/jn.00504.2017)), human functional imaging  ([Wan et al. 2017](https://doi.org/10.1002/hbm.23932)) and animal training ([Berger et al. 2017](https://doi.org/10.1152/jn.00614.2017)).

- [Workflow](#workflow)
- [Demo live scripts](#demo-live-scripts)
- [About gramm](#about-gramm)
  - [Installation](#Installation)
  - [Documentation](#Documentation)
  - [Citing gramm](#citing-gramm)
- [Features](#features)
- [Gallery](#gallery)

## Workflow

The typical workflow to generate a figure is detailed in the ["Getting Started" live script.](#demo-live-scripts)

In short:
1. Provide gramm with the relevant data for the figure: X and Y variables, but also grouping variables that will determine color, subplot rows/columns, etc.
2. Add graphical layers to your figure: raw data layers (directly plot data as points, lines...) or statistical layers (fits, histograms, densities, summaries with confidence intervals...). One instruction is enough to add each layer, and all layers offer many customization options.
3. Draw the figure, gramm takes care of all the annoying parts: no need to loop over colors or subplots, colors and legends are generated automatically, axes limits are taken care of, etc.

For example, with gramm, 7 lines of code are enough to create the figure below from the <code>carbig</code> dataset. Here the figure represents the evolution of fuel economy of new cars in time, with number of cylinders indicated by color, and regions of origin separated across subplot columns:
<img src="images/gettingstarted_export.png" alt="GettingStarted example" width="800">

```matlab
load example_data.mat %Load example dataset about cars

% Create a gramm object, provide x (year of production) and y (fuel economy) data,
% color grouping data (number of cylinders) and select a subset of the data
g=gramm('x',cars.Model_Year,'y',cars.MPG,'color',cars.Cylinders,...
    'subset',cars.Cylinders~=3 & cars.Cylinders~=5);
% Subdivide the data in subplots horizontally by region of origin
g.facet_grid([],cars.Origin_Region);
% Plot raw data as points
g.geom_point("dodge",0.5);
% Plot linear fits of the data with associated confidence intervals 
g.stat_glm();
% Set appropriate names for legends
g.set_names('column','Origin', 'x','Year of production', y','Fuel economy (MPG)','color','# Cylinders');
%Set figure title
g.set_title('Fuel economy of new cars between 1970 and 1982');
% Do the actual drawing
g.draw();
```

## Demo live scripts ##
|Demo|View online|Open in Matlab Online|Preview|
|---|---|---|---|
|Getting Started|[👀 Preview](http://htmlpreview.github.io/?https://github.com/piermorel/gramm/blob/packaging/gramm/html/GettingStarted.html) |[![Open in MATLAB Online](https://www.mathworks.com/images/responsive/global/open-in-matlab-online.svg)](https://matlab.mathworks.com/open/github/v1?repo=piermorel/gramm&file=gramm/doc/GettingStarted.mlx)|<img src="images/gettingstarted_export.png" width="300">|
|Explore grouped data|[👀 Preview](http://htmlpreview.github.io/?https://github.com/piermorel/gramm/blob/packaging/gramm/html/GettingStarted.html) |[![Open in MATLAB Online](https://www.mathworks.com/images/responsive/global/open-in-matlab-online.svg)](https://matlab.mathworks.com/open/github/v1?repo=piermorel/gramm&file=gramm/doc/Groups.mlx)|<img src="images/groups_export.png" width="300">|
|Explore X/Y data|[👀 Preview](http://htmlpreview.github.io/?https://github.com/piermorel/gramm/blob/packaging/gramm/html/XY.html) |[![Open in MATLAB Online](https://www.mathworks.com/images/responsive/global/open-in-matlab-online.svg)](https://matlab.mathworks.com/open/github/v1?repo=piermorel/gramm&file=gramm/doc/XY.mlx)|<img src="images/xy_export.png" width="300">|
|Explore Time Series data|[👀 Preview](http://htmlpreview.github.io/?https://github.com/piermorel/gramm/blob/packaging/gramm/html/TimeSeries.html) |[![Open in MATLAB Online](https://www.mathworks.com/images/responsive/global/open-in-matlab-online.svg)](https://matlab.mathworks.com/open/github/v1?repo=piermorel/gramm&file=gramm/doc/TimeSeries.mlx)|<img src="images/timeseries_export.png" width="300">|
|Advanced examples|[👀 Preview](http://htmlpreview.github.io/?https://github.com/piermorel/gramm/blob/packaging/gramm/html/examples.html) |[![Open in MATLAB Online](https://www.mathworks.com/images/responsive/global/open-in-matlab-online.svg)](https://matlab.mathworks.com/open/github/v1?repo=piermorel/gramm&file=gramm/doc/examples.mlx)|<img src="images/overlaid_export.png" width="300">|


## About gramm ##

### Installation ###

- Automatically within MATLAB : Open the Add-ons explorer, search for "gramm" and click Add !
- Or by downloading the toolbox package : download the latest .mltbx file from the [GitHub Releases](https://github.com/piermorel/gramm/releases) and double-click the downloaded file to install.

### Documentation ###

Once the toolbox is installed, type ```doc``` in the MATLAB command window and you will see gramm in the "Supplemental Software" on the bottom left menu. From there you will have access to several live script demos and a cheat sheet with all commands in a compact format.

### Citing gramm ###

Gramm has been published in the Journal of Open Source Software. If you use gramm plots in a publication you can thus cite it using the following:

[![DOI](http://joss.theoj.org/papers/10.21105/joss.00568/status.svg)](https://doi.org/10.21105/joss.00568)

Morel, (2018). Gramm: grammar of graphics plotting in Matlab. Journal of Open Source Software, 3(23), 568, https://doi.org/10.21105/joss.00568

### Compatibility ###

 Recent versions of gramm (3.0 and above) target MATLAB above R2018b. Older releases work in older MATLAB versions. The statistics toolbox is required for some methods: <code>stat_glm()</code>, some <code>stat_summary()</code> methods, <code>stat_density()</code>. The curve fitting toolbox or the statistics toolbox is required for <code>stat_fit()</code>.


## Main Features
- Accepts X, Y, Z and grouping data in varied types and shapes (arrays, matrices, cells)

- Multiple ways of separating groups of data:
  - Colors, lightness, point markers, line styles, and point/line size (<code>'color'</code>, <code>'lightness'</code>, <code>'marker'</code>, <code>'linestyle'</code>,  <code>'size'</code>)
  - Subplots by row and/or columns, or wrapping columns (<code>facet_grid()</code> and <code>facet_wrap()</code>). Multiple options for consistent axis limits across facets, rows, columns, etc. (using <code>'scale'</code> and <code>'space'</code>)
  - Separate figures (<code>fig()</code>)

- Multiple ways of directly plotting the data:
  - scatter plots (<code>geom_point()</code>) and jittered scatter plot (<code>geom_jitter()</code>)
  - lines (<code>geom_line()</code>)
  - pre-computed confidence intervals (<code>geom_interval()</code>)
  - bars plots (<code>geom_bar()</code>)
  - raster plots (<code>geom_raster()</code>)
  - labels (<code>geom_label()</code>)
  - point counts (<code>geom_count()</code>)
  - swarm / beeswarm plots (<code>geom_swarm()</code>)
  - text labels (<code>geom_label()</code>)


- Multiple statistical visualizations on the data:
  - y data summarized by x values (uniques or binned) with confidence intervals (<code>stat_summary()</code>)
  - histograms and density plots of x values (<code>stat_bin()</code> and <code>stat_density()</code>)
  - box and whisker plots (<code>stat_boxplot()</code>)
  - violin plots (<code>stat_violin()</code>)
  - quantile-quantile plots (<code>stat_qq()</code>) of x data distribution against theoretical distribution or y data distribution.
  - Smoothed data (<code>stat_smooth()</code>)
  - 2D binning (<code>stat_bin2d()</code>)
  - GLM fits (<code>stat_glm()</code>, requires statistics toolbox)
  - Custom fits with user-provided anonymous function (<code>stat_fit()</code>)
  - Ellipses of confidence (<code>stat_ellipse()</code>)

- Easy export in multiple formats with a convenient <code>export()</code> method that can be called after <code>draw()</code> and maintains correct dimensions/aspect ratio. 
- All visualizations have plenty of options accessible through arguments, from computational to esthetic ones.
- Representation of groupings can be fully customized (colormaps, ordering)
- Multiple gramm plots can be combined in the same figure by creating a matrix of gramm objects and calling the <code>draw()</code> method on the whole matrix. An overarching title can be added by calling <code>set_title()</code> on the whole matrix.
- MATLABs axes properties are acessible through the method <code>axe_property()</code>
- Non-data graphical elements can be added such as reference lines or polygons (<code>geom_abline()</code>, <code>geom_vline()</code>,<code>geom_hline()</code>,<code>geom_polygon()</code>)


## Gallery

All these examples are from the [advanced examples live scripts](#demo-live-scripts)

### Superimposition of gramm objects on the same axes

<img src="images/overlaid_export.png" width="600">

### Custom layouts ###

<img src="images/layout_export.png" alt="Custom layouts" width="600">

### Grid and scaling options ###

<img src="images/scaling_export.png" alt="facet_grid() options" width="600">

### Colormap and legend options ###

<img src="images/colorlegend_export.png" alt="facet_grid() options" width="600">

## Acknowledgements
gramm was inspired and/or used code from:
- [ggplot2](http://ggplot2.org)
- [Panda](http://www.neural-code.com/index.php/panda) for color conversion
- [subtightplot](http://www.mathworks.com/matlabcentral/fileexchange/39664-subtightplot) for subplot creation
- [colorbrewer2](http://colorbrewer2.org)
- [viridis colormap](https://bids.github.io/colormap/)
