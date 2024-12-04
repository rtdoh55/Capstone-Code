# Capstone-Code
# Context:
Neutrino particles are subatomic particles without any charge that are very hard to detect and are naturally produced. By studying the neutrino, we can gain insight into a type of physics that goes beyond the standard model, giving significance to these seemingly insignificant particles. These neutrinos occur through a beta decay which is where 2 neutrons decay and produce 2 protons, 2 electrons, and 2 neutrinos. Using High purity germanium detectors scientists were able to measure the charge being released from this beta decay. We're interested in a double beta decay (a hypothesized decay), which is where a neutrino decays into 2 protons, 2 electrons, and no neutrinos which would indicate that neutrinos are their own antiparticles. This is done by measuring the charge through a time series. This would allow us to see if there are charge deposits in one or multiple sites. Originially the standard way of discovering multi-site or single site events was done through an arduous physics process. Our job is to using a machine learning model to predict features that would allow us to differentiate between single and multi site events. This would save time and help the forward progression of the discovery of these particles.
# Data:
Example data is included in the data folder and the original files were downloaded from https://zenodo.org/records/8257027
# Objective:
The main objective of my code was to create functions that could be universally used for any waveform in this format to extract these parameters. These parameters would be used in our machine learning model to help determine which of these events are multi-site and which are single-site events.
# Prerequisites:
```bash
pip install -r requirements.txt
```
___
## Four parameters were extracted: 
- **Time Drift 10**
- **Rising Edge slope**
- **Inflection points**
- **LQ80 area growth rate**
### Time Drift 10
This parameter is used to find the time in the waveform where the waveform reaches 10 percent of its peak. This is important because relative to its peak, the time it takes for the waveform to reach 10 percent of its value can determine whether it is a multi-site or a single site event. This was done by first finding the max of the waveform (the peak) and multiplying it by .10 to find the value at 10% of the peak. Then if we subtract this number from the numpy array and take the absolute value and find the argmin, we get the value closest to 10% of the waveform peak.
### Rising Edge Slope
This parameter is used to find the slope of the rising edge of the energy. This is important because in multi-site events there is a smaller slope because of the second deposit of energy. This was done through fitting a line to the waveform and extracting the slope as a parameter.
### Inflection Points
This parameter is used to find the number of inflection points in our data. This was done using numpy gradient twice to find the second derivative Then I used np.sign to find the signs of the second derivative. This is because when the second derivative changes sign it is an inflection point. So I used np.diff to subtract the neighboring values and find where the values were either 2 or -2 and these would be the inflection points. 
### Area Growth Rate
The Area growth rate is used to find the area growth from after 80% of the peak energy subtracted from the area growth if the energy remained at the peak. This was done by multiplying the amount of data points from the 80% of the peak to the end by the peak value and then adding add the values from the peak to the tail. Then subtracting the peak area from the area of the growth from the 80% of the value.
___
# Parameter Extraction
### Objective:
The main objective of this was to gather all the parameter extraction codes from all the group members and use them in a couple of lines to extract the parameters from each of our data files. This wsa then stored in a dataframe and uploaded to a csv file that could be used for training our models.
### Process and Code
The process used to extract all the parameters from each waveform was to use list comprehension and loops to apply each parameter extraction to each waveform. This would allow us to extract each pararmeter into a numpy array and then add the numpy array to a dataframe column
