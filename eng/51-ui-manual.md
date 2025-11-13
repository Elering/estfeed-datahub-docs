 # Estfeed user manual

## Contents

<!-- TOC -->

* [Users and rights](#users-and-rights)
  * [Adding a new regular user to your company](#adding-a-new-regular-user-to-your-company)
  * [Modifying roles for a regular user](#modifying-roles-for-a-regular-user)
  * [Creating a new technical user](#creating-a-new-technical-user)
  * [Assigning or modifying roles for an existing technical user](#assigning-or-modifying-roles-for-an-existing-technical-user)
* [Metering points](#metering-points)
  * [Generating a metering point EIC code](#generating-a-metering-point-eic-code)
  * [Creating a new metering point](#creating-a-new-metering-point)
  * [Metering point bulk import](#metering-point-bulk-import)
  * [Modifying a metering point](#modifying-a-metering-point)
  * [Metering point search](#metering-point-search)
  * [Downloading metering point data](#downloading-metering-point-data)
* [Metering data](#metering-data)
  * [Importing metering data](#importing-metering-data)
  * [Download metering data](#download-metering-data)
  * [Metering data search](#metering-data-search)
* [Agreements](#agreements)
  * [Grid agreement](#grid-agreement)
  * [Registering a new customer to the system](#registering-a-new-customer-to-the-system)
  * [Supply agreement](#supply-agreement)
  * [Aggregation agreement](#aggregation-agreement)
  * [Retroactive Addition of Open Supply Agreements](#retroactive-addition-of-open-supply-agreements)
  * [Deleting an Agreement](#deleting-an-agreement)
  * [Modifying an Agreement](#modifying-an-agreement)
  * [Retroactive Modification of Open Supply Agreements](#retroactive-modification-of-open-supply-agreements)
  * [Agreement search](#agreement-search)
  * [Downloading Agreements](#downloading-agreements)
  * [Agreement Coordinations](#agreement-coordinations)
* [Connection requests](#connection-requests)
  * [Sending a connection request](#sending-a-connection-request)
  * [Reading a connection request](#reading-a-connection-request)
  * [Answering to a connection request](#answering-to-a-connection-request)

## Users and rights

After signing the data exchange platform usage agreement, administrator rights will be granted to the manager specified in the agreement. The manager can also assign rights to other employees of their company and create technical users. A technical user is required for using the Estfeed Datahub API interface. For using the web interface, a technical user is not needed.

### Adding a new regular user to your company

- Make sure you are in the correct role
- 'Home' -> 'Users & Roles'
- 'Add user' -> select 'Regular user' as user type
- Add personal code and country of the person, who is being added as a new user
- Choose role or roles for that user (Admin role contains all of the other roles; each user can grant a maximum of the same rights as they have)
- 'Assign'
- Chosen user has been granted the preferred roles

### Modifying roles for a regular user

- 'Home' -> 'Users & Roles'
- (if needed specify the search with a name and/or a personal code) -> 'Search'
- Choose a user whose rights need to be changed
- Click the black pencil icon on the right side of the corresponding row. If the button is not immediately visible, scroll to the right using the bar above the table.
- Add, remove or change the roles as needed
- 'Assign'
- Roles for this regular user have been updated

More informaion about user types: [Users management](03.02-users-management.md)


### Creating a new technical user

- 'Home' -> 'Users & Roles'
- 'Add user' -> select 'Technical user' as user type
- Check the box "Or create new"
- Enter the suffix
- Choose the roles for this technical user
- 'Create & Assign'
- Copy the "Client ID" and "Client Secret" to your personal notes **right away** 
- Close the module window, the technical user has been created and it has been assigned the required roles

> [!WARNING]
> "Client ID" and "Client Secret" which are shown in the module window after creating a new technical user need to be copied somewhere right away, because "Client Secret" **can't be retrieved later!**

### Assigning or modifying roles for an existing technical user

There are two possibilities for that.

Using "Add user" module:
- 'Home' -> 'Users & Roles'
- 'Add user' -> select 'Technical user' as user type
- Select a technical user (if there is only one existing technical user, it is chosen automatically; if there are many, the technical user needs to be chosen from the drop-down selection)
- Add, remove or change the roles as needed
- 'Assign'
- Roles for this technical user have been updated

Using search:
- 'Home' -> 'Users & Roles'
- 'Search'
- Choose a technical user
- Click the black pencil icon on the right side of the corresponding row. If the button is not immediately visible, scroll to the right using the bar above the table
- Add, remove or change the roles as needed
- 'Assign'
- Roles for this technical user have been updated

More informaion about user types: [Users management](03.02-users-management.md)

## Metering points

### Generating a metering point EIC code
Each grid operator, closed distribution network operator, line operator, producer, and aggregator is assigned an EIC code range by the data exchange platform. All metering point EIC codes must remain within this range. The next available metering point EIC code can be generated in Datahub.

- 'Metering points' -> 'Metering Point Bulk Import' -> 'Generate EIC codes' -> choose how many codes are needed -> 'Generate'
- Copy the generated EIC code(s)

### Creating a new metering point

Before registering grid agreement, the metering point must be registered. When adding a metering point, the required technical details must also be filled in.

- 'Metering points' -> 'New'
- Fill all of the necessary fields (mandatory fields are marked with red asterisk)
- 'Create'
- New metering point is created

> [!WARNING]
> If you select Internal as the metering point type, you will no longer be able to register a grid contract. The metering point type cannot be changed after registration, and in such a case, a new metering point with a new EIC code must be registered.

More information: [Web interface](05-metering-point.md)

### Metering point bulk import
It is also possible to use bulk upload to create or update metering points. This is a practical solution when you need to add a large number of metering points at once. A single Excel file can contain up to 1500 metering points for creation or update.

- 'Metering points' -> 'Metering point bulk import' -> 'Download'
- Fill the downloaded file with all of the metering points information and save the file to the computer
- 'Import' -> 'Search' -> choose the filled file -> 'Import'
- In case of a successful importing all of the metering points described in the file, have been added to the system. To check it go to the metering point search (see [Metering point search](#metering-point-search)) and search for some of the metering points that were just imported.

More information: [Web interface](05-metering-point.md)

### Modifying a metering point
Metering point data must always be kept up to date. When any data changes, it must also be updated in the Estfeed Datahub. Some fields (for example, metering point type) cannot be modified — in such cases, a new metering point must be registered instead.

- 'Metering points'
- Refine your search as needed (by clicking ‘Detailed search’, you can see more search parameters)
- 'Search'
- In the search results, there is a pencil icon at the end of each row. If needed, use the bar above the table to scroll horizontally.
- Edit the desired data
- Click ‘Modify’
- The metering point data has been updated

More information: [Web interface](05-metering-point.md)

### Metering point search
To view the technical data and address of metering points, use the metering point search. The search will only display metering points that the market participant has a legal basis to access.

- 'Metering points' 
- Specify the search if according to your needs (more parameters for specifiyng the search are available by clicking on 'Detailed search')
- 'Search'
- Search results show the metering points that 

More information: [Web interface](05-metering-point.md)

### Downloading metering point data
It is also possible to download metering points along with their technical data into an Excel file.

- 'Metering points'
- Refine your search as needed (by clicking ‘Detailed search’, you can see more parameters to specify your search)
- 'Search'
- 'Download'

More information: [Web interface](05-metering-point.md)

## Metering data

### Importing metering data

Importing metering data to Estfeed:
- 'Metering data' -> 'Template' -> choose the parameters needed for uploading metering data (*for uploading hour-resolution data the timestamps need to be full hours and for uploading 15-min-resolution data the timestamps need to be full 15 minutes(:00, :15, :30, :45)*) -> 'Download'
- Fill all of the columns in the downloaded tempelate and save in your computer. Guide how to fill the Excel file can be found here: [Transmitting metering data via Excel](12-metering-data.md#transmitting-metering-data-via-excel).
- 'Metering data' -> 'Import' -> choose the file to upload -> 'Import'
- If the file has no mistakes then the metering data is imported on is being importated
- To see if the metering data has beed imported can be checked by two flows:
  - 'Metering data' -> 'Metering Data Status' -> choose a time period -> 'Search'
  - 'Metering data' -> 'Fill the necessary fields' -> 'Search' -> Check if the metering data you uploaded comes up in the search

[!WARNING]
When uploading metering data, the reading time value — the time when the data was read — is validated. Estfeed displays only the data with the most recent reading time. When correcting data, please make sure that the reading time is later than the previous upload. If this column is left empty in Excel, the upload time will automatically be used as the reading time.

[!WARNING]
After uploading the data, make sure to check the data processing status to confirm that the data was successfully saved. This can be done in the web interface under the 'Metering data status' page.

More information: [Transmitting metering data via the web interface](12-metering-data.md)


### Download metering data
You can also download metering data into an Excel file. The data will be downloaded in its original resolution, which cannot be changed by the user.

Downloading the metering data:
- 'Metering data' -> fill all of the necessary fields -> 'Search' -> 'Download'
- File with the requested metering data is downloaded

[!WARNING]
It is only possible to view metering data for one metering point at a time.

### Metering data search
You can also view metering data in the web interface. In the web interface, the data can be viewed in different resolutions, for example, by aggregating the total monthly consumption.

- 'Metering data'
- Add "Meter EIC" and "Period start" (the search can be specified by using different parameters)
- 'Search'
- The metering data corresponding to the entered search is displayed in the search results

[!WARNING]
It is only possible to view metering data for one metering point at a time.

More information: [Transmitting metering data via the web interface](12-metering-data.md)

## Agreements

### Grid agreement

A grid agreement can only be added by the metering point owner — a grid operator, closed distribution network operator, line operator, or producer. The metering point
must be registered beforehand.

- 'Agreements' -> 'New agreement'
- Choose the agreement type (Grid, Border Grid)
- 'Search meter'
- According to the selected parameters, find the metering point for which you want to create the agreement
- Choose one or many metering points
- 'Search customer'
- Choose a customer (*or register a new customer if the intended customer is not in the system yet, see [Registering a new customer to the system](#registering-a-new-customer-to-the-system))
- Add the 'Valid from' date (and 'Valid to' date)
- 'Register new agreement'
- New agreement is registered

More information: [Web interface](06.2-grid-agreement.md)

### Registering a new customer to the system

When adding a grid agreement, a client must always be specified. If the client is not yet registered in the data exchange platform, the client must be registered during the grid agreement creation.

This action can only be performed by Grid Operator role.
- 'Agreements' -> 'New agreement' -> 'Search meter' -> specify the search -> 'Search'
- Choose one or many metering points
- 'Search customer' -> 'Register new customer'
- Choose the customer type (Physical person, Legal person, Organization)
- Fill all of the mandatory fields
- 'Save'
- New customer is registered into the system so now new agreements can be formed with them

More information: [Web interface](06.2-grid-agreement.md)


### Supply agreement

An open supply agreement can only be added by a user with the Open Supplier role. The client must have a grid agreement at the metering point.

- 'Agreements' -> 'New agreement' 
- Enter the customers EIC code or click 'Search customer' to search for a customer by different parameters
- When the client is chosen -> 'Search meter' -> 'I consent'
- Choose one or many metering points for which the agreement is being created
- Add 'Valid from' date (and 'Valid to' date)
- 'Register new agreement'
- New agreement is registered

More information: [Web interface](06.3-open-supply-agreement.md)

### Aggregation agreement
An aggregation agreement can only be added by a user with the Aggregator role. The metering point must be registered beforehand.

- 'Agreements' -> 'New agreement'
- Add your metering point EIC code or click 'Search metering point'
- Add your client’s EIC code or click 'Search customer'
- Specify the validity period
- 'Register new agreement'
- The new agreement has been added

> [!WARNING] 
> The client must have a grid agreement at the metering point for the desired period, and no other aggregator may have an aggregation agreement for the same metering point during that period.

More information: [Aggregation agreement](06.6-aggregation-agreement.md)

### Retroactive Addition of Open Supply Agreements
There are specific rules for the dates when open supply agreements can be added. If a agreement was not added on time, you can also initiate agreement coordination. In that case, the agreement will only be registered after approval by the parties. This can only be done with the Open Supplier role.

- 'Agreements' -> 'New agreement'
- In the agreement form, check 'Agreement Coordination'
- Add the customer’s EIC code or click 'Search customer'
- Add the metering point’s EIC code or click 'Search metering point'
- Enter the desired dates
- Add a reason
- Click 'Initiate Coordination'
- The coordination has been initiated.

More information: [Web interface](06.8-agreement-amendments-requiring-coordination.md)

### Deleting an Agreement
Deleting agreements is allowed in certain cases for agreements starting in the future. The rules can be found on the agreement type page in this documentation.

- 'Agreements'
- Fill in the desired fields to refine the search (more options under 'Detailed search')
- 'Search'
- If deletion is allowed, a 'Delete' button will appear at the end of the row
- Confirm deletion
- The agreement has been deleted

### Modifying an Agreement
Agreements can also be modified, for example, to add an end date. The rules can be found on the agreement type page in this documentation.

- 'Agreements'
- Fill in the desired fields to refine the search (more options under 'Detailed search')
- 'Search'
- If modification is allowed, a 'Modify' button will appear at the end of the row
- Make the desired changes
- 'Save'
- The agreement changes have been saved

### Retroactive Modification of Open Supply Agreements
There are specific rules for the dates when open supply agreements can be modified. If a agreement was not modified on time, you can also initiate agreement coordination. In that case, the agreement will only be registered after approval by the parties. This can only be done with the Open Supplier role.

- 'Agreements'
- Fill in the desired fields to refine the search (more options under 'Detailed search')
- 'Search'
- In the search results, click 'Modify' at the end of the row, or if not present, 'Coordination'
- In the modification window, check 'Agreement Coordination'
- Make the desired changes
- Add a reason
- Click 'Initiate'
- The coordination has been initiated.

More information: [Web interface](06.8-agreement-amendments-requiring-coordination.md)

### Agreement search
Searching for agreements may be necessary, for example, for billing, data verification, or modifying agreements.

- 'Agreements'
- Fill the fields to specify the search (more options under 'Detailed search')
- 'Search'
- Agreements corresponding to the chosen parameters are displayed in the search results

### Downloading Agreements
We also offer the option to download agreements into Excel. A maximum of 40,000 agreements can be downloaded at once. To reduce a larger number, use additional search parameters or the API solution.

- 'Agreements'
- Fill in the desired fields to refine the search (more options under 'Detailed search')
- 'Search'
- Agreements matching the selected parameters will be displayed in the search results
- Click 'Download'
- The Excel file has been downloaded

### Agreement Coordinations
After initiating agreement coordinations, the affected parties must approve or reject the changes.

- 'Agreements' -> 'Agreement Coordination'
- Optionally, refine your search. For example, check 'Awaiting my decision'
- 'Search'
- Optionally, click on a coordination row to see more information. Clicking the document icon allows viewing the related agreements
- At the end of each row awaiting approval, there are 'Approve' or 'Reject' buttons. Make the appropriate choice
- In the modal that opens, confirm your choice. When rejecting, a reason must be provided
- A response has been given for the coordination

More information: [Web interface](06.8-agreement-amendments-requiring-coordination.md)


## Connection requests

To send any connection requests, there already needs to be current joint invoice agreement (see [Joint invoice agreement](#joint-invoice-agreement)), grid agreement (see [Grid agreement](#grid-agreement)) and supply agreement (see [Supply agreement](#supply-agreement)).

![Connection request scheme](../images/Connection_request_scheme.jpeg)

***Diagram 1.** Schema of assumptions for network connection requests* 

### Sending a connection request

This action can only be performed by Open Supplier role. If all of the prerequisite contracts are in place, then:
- 'Connection requests' -> 'Initiate'
- Fill all of the necessary fields (marked with a red asterisk)
- *To "Receiver EIC" - Grid Operator EIC code who has active Grid agreement with this customer at this metering point*
- *To "Customer EIC" - EIC code of the customer who has active Grid and Supply agreements in this metering point*
- *"Metering point EIC" - Metering point EIC code that has active Grid and Supply agreements with this customer*
- If needed, a message can be added
- 'Send'
- The connection request has been sent

### Reading a connection request

This action can be performed by Open Supplier, Closed Network Distribution or Grid Operator roles.

- 'Connection requests'
- Choose a timeperiod ("Creation Date From" and "Creation Date To") so the time connection request was sent would be in that timeperiod
- 'Search'
- In the search results are shown all of the connection requests that have been made during that time period
- Connection requests history can be viewed by opening the 'Message history' icon from the right side of chosen message requests row

### Answering to a connection request

This action can be performed by Open Supplier and Grid Operator roles.

- 'Connection requests'
- Search for messages in certain timeperiod
- Choose a connection request message to respond to
- Click on 'Quick reply' icon, second icon from right on that messages row
- Fill all of the necessary fields
- 'Reply'
- Reply to the connection request has been sent. It can be checked by clicking on 'Message history'.

