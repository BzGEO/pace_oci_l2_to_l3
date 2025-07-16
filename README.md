# Tutorial: Processing PACE OCI level-2 surface reflectance data to level-3

[![DOI](https://zenodo.org/badge/DOI/10.5281/zenodo.15993990.svg)](https://doi.org/10.5281/zenodo.15993990)

Tutorial for using NASA's SeaDAS to convert PACE OCI L2 surface reflectance to L3 data

## Description: Why do I need to review this tutorial?
**Scenario:** *You are a regular GIS user, with a Windows computer. You want to be able to get PACE OCI surface reflectance data at its original 1.2 km spatial resolution, in a GIS-ready format to be able to view the data in [ArcGIS](https://www.esri.com/en-us/arcgis/products/arcgis-desktop/overview) or [QGIS](https://qgis.org/).*

## Required software

To be able to execute the steps of this tutorial, you will need to install [Docker](https://www.docker.com/products/docker-desktop/) and [SeaDAS](https://seadas.gsfc.nasa.gov/downloads/).

## Workflow

*Slides of the walk-through of these steps are available in [GitHub](https://github.com/BzGEO/pace_oci_l2_to_l3/blob/main/nasa_pace_oci_processing_seadas_2025-07-16.pdf) or as [Google Slides](https://bit.ly/pace_oci_seadas).*

![](https://github.com/BzGEO/pace_oci_l2_to_l3/blob/main/_graphics/pace_oci_seadas_export.png)

1. Install Docker if you don't already have it installed: https://www.docker.com/products/docker-desktop/.
2. Install NASA SeaDAS if you don't already have it installed: https://seadas.gsfc.nasa.gov/downloads/.
3. Use the instructions provided by NASA to properly configure the SeaDAS dockerized container: https://seadas.gsfc.nasa.gov/client_server/.
4. Download PACE OCI level-2 surface reflectance data from NASA Earth Data: https://search.earthdata.nasa.gov/search?q=surface%20reflectance&fi=OCI&as[instrument][0]=OCI.
    * You can choose either "Level-2 Regional Surface Reflectance Data, version 3.0" [data](https://search.earthdata.nasa.gov/search/granules?p=C3385050059-OB_CLOUD&pg[0][v]=f&pg[0][gsk]=-start_date&q=surface%20reflectance&fi=OCI&as[instrument][0]=OCI&tl=1731145542.333!4!!) or "" [data](https://search.earthdata.nasa.gov/search/granules?p=C3385050055-OB_CLOUD&pg[0][v]=f&pg[0][gsk]=-start_date&q=surface%20reflectance&fi=OCI&as[instrument][0]=OCI&tl=1731145584.466!4!!).
    * Data are in NetCDF (.NC) format, which SeaDAS and other software applications can read fairly easily, but which are not considered *GIS ready.*
    * To download data from the NASA Earth Data website, you will need to [login](https://urs.earthdata.nasa.gov/) using your credentials. If you do not have credentials for NASA Earth Data, you can [register](https://urs.earthdata.nasa.gov/users/new) for free.
5. You will need to open the NetCDF file, for instance, using *File -> Import -> Generic Formats -> NetCDF (Generic).*
6. Since you have properly configured the SeaDAS processor using the instructions in step 3 above, next navigate to *SeaDAS-Toolbox -> Install/Update SeaDAS Processors.*
7. In the window that opens that says "Configure OCSSW Location" at the top, change "OCSSW Location" from "virtual machine" to "docker."
8. A dialog will show up saying "Running install_ocssw" and indicating how many modules are being installed. After that is successful, there will be a message saying "Program execution completed!"
9. Make sure that you have the latest version selected under "OCSSW Tag" (e.g., V2025.1), and that you have the checkbox for OCI selected under "Missions." Then click the "Run" button.
10. Navigate to *SeaDAS-Toolbox -> multilevel_processor.*
11. Since we need to convert from Level-2 to Level-3 data, select the **l2gen** option, but also **l2extract**, **l2brsgen**, **l2bin**, and **l3mapgen**. Ignore whatever errors might pop up. Wait about 5 minutes, and then shut down SeaDAS.
12. Reopen SeaDAS and navigate to *File -> Reopen Product* and select the name of the last file you had opened in SeaDAS. This will reopen the file you had been processing, and you will notice that it will now have an "rhos" folder added under the "Bands" folder. That "rhos" folder will contain the names of the 122 spectral bands that have been created.
13. The output data will not be orthorectified, so you will still need to project the data, using *Raster -> Geometric -> Reprojection*. I recommend just using the default values, which will keep the data in WGS 1984 ("lat / long").
14. After that processing, the data can be exported to GeoTIF, per *File -> Export -> GeoTIFF / BigTIFF.*

## Notes
If you would like to *skip* processing the PACE OCI data on your desktop system and just work with the data in the cloud, check out the PACE OCI toolkit for [Google Earth Engine](https://code.earthengine.google.com/) (GEE): https://github.com/BzGEO/pace_oci_toolkit.

## Acknowledgements
This work is being led by researchers from the [Lab for Applied Science](https://www.uah.edu/essc/laboratory-for-applied-science) of the [Earth System Science Center](https://www.uah.edu/essc) of the [University of Alabama in Huntsville](https://www.uah.edu/) and has been supported by the [NASA](https://www.nasa.gov) Earth Action / NASA [Marshall Space Flight Center](https://www.nasa.gov/marshall/). This work is being done in the context of an [Early Adopters project](https://pace.oceansciences.org/people_ea.htm?id=127) for PACE. The PACE Mission Applications Lead, Dr. Morgaine McKibben (NASA / SSAI), is acknowledged for her support, as are Skye Caplan (NASA / SSAI) of the PACE mission, and Dr. K. Fred Huemmrich of the PACE Science & Applications Team (NASA / UMBC). Kudos are also due to [Kelsey Herndon](https://github.com/herndk1) (NASA / UAH), [Prof. Rob Griffin](https://github.com/r-griffin), [Dr. Africa-Flores-Anderson](https://github.com/africaf) (NASA), [Eric Anderson](https://github.com/andersoner) (NASA), Dr. Kevin Horn (NASA), Dr. Ashutosh Limaye (NASA), and Dan Irwin (NASA) of NASA MSFC.

## Contact information

If you have any questions, feel free to contact Emil Cherrington by :envelope_with_arrow: email: **emil.cherrington [at] uah.edu**.
