# data-orig #

The `data-orig` folder contains original data files downloaded from various websites.  The contents of each file are described below, as well as the methodology used to obtain the data and mapping to the joined dataset.

## Business-Entities-in-Colorado.csv ##

This file contains original data downloaded from the [Business Entities in Colorado](https://data.colorado.gov/Business/Business-Entities-in-Colorado/4ykn-tg5h/data) dataset available on the [Colorado Information Marketplace (CIM)](https://data.colorado.gov/) that contains business entity IDs.  The business entity ID is useful for linking State datasets.  The dataset was filtered to only include entities with the words "ditch" in the entity name.  The dataset was then exported as a CSV file.  The same process was used with the words "irrigation" and "reservoir" to create three separate CSV files. 
The three files were then opened in Excel and compiled into a single dataset.  The dataset then needed to be further filtered because it was assumed that entities with names such as "X Irrigation and Landscaping Company" were not ditch companies.  OWF decided to include entities with names that contained "Irrigation Company" or "Irrigating Company", but deleted entities with names that only contained "Irrigation" because it was also assumed that these entities are associated with landscaping/sprinklers, rather than ditches.  The file was then saved in CSV format.
  
The file contains the following data columns.

* **entityid** -- state-assigned identification number for a business entity; integer format; is the **BusinessEntity_ID** column in the main dataset
* **entityname** -- name of the ditch or reservoir company; text format; is the **DitchReservoirCompanyName** column in the main dataset
* **principaladdress1** -- street address of the company; text format; not used in main dataset but used to find latitude and longitudes coordinates
* **principaladdress2** -- alternate street address of the company; text format; not used in the main dataset
* **principalcity** -- city where the company is located; text format;  not used in main dataset but used to find latitude and longitudes coordinates
* **principalstate** -- state where the company is located; text format;  not used in main dataset but used to find latitude and longitudes coordinates
* **principalzipcode** -- zip code where the company is located; integer format;  not used in main dataset but used to find latitude and longitudes coordinates
* **principalcountry** -- country where the company is located; text format;  not used in main dataset
* **mailingaddress1** -- mailing street address of the company; text format; not used in main dataset but used to find latitude and longitudes coordinates if principal address is missing
* **mailingaddress2** -- alternate mailing street address of the company; text format; not used in the main dataset
* **mailingcity** -- mailing city where the company is located; text format;  not used in main dataset but used to find latitude and longitudes coordinates if principal city is missing
* **mailingstate** -- mailing state where the company is located; text format;  not used in main dataset but used to find latitude and longitudes coordinates if principal state is missing
* **mailingzipcode** -- mailing zip code where the company is located; integer format;  not used in main dataset but used to find latitude and longitudes coordinates if principal zip code is missing
* **mailingcountry** -- mailing country where the company is located; text format;  not used in main dataset
* **entitystatus** -- indication of whether the company still exists, is in good standing, is delinquent or dissolved; text format; not used in main dataset
* **jurisdictonofformation** -- jurisdiction of formation(?); empty column; not used in main dataset
* **entitytypeverbatim** -- type of entity, such as Ditch Company, Nonprofit Corporation, Limited Liability Company, etc.; text format; not used in main dataset
* **entitytype** -- abbreviation of type of entity, such as DT for Ditch Company; text format; not used in main dataset
* **agentfirstname** -- first name of registered agent, who serves as the contact for the company; text format; not used in main dataset
* **agentmiddlename** -- middle name of registered agent, who serves as the contact for the company; text format; not used in main dataset
* **agentlastname** -- last name of registered agent, who serves as the contact for the company; text format; not used in main dataset
* **agentsuffix** -- optional suffix to name of registered agent, who serves as the contact for the company; text format; not used in main dataset
* **agentorganizationname** -- registered agent's organization name, presumably only if different from entityname; text format; not used in main dataset
* **agentprincipaladdress1** -- street address of the agent; text format; not used in main dataset
* **agentprincipaladdress2** -- alternate street address of the agent; text format; not used in the main dataset
* **agentprincipalcity** -- city where the agent is located; text format;  not used in main dataset
* **agentprincipalstate** -- state where the agent is located; text format;  not used in main dataset
* **agentprincipalzipcode** -- zip code where the agent is located; integer format;  not used in main dataset
* **agentprincipalcountry** -- country where the agent is located; text format;  not used in main dataset
* **agentmailingaddress1** -- mailing street address of the agent; text format; not used in main dataset
* **agentmailingaddress2** -- alternate mailing street address of the agent; text format; not used in the main dataset
* **agentmailingcity** -- mailing city where the agent is located; text format;  not used in main dataset
* **agentmailingstate** -- mailing state where the agent is located; text format;  not used in main dataset
* **agentmailingzipcode** -- mailing zip code where the agent is located; integer format;  not used in main dataset
* **agentmailingcountry** -- mailing country where the agent is located; text format;  not used in main dataset
* **entityformdate** -- formation date of the entity; date format; is the **EntityStartDate** column in the main dataset

If then entity has dissolved, then this is stated within the "entityname" column.  The dissolution date was removed from the "entityname" column and copied into the **EntityEndDate** column.


## DARCA-Members.csv ##

This file is a list of ditch and reservoir companies that are members of the [Ditch and Reservoir Company Alliance](https://www.darca.org/).  DARCA maintains a [list](https://www.darca.org/2017-darca-members.html) of members on its website.  The list was copied directly from the website and pasted into Excel.  The list was then saved in CSV format.

The file contains the following data columns.

* **DARCAMemberName** -- name of the ditch or reservoir company; text format; manually cross-referenced to the **DitchReservoirCompanyName** column in the main dataset
* **Municipality** -- municipality where the company is located; text format; not used in main dataset but could be cross-checked with main dataset for quality control

Once the "DARCAMemberName" column was cross-referenced to the **DitchReservoirCompanyName** column in the main dataset, then the "DARCAMemberName" column was pasted into the main dataset and the column renamed to **DARCAMember**.  Then the names were substituted with "Y" (Yes) to indicate membership.




