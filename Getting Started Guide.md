# Getting Started Guide

A guide to connecting to and querying OS Places API in Microsoft's Power Apps.


### Connecting to OS Places API

From the **Power Apps** homescreen, navigate to **Data > Connections > New Connections**, and either search for or scroll to **OS Places API**.

![image](https://user-images.githubusercontent.com/81246539/112861525-c6dbcb80-90ac-11eb-9414-2aeaf983470a.png)

Select the connector and enter your **API key**. For more information on the API and accessing a key, please go to **LINK**.

Click **Create**. Your new connection will now appear under yout list of active connections.


### Creating a new app

In the **Power Apps** homescreen, navigate to **Create** and select a new **Canvas app from blank**.

![image](https://user-images.githubusercontent.com/81246539/112861506-c2171780-90ac-11eb-996c-46b725e94d99.png)

Name your app, and select either **Tablet or Phone** layout as per your need. Click **Create**.


### Adding Data to the app

In the **Power Apps studio** for your newly created app, navigate to the **Data** tab in the toolbar on the left side.

![image](https://user-images.githubusercontent.com/81246539/112861270-9005b580-90ac-11eb-9326-2d8260e6c6d9.png)


Click **Add data**, navigate to **Connectors** and select **OS Places API**. The connection you created earlier will be visible here, and can be selected as a data source.


### Setting up a free text address search

Rename **Screen1** to **AddressSearch** from the Tree view on the left side.

![image](https://user-images.githubusercontent.com/81246539/112861625-deb34f80-90ac-11eb-8569-d77841082efd.png)

Insert a **Text input control** from the **Insert** Tab **> Text > Text input** and rename the control from **TextInput1** to **SearchBar**.

Insert a **Button** input control from the **Insert** Tab and rename the control from **Button1** to **SearchButton**.

![image](https://user-images.githubusercontent.com/81246539/112861488-bdeafa00-90ac-11eb-8e56-e2e82c2c76c6.png)

In the properties pane for **SearchBar** (appears on the right side), clear the **Default** value, ensure the **Format** is **Text**, and change the **HintText** to **“Enter Address Search Here”**.

![image](https://user-images.githubusercontent.com/81246539/112861829-128e7500-90ad-11eb-9c48-260af3bcdf4d.png)

For additional functionality, toggle the **Clear** button and **Enable spell check** parameters to on to allow for faster clearing of search queries and spell checking.

In the properties pane for **SearchButton**, change **Text** to **"Search"** and ensure **Display mode** is set to **edit**. In the **advanced** settings, clear the **OnSelect** property and enter the following formula:

*Set (SearchResults, OSPlaces.Find ('SearchBar'.Text).results)*

![image](https://user-images.githubusercontent.com/81246539/112861869-1cb07380-90ad-11eb-8439-3e4d787df173.png)

![image](https://user-images.githubusercontent.com/81246539/112861853-18845600-90ad-11eb-8a69-bd3e7079e2e7.png)


You'll notice that once entered, an **error notification** will pop up over your **SearchButton**. This is because we have not yet created a gallery in which to display search results. This will be covered in the next section.

Note that this formula is for a free text address search using the **OSPlaces.Find** resource. For other **OS Places API** resources, the following formulas can be entered instead:

* **Postcode search**
*Set (SearchResults, OSPlaces.Postcode ('SearchBar'.Text).results)*

* **UPRN search**
*Set (SearchResults, OSPlaces.UPRN ('SearchBar'.Text).results)*

* **Nearest address to a set of Coordinates search**
*Set (SearchResults, OSPlaces.Nearest ('SearchBar'.Text).results)*

For more information on how these resources work and the required inputs, please go to **LINK**.


### Creating a search results gallery

**Insert** a **Blank vertical gallery** from he **Insert** Tab **> Gallery > Blank vertical** and rename the gallery from **Gallery1** to **Results**. Resize your new gallery as required.

![image](https://user-images.githubusercontent.com/81246539/112861345-9eec6800-90ac-11eb-9368-7522f275b97c.png)

In the advanced settings for your **Results** gallery, clear the **Items** property and enter **SearchResults** (matching the variable within the search formula above).

![image](https://user-images.githubusercontent.com/81246539/112861452-b62b5580-90ac-11eb-9ef6-83adc11f3d7d.png)

With your **Results** gallery selected, insert a **Text label** from the **Insert** Tab **> Text > Label**. Rename the label from **Label1** to **Address**.

![image](https://user-images.githubusercontent.com/81246539/112861364-a27fef00-90ac-11eb-857a-b8f8ebfed431.png)

In the **advanced settings** for your **Address** text label, clear the **Text** property and enter the following formula:

*ThisItem.DPA.ADDRESS*

![image](https://user-images.githubusercontent.com/81246539/112861406-aad82a00-90ac-11eb-87dd-2a242793e0f9.png)

Resize the label and the gallery as required.

Note that this formuala uses the **ADDRESS** field from **OS Places API**. Additonal labels can be added to the gallery using fields including but not limited to **POSTCODE, ORGANISATION_NAME, X_COORDINATE, Y_COORDINATE,** and **UPRN**.


### Performing a search query

Your basic free text search is now configured. To test this without publishing the app, navigate to **Preview the app** in the top-right corner.

![image](https://user-images.githubusercontent.com/81246539/112861569-d0653380-90ac-11eb-9d83-f8d153e707cb.png)

In the **preview screen**, type a search query into the search bar, and click the **search button**. The results of the search will now appear in the **results gallery** below.

![image](https://user-images.githubusercontent.com/81246539/112861781-060a1c80-90ad-11eb-89e2-e89c21e520b8.png)

