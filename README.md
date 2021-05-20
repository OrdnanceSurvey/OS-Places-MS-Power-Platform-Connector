# Getting Started Guide

Ordnance Survey Places provides the latest details of over 40 million addresses across the UK connecting the existing OS Places API service to your app.

A guide to connecting to and querying OS Places API in Microsoft's Power Apps.

### Connecting to OS Places API

From the **Power Apps** homescreen, navigate to **Data > Connections > New Connections**, and either search for or scroll to **OS Places API**.

![image](https://user-images.githubusercontent.com/81246539/112963255-1965c800-913f-11eb-8d61-cc05ce7178c1.png)

Select the connector and enter your **API key**.

Click **Create**. Your new connection will now appear under yout list of active connections.


### Creating a new app

In the **Power Apps** homescreen, navigate to **Create** and select a new **Canvas app from blank**.

![image](https://user-images.githubusercontent.com/81246539/112963215-0fdc6000-913f-11eb-830c-f0c5465b544f.png)

Name your app, and select either **Tablet or Phone** layout as per your need. Click **Create**.


### Adding Data to the app

In the **Power Apps studio** for your newly created app, navigate to the **Data** tab in the toolbar on the left side.

![image](https://user-images.githubusercontent.com/44440827/118996288-b0047780-b97f-11eb-80ce-c4da15200847.png)


Click **Add data**, navigate to **Connectors** and select **OS Places API**. The connection you created earlier will be visible here, and can be selected as a data source.


### Setting up a free text address search

Rename **Screen1** to **AddressSearch** from the Tree view on the left side.

![image](https://user-images.githubusercontent.com/81246539/112963425-44501c00-913f-11eb-8b2e-1b9f774ec51c.png)

Insert a **Text input control** from the **Insert** Tab **> Text > Text input** and rename the control from **TextInput1** to **SearchBar**.

Insert a **Button** input control from the **Insert** Tab and rename the control from **Button1** to **SearchButton**.

![image](https://user-images.githubusercontent.com/81246539/112963184-06eb8e80-913f-11eb-9ebc-f73af905c6df.png)

In the properties pane for **SearchBar** (appears on the right side), clear the **Default** value, ensure the **Format** is **Text**, and change the **HintText** to **“Enter Address Search Here”**.

![image](https://user-images.githubusercontent.com/81246539/112963450-4c0fc080-913f-11eb-937b-5864d09876f7.png)

For additional functionality, toggle the **Clear** button and **Enable spell check** parameters to on to allow for faster clearing of search queries and spell checking.

In the properties pane for **SearchButton**, change **Text** to **"Search"** and ensure **Display mode** is set to **edit**.

![image](https://user-images.githubusercontent.com/81246539/112963536-60ec5400-913f-11eb-921a-dfa2b469ddfc.png)

In the **advanced** settings, clear the **OnSelect** property and enter the following formula:

*Set (SearchResults, OSPlaces.Find ('SearchBar'.Text).results)*

![image](https://user-images.githubusercontent.com/81246539/112963486-56ca5580-913f-11eb-9ed5-363faf690d81.png)

You'll notice that once entered, an **error notification** will pop up over your **SearchButton**. This is because we have not yet created a gallery in which to display search results. This will be covered in the next section.

Note that this formula is for a free text address search using the **OSPlaces.Find** resource. For other **OS Places API** resources, the following formulas can be entered instead:

* **Postcode search**
*Set (SearchResults, OSPlaces.Postcode ('SearchBar'.Text).results)*

* **UPRN search**
*Set (SearchResults, OSPlaces.UPRN ('SearchBar'.Text).results)*

* **Nearest address to a set of Coordinates search**
*Set (SearchResults, OSPlaces.Nearest ('SearchBar'.Text).results)*

### Creating a search results gallery

**Insert** a **Blank vertical gallery** from he **Insert** Tab **> Gallery > Blank vertical** and rename the gallery from **Gallery1** to **Results**. Resize your new gallery as required.

![image](https://user-images.githubusercontent.com/81246539/112963161-ffc48080-913e-11eb-9d11-d2082adfd3a3.png)

In the advanced settings for your **Results** gallery, clear the **Items** property and enter **SearchResults** (matching the variable within the search formula above).

![image](https://user-images.githubusercontent.com/81246539/112963394-3b5f4a80-913f-11eb-8066-2c185725e3ad.png)

With your **Results** gallery selected, insert a **Text label** from the **Insert** Tab **> Text > Label**. Rename the label from **Label1** to **Address**.

![image](https://user-images.githubusercontent.com/81246539/112963072-ec191a00-913e-11eb-98fb-abced16144bc.png)

In the **advanced settings** for your **Address** text label, clear the **Text** property and enter the following formula:

*ThisItem.DPA.ADDRESS*

![image](https://user-images.githubusercontent.com/81246539/112963632-7a8d9b80-913f-11eb-8cfb-e6213d3bd4f8.png)

Resize the label and the gallery as required.

Note that this formuala uses the **ADDRESS** field from **OS Places API**. Additonal labels can be added to the gallery using fields including but not limited to **POSTCODE, ORGANISATION_NAME, X_COORDINATE, Y_COORDINATE,** and **UPRN**.


### Performing a search query

Your basic free text search is now configured. To test this without publishing the app, navigate to **Preview the app** in the top-right corner.

![image](https://user-images.githubusercontent.com/81246539/112963281-21256c80-913f-11eb-8d05-4bac628221bc.png)

In the **preview screen**, type a search query into the search bar, and click the **search button**. The results of the search will now appear in the **results gallery** below. Your app and results should look something like the below. You have now performed your first free text search using OS Places API in Power Apps.

![image](https://user-images.githubusercontent.com/81246539/112963125-f89d7280-913e-11eb-93a4-225d87b4f614.png)

By combining the above inputs and formulas with additonal app components, fields, and styling, you can create a bespoke app with greater functionality and a fully expanded user interface, such as the below:

![image](https://user-images.githubusercontent.com/81246539/112963096-f1766480-913e-11eb-8dd4-6b11c9548d54.png)
