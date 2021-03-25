



##Connecting to OS Places API

From the Power Apps homescreen, navigate to Data > Connections > New Connections, and either search for or scroll to OS Places API. 

Select the connector and enter your API key. For more information on the API and accessing a key, please go to LINK.

Click create. Your new connection will now appear under yout list of active connections.



##Creating a new app

In the PowerApps Studio or Web, navigate to Create and create a new Canvas app from blank.

Name your app, and select either Tablet or Phone layout as per your need. 

Click Create.


##Adding Data to the app

In the studio for your newly created app, navigate to the Data tab in the toolbar on the left side.

Click Add data, navigate to Connectors and select OS Places API. The connection you created earlier will be visible here, and can be selected as a data source.


##Setting up a free text address search

Rename Screen1 to AddressSearch from the Tree view on the left side.

Insert a Text input control from the Insert Tab > Text > Text input and Rename the control from TextInput1 to SearchBar.

Clear the Default value, ensure the Format is Text, and change the HintText to “Enter Address Search Here”.

For additional functionality, toggle the Clear button and Enable spell check parameters to on to allow for faster clearing of search queries and spell checking.

Insert a Button input control from the Insert Tab and Rename the control from Button1 to SearchButton.

Change Text to "Search" and ensure Display mode is set to edit.

In the advanced settings for your SearchButton, clear the OnSelect property and enter the following formula:

Set (SearchResults, OSPlaces.Find ('SearchBar'.Text).results)

You'll notice that once entered, an error notification will pop up over your SearchButton. This is because we have not yet created a gallery in which to display search results. This will be covered in the next section.

Note that this formula is for a free text address search using the OSPlaces.Find resource. For other OS Places API resources, the following formulas can be entered instead:

Postcode search
Set (SearchResults, OSPlaces.Postcode ('SearchBar'.Text).results)

UPRN search
Set (SearchResults, OSPlaces.UPRN ('SearchBar'.Text).results)

Nearest address to a set of Coordinates search
Set (SearchResults, OSPlaces.Nearest ('SearchBar'.Text).results)

For more information on how these resources work and the required inputs, please go to LINK.


##Creating a search results gallery

Insert a Blank vertical gallery from he Insert Tab > Gallery > Blank vertical and Rename the gallery from Gallery1 to Results. Resize your new gallery as required.

In the advanced settings for your Results gallery, clear the Items property and enter SearchResults (matching the variable within the search formula above).

With your Results gallery selected, insert a Text label from the Insert Tab > Text > Label. Rename the label from Label1 to Address.

In the advanced settings for your Address text label, clear the Text property and enter the following formula:

ThisItem.DPA.ADDRESS

Resize the label and the gallery as required.

Note that this formuala uses the ADDRESS, X_COORDINATE, and Y_COORDINATE fields from OS Places API. Additonal labels can be added to the gallery using fields including but not limited to POSTCODE, ORGANISATION_NAME, and UPRN.


##Performing a search query

Your basic free text search is now configured. To test this without publishing the app, navigate to Preview the app in the top-right corner.

In the preview screen, type a search query into the search bar, and click the search button. The results of the search will now appear in the results gallery below.















