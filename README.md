# Data for "Bacterial cheating drives the population dynamics of cooperative antibiotic resistance plasmids" by Eugene A Yurtsev, Hui Xiao Chao, Manoshi S Datta, Tatiana Artemova, Jeff Gore

Data is located inside csv files located inside the subfolder called "data". Blanks
represent missing data values.

The following kinds of data are included:

1. time traces used to produce Figure 1A (**data/Figure1A.csv**)

    In these experiments, we tracked a few select populations over multiple cycles
    in a single environment (fixed ampicillin concentration). After 24 hours of
    growth, each culture was diluted into fresh medium. This medium was
    supplemented with antibiotic, so the starting antiboitic concentration at each
    cycle was at the same value across the different days.

    Please read analysis section for more information.

2. Difference maps (**data/difference_maps_ampicillin_no_inhibitor.csv**, **data/difference_maps_ampicillin_with_tazobactam.csv**)

    In these experiments, we grew many bacterial populations over a single cycle in
    a variety of environments (different tazobactam, ampicillin concentrations)
    from a variety of initial starting conditions (changing both the total initial
    cell density and the relative abundance of resistant and sensitive bacteria). 

    These experiments were done 3 times.

    Please read analysis section for more information.

    ### columns in csv file

    * ampicillin - antibiotic concentration in micrograms per ml
    * fraction # - integer between [0, 23] or [0, 11]. used for convenience
    to enumerate the different initial starting fractions.
    * ODf - final optical density
    * ODi - initial optical density (if available).
    * ff - fraction of ampicillin resistant cells measured at the end of the growth cycle
    * fi - fraction of ampicillin resistant cells measured at the beginning of the growth cycle
    * replicate - either 0, 1, 2 denotes the experiment from which the data came.
    * dilution - the amount by which the culture gets diluted between consecutive growth cycles. (The initial density in cycle t+1 should be the final density in cycle t over the dilution factor.)
    * tazobactam - measured in either nanograms per ml or micrograms per ml. use manuscript as reference.

3. Extracted equilibrium fractions (**data/equilibrium_fractions_ampicillin_no_inhibitor.csv**, **data/equilibrium_fractions_ampicillin_with_tazobactam.csv**)

    For convenience we are providing the equilibrium fractions that we extracted
    from the difference map measurements. For each difference map, we determined
    where the difference map intersected the 1:1 line. (We used linear
    interpolation between the two points in the difference map that straddle the
    1:1 line to determine the equlibrium point.) The results were inspected
    visually to make sure that the determined equilibrium point agreed with the
    difference map.

    The results plotted in Fig 3C and 4C are the mean equilibrium fractions. The
    error is the standard error of the mean. 

    ### columns in csv file

    * dilution, ampicillin - same as before
    * feq #1 - equilibrium fraction as determined during the first replicate experiment
    * feq #2 - equilibrium fraction as determined during the second replicate experiment
    * feq #3 - equilibrium fraction as determined during the third replicate experiment

## Analysis

At the end of each cycle, we used a combination of flow cytometry and spectrophotometry to measure the
abundance of the sensitive and resistant cells in each bacterial culture. 

The data that is contained inside the files reports the final abundance of the
two subpopulations on each day. (If not available, the initial abundance on a
given day can be calculated by taking the final abundance over the previous day
and dividing it by the dilution factor.)

To get the data in the csv files, the following processing steps have taken place:

A. The relative abundances of each population were extracted from raw fcs files using the appropriate gates. In a small fraction of the flow cytometery measurements, the cell density was too high in the well for accurate measurement of the relative abundance. Hence, the relative abundance was set to NaN when the event rate at the flow cytometer exceeded 2000 events / sec. 
B. raw plate reader data was corrected for background noise and for plate reader saturation effects.
C. meta data, plate reader measurements, and relative abundances were merged together into a table which was saved into this csv file.

## IPython notebooks and NBViewer

ipynb files are ipython notebook files that contain analysis and/or produce
sample figures using the data in the csv files. The ipython notebooks are
provided simply as convenience to show how to work with some of the data inside
the csv files. These files are not meant to reproduce the figures in the
manuscript.

View these ipython notebooks online using the following links:

* [Equilibrium Fractions](http://nbviewer.ipython.org/urls/bitbucket.org/eugene_yurtsev/bacterialcheatingproject/raw/master/sample_plot_equilibrium_fractions.ipynb)
* [Figure 1A](http://nbviewer.ipython.org/urls/bitbucket.org/eugene_yurtsev/bacterialcheatingproject/raw/master/Figure1A.ipynb)
* [Difference maps](http://nbviewer.ipython.org/urls/bitbucket.org/eugene_yurtsev/bacterialcheatingproject/raw/master/difference_maps.ipynb)

