# Data for "Bacterial cheating drives the population dynamics of cooperative antibiotic resistance plasmids" 
## by Eugene A Yurtsev, Hui Xiao Chao, Manoshi S Datta, Tatiana Artemova, Jeff Gore
--------------------------------------------------------------------------------------------

Data is located inside csv files located inside the subfolder called ["data"](https://github.com/eyurtsev/bacterial_cheating/blob/master/data/). Blanks
represent missing data values. The following kinds of data are included:

1. time traces [(data/timetraces.csv)](https://github.com/eyurtsev/bacterial_cheating/blob/master/data/timetraces.csv)

    In these experiments, we tracked 23 populations over multiple cycles in a
    single environment (fixed ampicillin concentration). After 24 hours of
    growth, each culture was diluted into fresh medium. This medium was
    supplemented with antibiotic, so the starting antiboitic concentration at
    each cycle was at the same value across the different days.

    In this dataset, we include 3 biological replicates; i.e., all the
    experiments were done on the same 96-well plate during the same time, but
    with bacterial cultures that came from 6 different bacterial colonies (3
    resistant and 3 sensitive).

    Please read analysis section for more information.

    | column     | meaning                                                                                                                                                                         |
    |------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
    | amp        | concentration of the antibiotic ampicillin in micrograms per ml                                                                                                                                   |
    | culture_id | a **unique** integer assigned to each culture in the experiment                                                                               |
    | replicate  | integer to indicate from which experiment the data came from                                                                                                                    |
    | ODf        | Final population density (measured in units of optical density), population density at end of growth cycle  measurement corrected for non-linear effects and background         |
    | ff         | Final fraction of resistant cells (measured using flow cytometry), fraction of resistant cells at end of growth cycle                                                           |
    | dilution   | The amount by which the culture was diluted, ODi (at t+1) should be ODf (at t) divided by the dilution factor                                                                   |
    | tazobactam | concentration of inhibitor,  measured in either micrograms per ml or nanograms per ml.  Use manuscript for reference.                                                           |
    | day        | the time point, number of cycles that passed



2. Difference maps ([data/difference_maps_ampicillin_no_inhibitor.csv](https://github.com/eyurtsev/bacterial_cheating/blob/master/data/difference_maps_ampicillin_no_inhibitor.csv),
                    [data/difference_maps_ampicillin_with_tazobactam.csv](https://github.com/eyurtsev/bacterial_cheating/blob/master/data/difference_maps_ampicillin_with_tazobactam.csv))

    In these experiments, we grew many bacterial populations over a single cycle in
    a variety of environments (different tazobactam, ampicillin concentrations)
    from a variety of initial starting conditions (changing both the total initial
    cell density and the relative abundance of resistant and sensitive bacteria). 

    These experiments were done three times on different days with different
    bacterial cultures. As a result, the dataset should provide a good sense of
    the variability in the system.

    Please read analysis section for more information.

    | column     | meaning                                                                                                                                                                         |
    |------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
    | ampicillin | antibiotic concentration in micrograms per ml                                                                                                                                   |
    | culture_id | provided for convenience, but **not unique**, use ampicillin concentrations and replicate # to identify cultures uniquely                                                                               |
    | replicate  | integer to indicate from which experiment the data came from                                                                                                                    |
    | ODf        | Final population density (measured in units of optical density), population density at end of growth cycle  measurement corrected for non-linear effects and background         |
    | ODi        | Initial population density (measured in units of optical density), population density at beginning of growth cycle  measurement corrected for non-linear effects and background |
    | ff         | Final fraction of resistant cells (measured using flow cytometry), fraction of resistant cells at end of growth cycle                                                           |
    | fi         | Initial fraction of resistant cells (measured using flow cytometry), fraction of resistant cells at the beginning of the growth cycle                                           |
    | dilution   | The amount by which the culture was diluted, ODi (at t+1) should be ODf (at t) divided by the dilution factor                                                                   |
    | tazobactam | concentration of inhibitor,  measured in either micrograms per ml or nanograms per ml.  Use manuscript for reference.                                                           |

3. Extracted equilibrium fractions ([data/equilibrium_fractions_ampicillin_no_inhibitor.csv](https://github.com/eyurtsev/bacterial_cheating/blob/master/data/equilibrium_fractions_ampicillin_no_inhibitor.csv), 
[data/equilibrium_fractions_ampicillin_with_tazobactam.csv](https://github.com/eyurtsev/bacterial_cheating/blob/master/data/equilibrium_fractions_ampicillin_with_tazobactam.csv))

    For convenience we are providing the equilibrium fractions that we extracted
    from the difference map measurements. For each difference map, we determined
    where the difference map intersected the 1:1 line. (We used linear
    interpolation between the two points in the difference map that straddle the
    1:1 line to determine the equlibrium point.) The results were inspected
    visually to make sure that the determined equilibrium point agreed with the
    difference map.

    The results plotted in Fig 3C and 4C are the mean equilibrium fractions. The
    error is the standard error of the mean. 

    | column     | meaning                                                                                                                                                                         |
    |------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
    | ampicillin | antibiotic concentration in micrograms per ml                                                                                                                                   |
    | dilution   | The amount by which the culture was diluted, ODi (at t+1) should be ODf (at t) divided by the dilution factor                                                                   |
    | tazobactam | concentration of inhibitor,  measured in either micrograms per ml or nanograms per ml.  Use manuscript for reference.                                                           |
    | feq #1     | equilibrium fraction as determined during the first replicate experiment              |
    | feq #2     | equilibrium fraction as determined during the second replicate experiment             |
    | feq #3     | equilibrium fraction as determined during the third replicate experiment              |


## Analysis
--------------------------------------------------------------------------------------------

At the end of each cycle, we used a combination of flow cytometry and spectrophotometry to measure the
abundance of the sensitive and resistant cells in each bacterial culture. 

To get the data in the csv files, the following processing steps have taken place:

* The relative abundances of each population were extracted from raw fcs files using the appropriate gates. In a small fraction of the flow cytometery measurements, the cell density was too high in the well for accurate measurement of the relative abundance. Hence, the relative abundance was set to NaN when the event rate at the flow cytometer exceeded 2000 events / sec. 
* raw plate reader data was corrected for background noise and for plate reader saturation effects.
* meta data, plate reader measurements, and relative abundances were merged together into a table which was saved into this csv file.

## IPython notebooks and NBViewer
--------------------------------------------------------------------------------------------

ipynb files are ipython notebook files that contain analysis and/or produce
sample figures using the data in the csv files. The ipython notebooks are
provided simply as convenience to show how to work with some of the data inside
the csv files. These files are not meant to reproduce the figures in the
manuscript.

View these ipython notebooks online using the following links:

* [Timeseries](https://github.com/eyurtsev/bacterial_cheating/blob/master/timeseries.ipynb)
* [Difference Maps](https://github.com/eyurtsev/bacterial_cheating/blob/master/difference_maps.ipynb)
* [Equilibrium Fractions](https://github.com/eyurtsev/bacterial_cheating/blob/master/equilibrium_fractions.ipynb)

## Running IPython notebooks locally
--------------------------------------------------------------------------------------------

If you want to run any of these IPython notebooks locally, you will need to
install python and associated dependencies. A simple way of obtaining python
together with all the necessary dependencies is by installing either
[canopy](https://www.enthought.com/products/canopy/) or
[anaconda](https://store.continuum.io/cshop/anaconda/).

After installing these dependencies, you can launch an IPython notebook (or jupyter) by opening a shell
and typing: "ipython notebook".

The IPython notebooks included in this repository make use of the
[pandas](http://pandas.pydata.org/) python package. Please refer to pandas
official page for documentation.
