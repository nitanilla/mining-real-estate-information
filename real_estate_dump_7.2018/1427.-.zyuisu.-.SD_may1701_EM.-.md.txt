## Synopsis
The product we are to build consists of a web application that allows users to query and view various maps that represent “natural and anthropogenic stresses” (compounds that are added to the ecosystem). Based off of ASCII files provided by Prof. Chaoqun Lu, our goal is to provide an easy and automated way to generate visutally stunning maps of various compounds and create a platform that will allow dynamic loading of said maps onto a 3D space. For more information, visit: http://may1701.sd.ece.iastate.edu/

## Motivation
The Visual Earth Modeling System will allow various policy makers (government, grant societies, etc.) and land managers (real-estate, governmental, farmers, etc.) to visually examine, further analyze, and understand spatial patterns of various gas compounds, water discharges, and nutrient movement. Allowing these stakeholders to further understand the environment will aid them in making decisions in reference to pollution policy, development of land to be used for various crops, grant making, etc.

## Installation
TODO

## IDE Setup
Currently, all developers use Eclipse Neon.2 for contributing to this project. Proper cross-IDE development will require a build tool like Ant to setup consistent formatting rules. Until then, code style preferences can be found in the folder named Code_Style.

This project uses JavaFX 8, which requires Java 1.8 or higher (for Linux users, note that the OpenJDK does not contain the required libraries). Under Eclipse, we also recommend using the following:
  - e(fx)clipse: Can be found via Eclipse update site(s): https://www.eclipse.org/efxclipse/install.html#for-the-lazy
  - Gluon SceneBuilder: A drag and drop tool to layout JavaFX FXML pages.

Additionally, you will require the following tool(s):
  - Tinylog: Available under resources/tinylog-1.1, tinylog.jar must be added under referenced libraries.
  - ArcPy: These libraries are available under an installation of ArcGIS for Server, and are required for the Python scripts to run.

## API Reference
Provided via Javadocs. The simpler Python scripts have their own individual documentation.

## License
This program is free software: you can redistribute it and/or modify it under the terms of the GNU General Public License as published by the Free Software Foundation, either version 3 of the License, or (at your option) any later version.
  This program is distributed in the hope that it will be useful, but WITHOUT ANY WARRANTY; without even the implied warranty of MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the GNU General Public License for more details.
  You should have received a copy of the GNU General Public License along with this program.  If not, see <http://www.gnu.org/licenses/>.
 
