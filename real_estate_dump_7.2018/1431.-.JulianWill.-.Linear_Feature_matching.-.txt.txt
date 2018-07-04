****************************Description***********************************
* This repository contains python scripts for the matching of two linear *
* feature shape-files.							 *
* 								         *
* The two datasets are matched for defined areas. The script divides	 *
* the area(s) into 1 square kilometre squares and matches the datasets   *
* for each square separately. The output of the script is a matched 	 *
* shape-file covering the extent of each square for each dataset.	 *
* 									 *
* For the best matching results, the two linear feature datasets should  *
* have similar scale representation and should be topological structured.*
* 									 *
* The scripts are original developed to match OpenStreetMap road network *
* data with Real-Estate data of Lantmäteriet	 			 *
* (Swedish National Mapping Agency) for a quality assessment of OSM. 	 *
* It has not been jet tested with other datasets, but it should          *
* generally work with any linear feature datasets.			 *
* The script uses the functionality of QGIS (http://qgis.org/en/site/)	 *
* which is an open source geographic information system			 *
*   									 *
***************************How to use*************************************
* Requires: Installation of QGIS (tested on version 2.2)		 *
* 	    Installation of Python (2.7~)				 *
*    	    Installation of python package Shapely			 *
*    	    Installation of python package Natural Language Toolkit  	 *
*   									 *
* Input data: two linear feature dataset (the one with a higher 	 *
*                 documented quality is called LM in scripts, the other  *
*                 one OSM)						 *
*  	      one polygon shape-file with defines the area(s) in which 	 *
* 		  the data should be matched. (Area(s) have to be bigger *
		  than 1km²)						 *
*   									 *
* Preparation: add required paths to 'config_file_matching.ini'          *
*   									 *
* Execution: execute 'Linear_feature_matching.py' 	   		 *
	    (in tests it is executed from the python console within QGIS)*
*   								         *
* Output: the output files of the OSM dataset and LM dataset contain     *
*	  a attribute called "LM_match" respective "OSM_match" which     *
* 	  contain the id ("id_clip") of matching feature(s)		 *
*   									 *	   
***************************License****************************************
*                                                                        *
* This program is free software; you can redistribute it and/or modify   *
* it under the terms of the GNU General Public License as published by   *
* the Free Software Foundation; either version 2 of the License, or      *
* (at your option) any later version.                                    *
*   									 *
* It is distributed in the hope that it will be useful, but WITHOUT ANY  *
* WARRANTY; without even the implied warranty of MERCHANTABILITY or      *
* FITNESS FOR A PARTICULAR PURPOSE. See the GNU General Public License   *
* for more details.                                                      *
*   									 *
* For a copy of the GNU General Public License see                       *
* "http://www.gnu.org/licenses/gpl-3.0.en.html".                         *
*   									 *
* The latest source for this software can be accessed at                 *
* "https://github.com/JulianWill/Linear_Feature_matching/"		 *
*   				 					 *
* Copyright © 2014 Julian Will						 *
*   									 *
**************************************************************************
* Contact the author: Julian Will. Email: julianwill88@web.de		 *
*   									 *
* For a detailed explanation of the used methodology see:	 	 *
* Development of an automated matching algorithm to  assess the quality  *
* of the OpenStreetMap road network - A case study in Göteborg, Sweden 	 *
* (Master thesis at Lund University, Julian Will)			 *
**************************************************************************