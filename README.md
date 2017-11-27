# owf-data-co-ditch-and-reservoir-companies #

This repository contains the [Open Water Foundation (OWF)](http://openwaterfoundation.org) dataset for Colorado ditch and reservoir companies (irrigation water supply companies).
This is a foundational dataset that provides unique identifiers and other data for ditch and reservoir companies.
The identifiers can be used to link other datasets, such as agricultural ditches and municipal water providers.
OWF has created and is maintaining this dataset to facilitate work on various data analysis and visualization projects in Colorado.

## Repository Contents ##

The repository contains the following:

```text
.gitignore                      		Git configuration file to ignore files that should not be committed to the repository.
.gitattributes                  		Git configuration file indicate repository configuration, in particular handling of line-ending and binary files.
build/						Folder used by TSTool to create products for publication.
data/                           		Folder containing data files.
  Colorado-Ditch-Reservoir-Companies.xlsx     	Simple Excel file containing core data.
  Colorado-Ditch-Reservoir-Companies.csv      	The Excel file contents from the DitchReservoirCompany worksheet converted to a csv file, useful for automated processing.
data-orig/					Folder containing original data files downloaded from agency websites.
  Business-Entities-in-Colorado.csv		The data file containing original data download from the Colorado Information Marketplace containing Business Entity IDs. 
  DARCA-Members.csv  				The data file containing the list of Ditch and Reservoir Company Alliance (DARCA) members copied from DARCA's website.
  doc/
  ?                             		Additional documentation for the dataset.
analysis/                         		TSTool software command files to process data into useful forms.
  Process-xlsx-to-csv.TSTool			TSTool command file that processes the core dataset from .xlsx to .csv.
  README.md                     		Explanation of TSTool command files used to process the core data into other products.
```

### Colorado-Ditch-Reservoir-Companies.xlsx Contents ###

The core Excel workbook that serves as the master data contains the following data columns within the **DitchReservoirCompany** worksheet.

* **DitchReservoirCompanyName** -- name of the ditch/reservoir company
* **OWF_ID** -- unique text identifier created by OWF; may be used in the future to link other datasets
* **OWF_ID_Flag** --  data status of OWF_ID values; see more detail below
* **BusinessEntity_ID** -- state-assigned identification number for a business entity, from the [Colorado Information Marketplace](https://data.colorado.gov/Business/Business-Entities-in-Colorado/4ykn-tg5h/data), to link state datasets
* **BusinessEntity_ID_Flag** -- data status of BusinessEntity_ID values; see more detail below
* **DARCAMember** -- indication of whether the company is a member of the Ditch and Reservoir Company Alliance
* **EntityStartDate** -- formation date of the company
* **EntityStartDate_Flag** -- data status of EntityStartDate values; see more detail below
* **EntityEndDate** --  dissolution date of company, if applicable
* **EntityEndDate_Flag** -- data status of EntityEndDate values; see more detail below
* **Ditch_WDID_CSV** -- WDIDs (identifiers for structures such as ditches and reservoirs) of ditches the company is associated with, in comma-separated format (CSV) **TO BE ADDED**
* **Ditch_WDID_CSV_Flag** -- data status of Ditch_WDID_CSV values; see more detail below **TO BE ADDED**
* **Reservoir_WDID_CSV** -- WDIDs (identifiers for structures such as ditches and reservoirs) of reservoirs the company is associated with, in comma-separated format (CSV)  **TO BE ADDED**
* **Reservoir_WDID_CSV_Flag** -- data status of Reservoir_WDID_CSV values; see more detail below  **TO BE ADDED**
* **Latitude** -- latitude of company's point location in decimal degrees
* **Longitude** -- longitude of company's point location in decimal degrees
* **Lat_Long_Flag** -- indication of how latitude and longitude were determined
* **Municipality** -- municipality in which the ditch/reservoir company is located
* **Municipality_Flag** -- data status of Municipality values; see more detail below
* **IBCC_Basin** -- Interbasin Compact Committee (IBCC) basin in which the ditch company is located
* **IBCC_Basin_Flag** -- indication of how the basin was determined
* **Website** -- website URL of the ditch/reservoir company  **TO BE ADDED**
* **Website_Flag** -- data status of Website values; see more detail below  **TO BE ADDED**
* **Comment** -- any other information about the ditch/reservoir company

For many data columns, a second column of the same name with the word "Flag" added to the column name is present.  These columns are an indication of data status as it relates to missing data.  The following conventions are used:
* G = Value is known/good.  
* g = Value is estimated (but good).  The associated cell is also highlighted in yellow.
* N = Value is not applicable for the provider and a blank cell is expected.
* M = Value is known to be missing in original source and therefore a blank cell indicates that a value cannot be provided.
* m = Value is estimated to be missing.  The associated cell is also highlighted in gray.
* z = Value is unable to be confirmed.  A value is possible but cannot be confirmed one way or the other.  The associated cell is also highlighted in orange.
* x = OWF has not made an attempt to populate the cell at this time.  The value is missing because OWF has not attempted to find the value.  The associated cell is also highlighted in black.

Column names are taken from original sources if possible.  For clarity and attribution, agency abbreviations may be added to the original column name.  Column name length is not restricted, therefore, some data representations such as Esri shapefiles may contain truncated column names.  In such cases, alternative formats such as GeoJSON are recommended.

Descriptions of identifiers are also provided in the **Notes** worksheet within the workbook.  This worksheet also details how the original data were downloaded and where to find those files.


Other worksheets within the workbook contain the following:

* **ChangeLog** worksheet indicates any changes made to the dataset, the date they occurred and who made the changes.

* **Metadata_DitchReservoirCompany** worksheet serves as the metadata for data columns in the **DitchReservoirCompany** worksheet.


## Attribution ##

The data sources for this dataset are listed below.

* The Business Entity ID is from the [Colorado Information Marketplace](https://data.colorado.gov/Business/Business-Entities-in-Colorado/4ykn-tg5h/data) and is a state-assigned identification number.  OWF filtered the dataset based on the words "ditch", "irrigation" and "reservoir".  The dataset was also the source of the EntityStartDate and EntityEndDate data.
* Over half of the companies have a physical address listed in the dataset, but not latitude/longitude coordinates.  To obtain coordinate data, the dataset was opened in [Google Sheets](https://www.google.com/sheets/about/).  An add-on named Geocode by Awesome Table can take a physical address and convert it to coordinates, as long as the street address, city, state and zip code are provided.
* The IBCC_Basin column indicates which [Interbasin Compact Committee](http://cwcb.state.co.us/about-us/about-the-ibcc-brts/Pages/main.aspx) basin the company is located in.  To fill this column, OWF first saved the DitchReservoirCompany worksheet in csv format and then opened the file in QGIS to create a point layer of ditch companies.  Then a GIS shapefile of the IBCC basins was overlayed onto the point layer.  A shapefile of the basins can be found within the [Colorado Water Conservation Board (CWCB)'s Data Viewer](https://www.coloradodnr.info/h5v/Index.html?viewer=cwcbviewer).  The IBCC Basin layer is within the Admin Boundary category.  All of the ditch companies within a specific basin were then selected and labeled with the basin name.
* The [Ditch and Reservoir Company Alliance](http://www.darca.org/) maintains a list of members on its website.  The list was directly copied from the website and pasted into an Excel spreadsheet.
* Website URLs were found by manually searching for company websites.


## Data Workflow ##

This dataset was first created by downloading the "Business Entities in Colorado" dataset from the Colorado Information Marketplace.  Data were filtered to only include entities with the words "ditch", "irrigation" and "reservoir" in the entity name.
Further filtering was then required to eliminate entities that were landscaping companies "i.e., "X Irrigation and Landscaping Company".  Each entity has a state-assigned identification number, which OWF is referring to as BusinessEntity_ID.
Other data columns that come from this dataset include EntityStartDate, EntityEndDate and Municipality.  OWF created a unique text identifier (OWF_ID) that may be used in the future to link additional datasets.  OWF manually cross-referenced DitchReservoirCompanyName with the DARCA-Members.csv dataset.  
From here, the general workflow is as follows:
1. Data flags are created for many of the data columns that indicate data status as described above.
2. The data are formatted as a table to allow for data filtering.
3. The dataset is saved in .xlsx format.
4. The xlsx-formatted file is opened in TSTool and a short command file (Process-xlsx-to-csv.TSTool) converts the dataset into CSV format.
5. The xlsx-formatted file is opened in TSTool and a short command file converts the dataset into geoJSON format.  This step is optional and applicable for datasets in which a map will be created or if further processing will occur in GIS application such as QGIS.


## How to Use the Data ##

The Colorado Ditch and Reservoir Companies dataset provides a statewide list of ditch and reservoir companies.  There are unique identifiers for each company and the dataset allows cross-referencing the identifiers
so that other datasets can be joined.  For example, the [Colorado Municipal Water Providers dataset](owf-data-co-municipal-water-providers) uses municipal water provider
identifiers and can be used to link to this dataset to provide information about water rental programs between ditch companies and water providers.

The Excel or csv files can be used as tabular datasets as is, to create filtered lists or to link to other datasets.  Data-processing software such as TSTool can be used to link this dataset to other datasets.  Datasets can be used within GIS software to create maps.

The format and contents of the dataset will change over time.  It is recommended to save a copy of the dataset.

## License ##

The license is being determined.  All the data are public so there are not really any restrictions on use.

## Contributing ##

The Open Water Foundation is adding value by cross-referencing datasets.
If you use the dataset and have comments, please contact the maintainers and/or use the GitHub issues to provide feedback.

## Maintainers ##

Kristin Swaim (@kswaim, kristin.swaim@openwaterfoundation.org) is the primary maintainer at the Open Water Foundation.

Steve Malers (@smalers, steve.malers@openwaterfoundation.org) is the secondary contact.

## Contributors ##

None yet, other than OWF staff.
