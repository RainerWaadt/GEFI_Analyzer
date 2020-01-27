# GEFI_Analyzer
Fiji plugin for spatiotemporal analyses of genetically encoded fluorescent indicators in plant roots

The GEFI Analyzer plugin is a Fiji plugin that utilizes additional plugins, such as VectorGraphics2D-0.13 (https://github.com/eseifert/vectorgraphics2d) and xchart-3.5.2 (https://github.com/knowm/XChart).

This plugin requires processed and thresholded image stacks so that outside the specimen pixel values are NaN.

DEAD Plot
Calculates signal change relative to selected baseline shown as mean or mean ± 5 (average over +5 and -5 time frames).
Calculates "DElay" time, defined as time between treatment t0 and response. Response is defined as the timepoint at which the slope of the signal exceeds the slope of the baseline. Δ indicates signal change at this time point.
Calculates "Attack" time, defined as maximum mean value closest to the initial maximum slope value. In brackets: t(Attack)-t(DElay). Δmax indicates maximum signal change at this time point.
Calculates "Decay" time, defined as timepoint at which the slope reaches a minimum and remains low. In brackets: t(Decay)-t(Attack). Δsustain indicates signal change sustain level.
Calculations of DElay, Attack and Decay times depend on the selected slope calculated from ± 5; ± 10; ± 15 or ± 20 time frames.
Blue vertical line in the graph indicates current time point. Left mouse click over region to zoom in. Double mouse click to zoom out.
"Setup" allows for editing and visualizing graph and time parameters. X start, baseline recording [min];  X step, time frame duration [min].
Note that X start and X step parameters are used for calculating signal change, and for normalized vertical profile calculations.
"Results" opens a table showing time (x), mean and slope values. Click on column(s) to copy into clipboard.
Right click on graph enables export of results tables and saving of graph as PNG, JPG, BMP and SVG files; EPS and PDF is not supported.

Vertical Profile
Generates vertical profile response heat maps. Average of X (all pixels in one Y row) over time. 
(raw): Vertical profile of entire image stack.
(raw w/ tip): Vertical profile over a defined Y region (pixels) starting from the root tip, defined by "Tip Detection Settings".
"Normalize Vertical Profile" requires an open vertical profile from which the values of each Y pixel row are normalized (signal change) according to the settings defined in the "DEAD Plot Setup".
"Slope" extracts the slope values of each Y (pixel) row within a vertical profile. Generated slope map data look better after Gaussian Blur (1).

Correlation Plot
Requires two open Vertical Profile (stacks) synchronized via "Analyze/Tools/Synchronize Windows".
Calculates "Pearsons", "Kendalls" and "Spearmans" correlation over selected ROI with indicated length and time parameters. Data can be extracted and exported as mentioned before.

Root Tip Detector
For each image-stack frame the "Root Tip Detector" is adding a ROI into the "ROI Manager" starting at the root tip using the parameters set in "Tip Detection Settings".
The "trail +/- 10" averages the root growth over 20 image frames.
The growth rate is calculated from selected and indicated length and time. Use mouse to zoom in and out. Data can be extracted and exported as mentioned before.

Crop to Tip ROIs
Uses the ROIs generated by the "Root Tip Detector" and crops each image frame accordingly to an image stack with the root tip at the bottom.
If the Root Tip ROIs have not been generated yet, it will run the "Root Tip Detector" to generate them first. 

Tip Detection Settings
"Tip ROI Image Height" defines the ROI height for "Crop To Tip ROIs" and "Vertical Profile (raw w/ tip)"
"Not NaN Pixel Count" defines how many pixels with a value need to be found in a Y row in order to define that this is the root tip.
"Tip Offset" defines how many pixels below the detected root tip the ROI will be set.

Note, if multiple GEFIs have been acquired at the same time, define one GEFI image stack as "Master" for the "Root Tip Detection" and use the same ROIs written in the "ROI Manager" for "Vertical Profile (raw w/ tip)" and "Crop to Tip ROIs".

Good Luck with the experiments.
