# Capstone-Code
#### Objective:
The main objective of my code was to create functions that could be universally used for any waveform in this format to extract these parameters. These parameters would be used in our machine learning model to help determine which of these events are multi-site and which are single-site events.
___
## Four parameters were extracted, TP10, Rising Edge slope, Inflection points, and LQ80 area growth rate
Descriptions of how these parameters were extracted and their significance are included in our report.
### Time Drift 10
This parameter is used to find the time in the waveform where the waveform reaches 10 percent of its peak. This is important because relative to its peak, the time it takes for the waveform to reach 10 percent of its value can determine whether it is a multi-site or a single site event. This was done by first finding the max of the waveform (the peak) and multiplying it by .10 to find the value at 10% of the peak. Then if we subtract this number from the numpy array and take the absolute value and find the argmin, we get the value closest to 10% of the waveform peak.
### Rising Edge Slope
This parameter is used to find the slope of the rising edge of the energy. This is important because in multi-site events there is a smaller slope because of the second deposit of energy. This was done through fitting a line to the waveform and extracting the slope as a parameter.
### Inflection Points
This parameter is used to find the number of inflection points in our data. This was done using 
