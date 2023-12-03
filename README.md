# FRAP-Calculation
FRAP investigates cell kinetics using photobleaching. The software streamlines data analysis with a user-friendly GUI, accepting CSV and CZI files, and applies an algorithm based on scientific equations to output recovery rates and graphs.


**Background on FRAP**
FRAP stands for fluorescence recovery after photobleaching. As the name indicates, it is a method where a region of interest within the cell is exposed to high intensity laser for a short amount of time. The laser exposure is then removed to allow the region to recover. This is a widely used method to study the kinetics and diffusion within the cell. Typically, the cell membrane lipids are marked with a fluorescence tag, where the intensity of the fluorescence in the pre-bleach, bleach, and post bleach stages are captured by the confocal microscope and collected. As shown in the figure below, lipids and molecules move around within the cell which results in recovery of the area that has been photobleached.

 			![image](https://github.com/laylabitar/FRAP-Calculation/assets/79585453/d9d6935d-a845-40e8-ac33-7956e65e97e3)

				
    
    
   								 Figure 1. FRAP Process (carmen, 2012)



**Purpose of Software**
The aim of this project is to introduce a facilitated and a sped-up method to analyze data generated from photobleaching using a confocal microscope. The program will run a user-friendly GUI that will allow the user to input data and output graphs along with other results that are significant for analyzing fluorescence recovery photobleaching. It will provide the user an option to execute and export certain calculations and graphs with a click of only a few buttons. The software structure will be built based upon object-oriented programming (Matlab App Designer). This will eliminate code redundancy for different data input types. The program will initially accept two types of files: CSV and CZI. For the CZI, there is an already existing bio format plugin that will be incorporated within the program. The plugin allows to read and write microscope image files.

**Requirement’s list**
_Non-functional requirements_
•	A user-friendly GUI shall have a response of no more than 5 seconds to user input or interaction.
•	Algorithm shall output a recovery rate equal or more than zero.
•	Program shall detect pixel intensity ranging from zero (black) to 255(white).

_Functional requirements_
•	GUI shall be able to accept data input in the following file formats: .csv, czi
•	The user shall be able to manually select ROI
•	The program shall analyze the pixel intensity from the manually selected ROI
•	Algorithm shall output percent recovery 
•	Algorithm shall provide the best line of fit of the recovery curve along with the R2 value.
•	Program should be able to provide an option to save data and figures into the following file formats: csv,png,


**System Diagram**

			![image](https://github.com/laylabitar/FRAP-Calculation/assets/79585453/94fa6995-d587-4f87-90ec-c88dfda3b4c9)

 
								Figure 2. Flowchart of the Program


**Algorithm**		
The algorithm is created using equations adapted from the paper “Fluorescence recovery after photobleaching reveals regulation and distribution of connexin36 gap junction coupling within mouse islets of Langerhans” 1

		![image](https://github.com/laylabitar/FRAP-Calculation/assets/79585453/509bcb0a-581d-4f23-ad0d-d18ff86dbf8f)
			
				Equation 1: % Recovery Equation (Farnsworth, Nikki L et al,2014)
			
		![image](https://github.com/laylabitar/FRAP-Calculation/assets/79585453/4ef59205-48be-4add-979a-8a7f1dc9f6ac)
			
			 
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
 



GUI Concept Drawing
The GUI has two tabs. One for each data input type. Design of each tab is shown in the below figures.

![image](https://github.com/laylabitar/FRAP-Calculation/assets/79585453/ca978abb-2c08-4d58-8f50-f63044b78758)

  
					Figure 3a. GUI Design

     
![image](https://github.com/laylabitar/FRAP-Calculation/assets/79585453/6f40b3f1-6ecc-4c72-87e5-ee7897ff40ae)

				Figure 3b. GUI Design with Image Processing


