Specifications of main functions in the GrainSizeTools script
-------------

####**extract_areas** (*filePath*, *type = 'txt', col_name='Area'*)
Automatically extracts the data corresponding to the areas of grain profiles from the tabular-like data generated in the ImageJ application. To avoid problems use always forward slashes (or double backslashes) in the file path.

> **Inputs:**
>
> ***filePath***: *string*  
> The file location in the OS in quotes. To avoid problems use always forward slash (or double backslash)
>
> ***type***: *string; optional*  
> The type of the file, either 'txt' or 'csv'
>
>***col_name***: *string; optional*
> The name of the column that contains the areas of the grain profiles. It is set to 'Area' by default.
>
> **Returns**:  
> A numpy array with the areas of the grain profiles.

####**calc_diameters** (*areas, addPerimeter = 0*)
Calculate the diameters from the sectional areas via the equivalent circular diameter assuming that the grains have near-equant shapes.

> **Inputs:**
>
> ***areas***: *array_like*  
> The sectional areas of the grains.
>
> ***addPerimeter***: *integer or float; optional*  
> Correct the diameters estimated from the areas by adding the perimeter of the grain. If *addPerimeter* is not declared it is considered 0.

>**Returns**:  
> A numpy array with the diameters of the grains.

####**find_grain_size** (*areas, diameters, plot = 'freq', binsize = 'Scott'*)
Estimate different 1D measures of grain size from a population of apparent diameters and their areas. It includes the mean, the area-weighted mean, the median and the frequency peak grain sizes.

> **Inputs:**
>
> ***areas***: *array_like*  
> The areas of the grain profiles.
>
> ***diameters***: *array_like*  
> The apparent diameters of the grains.
>
> ***plot***: *string; optional*
> The preferred type of plot and grain size estimation. This can be 'freq' for a frequency vs diameter plot, 'log' for a frequency vs logarithmic diameter plot, 'sqrt' for a frequency vs square root diameter plot, and 'area' for a area-weighted frequency vs diameter plot.
>
> ***binsize***: *string, integer or float; optional*  
> The method used to calculate the bin size. This can be: 'FD' (Fredman-Diaconis rule), 'Scott' (Scott rule) or a user-defined scalar of type integer or float. If not specified, 'Scott' is used by default.
>
>**Returns**:  
> A number of 1D grain size values to use in paleopiezometry (or paleowattmetry) studies and the chosen plot. The values includes the mean, the median, the area-weighted mean and the frequency peak via the Gaussian kernel density estimator grain sizes. It also provides other values of interest such as the bin size and bandwidth estimated as well as the methods chosen.

####**derive3D** (*diameters, numbins=10, set_limit=None, fit=False, initial_guess=False*)
Estimates the actual population of diameters from a population of apparent diameters obtained from a thin section. It uses two approaches:

i) the standard Saltykov method (Saltykov 1967; Underwood 1970)  
ii) the two-step method (Lopez-Sanchez and Llana-Funez, in review)

The Saltykov method is optimal to estimate the volume of particular grain fraction as well as to obtain a qualitative view of the appearance of the actual 3D grain size population, either in uni- or multimodal populations. The two-step method is aimed at quantitatively estimating the actual 3D population of grain size. It is only valid for unimodal populations (*i.e.* completely recrystallized rocks) and returns the shape and scale values that describe the log-normal population of grain sizes as well as a plot.

> **Inputs:**
>
> ***diameters***: *array_like*  
> The apparent diameters of the grains.
>
> ***numbins***: *integer; optional*  
> The number of classes or bins used by the Saltykov method to unfold the population. If not declared, is set to ten by default.
>
> ***set_limit***: *integer or float; optional*  
> If the user defines a number, the script will return the volume occupied by the grain fraction of size less than or equal to that value.
>
> ***fit***: *True or False*  
> If False, the standard Saltykov method is applied. If True, the two-step method is applied. The Saltykov method is set by default.
>
>***initial_guess***: *True or False*  
> If False, the script will use the default guessing values to fit a log-normal distribution. If True, the script will ask the user to define the shape and scale guessing values.
>
>**Returns**:  
> In the case of the Saltykov method: The bin size, the frequencies (probabilities) of the different classes and a plot containing two subplots: i) the distribution of the actual grain size population according to the Saltykov method and ii) the volume-weighted cumulative distribution. The frequencies are normalized such that the integral over the range is one. Note that the sum of these values will not be equal to one unless bins of unity width are chosen. In the case of the two-step method: The optimal MSD and scale values and the precision of the estimation at a 3-sigma level.  Also a plot containing the unfolded population using the Saltykov method and the fitted lognormal probability density function with a trust region.

[next section](https://github.com/marcoalopez/GrainSizeTools/blob/master/DOCS/imageJ_tutorial.md)  
[table of contents](https://github.com/marcoalopez/GrainSizeTools/blob/master/DOCS/imageJ_tutorial.md)

----------
