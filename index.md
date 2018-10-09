## About
Last Updated: 2018-09-13    
Software Used: Tableau Public 2018.1  
Created by [Sarah Pugachev](https://github.com/sclayton29)  


## Table of Contents
* [Introduction](#introduction)
* [Getting the Data](#getting-the-data)
* [Loading the Data into Tableau](#loading-the-data-into-Tableau)
* [Creating a Map](#creating-a-map)
  * [Renaming a Sheet](#renaming-a-sheet)
  * [Understanding Tableau's Data Structure](#understanding-tableaus-data-structure)
  * [Building the Base Visualization](#building-the-base-visualization)
  * [Adding Filters](#adding-filters)
  * [Refining the Style](#refining-the-style)
  * [Exposing a Filter](#exposing-a-filter)
* [Creating a Bar Graph](#creating-a-bar-graph)
  * [Adding Data to Rows and Columns](#adding-data-to-rows-and-columns)
  * [Styling Bar Graph](#styling-bar-graph)

## Introduction
This lesson will take you through creating a data visualization with Tableau.

Tableau is a drag and drop tool that allows users to create interactive visualizations without any programming. This can be a good way to explore or present your data. You can view examples of Tableau built visualizations in the [Tableau Public Gallery](https://public.tableau.com/en-us/s/gallery). 

Tableau Public is available for anyone for free, but you have to save your visualizations to the Tableau server. If you have data you cannot or do not want to make public, [academic trials of the full software are available](https://www.tableau.com/academic).

If you follow along with this material, by the end of the workshop you will have a visualization that looks similar to the one below. 
{% include tableau-viz.html %} 

[Return to Top](#about)

## Getting the Data
For this lesson, we will look at campaign contributions in Oklahoma during the 2016 Presidential Election. 

We will be using freely available data from the [Federal Election Commission](https://classic.fec.gov/disclosurep/PDownload.do). We have done a bit of clean up work on this data. Namely, we removed all of the individual contributors names. 

*Why would we want to delete the contributors' names from our dataset?*  


Let's download the cleaned data to get started! 
* **[Download the cleaned data](https://github.com/sclayton29/Tableau-2016CampaignContributions/raw/master/data/OKContributions.csv)**
* Move the downloaded file to another location where you can easily locate it. I'll move the the file to my Desktop. 
* Look over the spreadsheet to get a better understanding of the data we will be using. 

*What are some of the data columns you think would be the most interesting to visualize?*   
*Do you anticipate any problems visualizing this data?*  
*What are some of the research questions you might hope to explore using this data?*


## Loading the Data into Tableau
Now that we have our data downloaded and have thought about our research areas, we are ready to get started.
   
First, let's get our data into Tableau.    
* Open your tableau application. 
* On the left side, under **Connect** and **To a File**, select **Text File**.
![Connect to a File](images/img_01.png)
*Note: Although you likely opened your file in Excel to view it in the section above. It is actually a [CSV file](https://en.wikipedia.org/wiki/Comma-separated_values), which Tableau classifies as a Text File. If the file had ended with an excel file extension like .xls, you would Connect to Microsoft Excel.*
* In the file explore that pops up, navigate to and select the OKContributions.csv file. Click **Open** to load the data. 
* A preview of the data you just loaded should open in the Tableau window. Look this over quickly to verify that you uploaded the correct dataset. 
![Data Preview after loading](images/img_02.png)

## Creating a Map
To create our first visualization, with this data, select **Sheet 1** in the bottom left corner. 
### Renaming a Sheet
Before we do anything else, let's rename Sheet 1. 
* Right click on **Sheet 1** at the bottom of the window. 
* Select **Rename**. 
* Enter a new name. For this example, we will use **Map**. 

### Understanding Tableau's Data Structure
Now, look at how our tabular data has been transformed into Dimensions and Measures. Each column name has been placed in the side panel. To the left of each column name is a symbol to indicate the data type assigned. Abc indicates textual data, the calendar icon symbolizes dates, the globe means spatial data, and the hashtag indicates numerical data.  
![Columns transformed](images/img_03.png)

*What exactly is the difference between dimensions and measures in Tableau?*  
According to the [Tableau Online Help](https://onlinehelp.tableau.com/current/pro/desktop/en-us/datafields_typesandroles.html):

"Dimensions contain qualitative values (such as names, dates, or geographical data). You can use dimensions to categorize, segment, and reveal the details in your data. Dimensions affect the level of detail in the view.

Measures contain numeric, quantitative values that you can measure. Measures can be aggregated. When you drag a measure into the view, Tableau applies an aggregation to that measure (by default)."

Tableau does a pretty good job of putting data columns into the correct categories and correct data type classifications. 

Luckily, Tableau provides some features to help us figure out when kind of data to use. On the right side of the Tableau window, you should see icons of different visualization types. *If you don't see this, click __Show Me__ in the upper right corner of the screen.* You can hover off the different visualization types to see what data types are recommended. 

Hoover over the symbol map (second row, first on left) to see that recommended data types. 
![Data types for symbol maps](images/img_04.png)

For symbol maps, you will need on 1 geo dimension and can add more dimensions and measures. 


### Building the Base Visualization
To create a visualization, we need to drag and drop data on the map. 

* Click on the **Contrbr Zip** under Dimensions on the left sidebar. Drag it over to the center **Drop Field Here.**
![Dragging Data Onto the Map](images/img_05.png)  

* Because, Tableau has classified this field as a geographical data dimension. A map was automatically selected as the data visualization. 

  *Note: This data should only contain Oklahoma contributions, but a few dots pop up in other parts of the country. What do you think is going on here? How would you investigate further?*

* Click on the newly created map, to see some map controls in the left corner. Click on the **plus sign** to zoom in closer to Oklahoma. Move the map around by holding down **Shift** while clicking and dragging the map. 

![Zoomed in Map of Oklahoma](images/img_06.png)
*How would you describe this map to a colleague? What does it show?*  

Let's add some more data to our map. We know the zip codes where the contributions are originating, but how large were these contributions? We will add additional data into the **Marks** panel located in between the data fields and the map. 
* Select **Contb Receipt Amt** located under **Measures**. Drag it it to **Size** under **Marks.** After doing this, you dots on the maps should be sized based on the amount contributed, and **SUM(Contb Re)** should be listed under **Marks** with the size icon to the left of it. 
![Sizing based on contribution amount](images/img_07.png)

Notice the map has changed. 
*Does anything seem strange about this map? Pay attention to the legend that appears on the right side of the window.*  
![Legend](images/img_08.png)
Open up your original data and try to figure out why it starts at -$2,700. 
*How would you approach or explain this issue?*

Also looking at the map, we notice that most of the dots are quite small. Looking at the scale in the legend, notice that it goes up to 322,873. We might imagine that most of the donations are not close to that size. Let's adjust the scale to show a bit more of the nuance in the smaller donations. 
* To adjust the scale, click the down arrow on the top of the legend box and select **Edit sizes**.
![Edit sizes](images/img_09.png) 
* In the drop down menu under **Sizes vary** select **By Range**. 
* Check the **End value for range** and edit the text box to be 150,000. 
* Click **OK** to apply these changes. 
![Edit sizes 2](images/img_10.png) 


### Adding Filters 
If you look back at your the original spreadsheet, you will notice that this dataset includes information about donations to many different candidates. Let's add a filter to only show contributions to Trump and Clinton. 
* Find **Cand Nm** under **Dimensions** and drag that to the **Filters** box (located right above the marks box).
* In the dialog box that appears, select **Clinton, Hilary Rodham** and **Trump, Donald J.**.
* Click **OK** to finalize the filter. 
* **Cand Nm** should now appear in your filter box, and your map should have updated to only show contributions to Trump and Clinton.
![Filter](images/img_11.png) 
*Note: If you want to go back and edit this filter, you can use the down arrow next to Cand Nm.* 

Sometimes when you add filters, you can miss the way the visualization changed. Luckily Tableau has undo and redo functionalities that allow you to quickly reverse and re-implement what you just did. You can either use your normal keyboard shortcuts (like Cmd + Z on Macs) or use the back and forward arrows at the top left of the screen. Try to undo and redo adding the filter and pay attention to how your map changes. 
![Undo and Redo](images/img_12.png) 

Before moving on, we want to set this filter to be applied to all of the related visualizations we will create. 
* To do this, click on the down arrow next to Cand Nm. 
* Select **Apply to Worksheets**.
* Then, select **All Using This Data Source**.
![Undo and Redo](images/img_12a.png) 


### Refining the Style
Notice that after we updated the filter, the scale we selected for our SUM(Contb Receipt Amt) doesn't seem as approriate. Let's go back into our legend and edit it. 
* Go the the SUM(Contb Recepit Amt) legend on the right size of the screen. 
* Click on the box and select the **down arrow**. 
* Select **Edit sizes**.
![Edit sizes](images/img_09.png) 
* In the dialog box that appears, select **Automatically** from the dropdown under **Sizes vary**. Also, **uncheck the End value for range box**. We lose a bit of control over the sizes this way, but we will not have to continually update the sizes as we add filters. 
* Click **OK** to apply your changes. 
![Edit sizes back to Automatic](images/img_13.png) 

SUM(Contb Recepit Amt) is not a very intuitive title for this legend. Let's change it to make it more understandable for viewers. 
* Click on the **down arrow** next to the title. 
* Select **Edit Title**.
![Edit title](images/img_14.png) 
* In the text box, that appears enter the title you want to use. For the example, we will use **Contribution Amount for Zip Code**.
* Click **OK** to save your changes. 


Let's now add an element to differentiate between Clinton and Trump's contributions. Using two different colors seems like a good choice. 
* To add colors based on the candidates, drag **Cand Nm** to the **Color** box under **Marks**.
* The map should update to show two different colors, and a legend for Cand Nm should appear on the left. Using the same steps, we used for the Contribution Amount, update the title of this legend to **Candidate**. 

We may also want to update the colors. Since red is commonly used to represent the Republican party and blue the Democratic party. Let's make Clinton blue and Trump red. 
* Click on the down arrow in the candidate box and select **Edit colors**.  
* Select **Clinton, Hillary Rodham** on the left and blue on the right to assign the color. 
* Repeat with **Trump, Donald J.** and red. 
* Click **OK** to save your changes. 
![Edit colors](images/img_15.png) 

*Note: There are almost always multiple way to do a task in Tableau. In the example above, you could have also editted the colors by clicking the __Colors__ under __Marks__*. 


### Exposing a Filter
We may also want to filter based on date to see if the contributions changed over time. 
* Add a filter using the **Contb Recepit Dt** dimension. 
* After you drag the field to the filter box, a dialog box will open asking you how you want to filter. Select **Range of Dates** and then **Next** to continue adding the filter. 
![Add Date filter](images/img_16.png) 
* In the next dialog box that appears, keep all the default settings and click **OK** to apply it.  

Your map should not change after applying this filter. After all, we selected all of the existing values. 

One of the benefits of Tableau is its interactivity. So, we can expose this filter as an option for viewers to use. 
* Select the down arrow next to **MY(Contb Recepit)**.
* Then, select **Show Filter**. 
![Showing Date Filter](images/img_17.png) 

Notice that this filter appears on the right side with slider that will allow you to sort through the dates. Play around with the slider and see how the map changes. Notice how the contribution amount legend also adjusts. 

*What are the pros and cons of this auto adjustment in the legend?*

As you  explore this functionality, you may notice that in the early dates there are not contributions that show on the map. We can exclude that time frame by forcing the filter to only include non-Null values. 
* Using the down arrow by the **Contb Receipt Dt**, select **Only Relevant Values**. 
![Show Only Relevant Values](images/img_18.png) 
* Go ahead and also change the title of **Contb Receipt Dt** to something more easily understandable. 

### Editing the Tooltip
Before we move on to our next visualization, let's edit the tooltip. The tooltip is the pop up that occurs when you click on a point on your map. 
* Try clicking on a point to see what show ups. 
![Current Tooltip](images/img_18a.png)
* To add another field to our tooltip, we need to drag that field onto the **Tooltip** box under **Marks**. 
* Try doing this with the **Contbr City** dimension. 
* Hover points to see the added info. 
* Like with our legend titles we want our tooltip to be as clear as possible. To edit the language used in the tooltip, select **Tooltip** in the **Marks** panel. 

## Creating a Bar Graph
When you were looking at the data, you may have notice a few columns about the contributors occupation. Let's dig into this some more using a bar graph. 

First, we need to create a new sheet to create our graph. 
* Next to **Map** in the bottom left corner, select the icon that looks like a **bar graph with a +**.
![Creating a New Sheet](images/img_19.png) 
* A blank sheet will open up. Rename the new sheet to something like **Professions**. 

### Adding Data
For the bar graph, we will need to add data, to rows and columns boxes near the top of the window. 
* Drag **Contbr Occupation** to Rows and **Contrb Receipt Amt to Columns**. 
![Adding Data to Rows and Columns](images/img_20.png) 
Recognizing the type of data added, Tableau should automatically create a bar graph. 

### Styling Bar Graph
