# FRAP-Calculation
FRAP investigates cell kinetics using photobleaching. The software streamlines data analysis with a user-friendly GUI, accepting CSV and CZI files, and applies an algorithm based on scientific equations to output recovery rates and graphs.


Layla Bitar
BIOE 4064				Final Project App Description		12/16/2021![image](https://github.com/laylabitar/FRAP-Calculation/assets/79585453/ace2e386-06d0-40fd-a9e2-e60fd1f60fa5)


Background on FRAP
FRAP stands for fluorescence recovery after photobleaching. As the name indicates, it is a method where a region of interest within the cell is exposed to high intensity laser for a short amount of time. The laser exposure is then removed to allow the region to recover. This is a widely used method to study the kinetics and diffusion within the cell. Typically, the cell membrane lipids are marked with a fluorescence tag, where the intensity of the fluorescence in the pre-bleach, bleach, and post bleach stages are captured by the confocal microscope and collected. As shown in the figure below, lipids and molecules move around within the cell which results in recovery of the area that has been photobleached.

 
				Figure 1. FRAP Process (carmen, 2012)



Purpose of Software
The aim of this project is to introduce a facilitated and a sped-up method to analyze data generated from photobleaching using a confocal microscope. The program will run a user-friendly GUI that will allow the user to input data and output graphs along with other results that are significant for analyzing fluorescence recovery photobleaching. It will provide the user an option to execute and export certain calculations and graphs with a click of only a few buttons. The software structure will be built based upon object-oriented programming (Matlab App Designer). This will eliminate code redundancy for different data input types. The program will initially accept two types of files: CSV and CZI. For the CZI, there is an already existing bio format plugin that will be incorporated within the program. The plugin allows to read and write microscope image files.

Requirement’s list
Non-functional requirements
•	A user-friendly GUI shall have a response of no more than 5 seconds to user input or interaction.
•	Algorithm shall output a recovery rate equal or more than zero.
•	Program shall detect pixel intensity ranging from zero (black) to 255(white).

Functional requirements
•	GUI shall be able to accept data input in the following file formats: .csv, czi
•	The user shall be able to manually select ROI
•	The program shall analyze the pixel intensity from the manually selected ROI
•	Algorithm shall output percent recovery 
•	Algorithm shall provide the best line of fit of the recovery curve along with the R2 value.
•	Program should be able to provide an option to save data and figures into the following file formats: csv,png,


System Diagram
 
				Figure 2. Flowchart of the Program


Algorithm		
The algorithm is created using equations adapted from the paper “Fluorescence recovery after photobleaching reveals regulation and distribution of connexin36 gap junction coupling within mouse islets of Langerhans” 1
 
Equation 1: % Recovery Equation (Farnsworth, Nikki L et al,2014)

 
Equation 2: Recovery Rate Equation (Farnsworth, Nikki L et al,2014)
In order to read the czi file, the MATLAB bio format folder is downloaded from the following link: https://docs.openmicroscopy.org/bio-formats/6.3.1/developers/matlab-dev.html
Once file is downloaded, it is added to the MATLAB path. The code starts by using the bfopen function to open the czi file. The function returns an n-by-4 array where n is the number of series in the dataset. The first series is used to extract the pixel data for the image. The following code is to initialize the opening of the czi file.
% find the number of series
data = bfopen(file);
size = height(data);
no_series = size;
% find the number of planes
planes = data{1,1};
no_planes = length(planes);

% The following loop extracts the pixel intensity for each data series
% data{no_series,1}{plane#,1}
for i=1:no_series
    for k=1:no_planes
        pixelData{i,k} = data{i,1}{k,1};
    end
end
 

Table 1. Data Structure and Function Table
Variables/Functions	Description
data	Variable that saves the data from the uploaded CSV file
post_bleach	Extract from data post-bleach values into a vector
pre_bleach_ave 	Variable that saves the extracted and averaged prebleach values for the specified ROI
percentRecovery	Variable with calculated percent recovery 
recoveryRate	Function that will find the best line of fit for change in recovery
prebleachFrames	The user input for the value of prebleach frames
final_fluorescence	The final mean fluorescence intensity
fluo_change	The average change of fluorescence at each data point
linear_change	The negative log of the fluorescence change to linearize the data

Recovery Time	Read from the excel file
Recovery Rate	The best line of fit for each vector of ROI
R_2	This is the R squared value for the recovery rate
no_planes	Number of planes/frames in the CZI file

no_frame	Number of frames on slider
pixelData	Variable containing the extracted pixel values from the selected ROI
fluo_pixel	Extracted "fluorescence" data from CZI image
ROI_selected	Checks if user has pushed the select ROI button
prebleachCZI	Prebleach frames for CZI
recovery_rate	Function that does the calculations using the algorithm resulting in the recovery rate 
percent_recovery	Function that does the calculations using the algorithm to find the percent recovery


GUI Concept Drawing
The GUI has two tabs. One for each data input type. Design of each tab is shown in the below figures.
  
					Figure 3a. GUI Design

 
				Figure 3b. GUI Design with Image Processing


