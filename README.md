# Speed Camera Violations, City of Chicago 

This file documents the analysis of **_Speed Camera Violations_** dataset provided by the City of Chicago. 
The dataset can be accessed [here](https://data.cityofchicago.org/Transportation/Speed-Camera-Violations/hhkd-xvj4).


## Introduction
Chicago experiences roughly 3,000 crashes annually between motor vehicles and pedestrians, about 800 of which involve children. Hence, the city initiated Children’s Safety Zone Program which protects children and other pedestrians by reminding motorists to slow down and obey speed laws – especially in school and park zones. 
Safety zones are designated as a 1/8th of a mile boundary around any Chicago parks or schools. <br/>
(Reference:https://www.chicago.gov/city/en/depts/cdot/supp_info/children_s_safetyzoneporgramautomaticspeedenforcement.html)

The program uses enhanced signage and automated safety cameras to identify and ticket motorists who are breaking the law by exceeding the speed limits. Automated speed enforcement cameras are one part of the “toolbox” the City uses to enhance safety for children and all residents in safety zones. <br/> (Reference:https://www.chicago.gov/city/en/depts/cdot/supp_info/children_s_safetyzoneporgramautomaticspeedenforcement.html)

## Speed Camera Violations Dataset
According to [Chicago Data Portal](https://data.cityofchicago.org/Transportation/Speed-Camera-Violations/hhkd-xvj4) website, this dataset reflects the daily volume of violations that have occurred in Children's Safety Zones for each automated speed enforcement camera. The data reflects violations that occurred from July 2014 to April, 2019. The dataset contains all violations regardless of whether a citation was issued.

### Exploratory Data Analysis (EDA)

[**Link to my Tableau public URL**](https://public.tableau.com/views/SpeedCameraViolations_Chicago_2014-19/Story1?:embed=y&:display_count=yes) 

1. Exploratory data analysis of this dataset revealed that there is an overall decline in the total number of violations recorded from 2015 to 2018 (years for which complete data is available). 

2. There are certain locations/ zip codes which have very high number of recorded violations as compared to other locations.

3. When plotting the number of violations on the city's map, northen part of the city has more locations with higher number of violations then the south.



## Delving deeper into findings from EDA
In Part 2 of this analysis, a set of dashboards have been developed for the Mayor of Chicago, to reveal interesting findings from the Speed Camera Violations Dataset.

[**Link to my Tableau public URL**](https://public.tableau.com/shared/CMRF63GT4?:display_count=yes) 

After EDA, there were certain questions that I wanted to explore which  guided this phase of the analysis. These questions and the subsequent analysis are presented below.


<br/>

### Q.1. Relationship between Red Light Camera Violations and Speed Camera Violations - __Are locations with Speed Camera violations also likely to have higher number of red light camera violations?__ 

Since Chicago also has a red light camera enforcement program, I wanted to compare the number of red light violations with speed camera violations to explore if there is any correlation between red light violations and speed camera violations- are certain areas in the city more prone to such violations and if yes what steps can be taken to make them safe.

The Red Light Camera violations dataset can be found [here](https://data.cityofchicago.org/Transportation/Red-Light-Camera-Violations/spqx-js37). 
I joined this dataset with Speed Camera dataset using **Violation Date** and **Zip Code** attributes and performing a full outer join since I did not want to lose any data from the Red Light Violations dataset (Losing out data might affect the overall numbers. Additionally this analysis can also be performed without joining the datasets and creating independent charts. I wanted the charts to appear in the same worksheet and hence performed the join.)

I first compared the number of speed camera violations with the number of red light camera violations from 2015 - 2018 and found that the number of red light violations are much smaller as compared to Speed Camera Violations.

![](Speed_RLC_Violations.png)

Turns out that number of **Speed Camera Violations are 6-7 times higher than red-light violations**.The difference in magnitude is surprising!


Next, I was interested to see if the same Zip Codes that were notorious for high speed camera violations had higher red light violations as well. I plotted the average number of violations per zipcode and arranged them in descending order and filtered the top 10 zip codes with highest number of violations. I then plotted the correponding average number of red-light camera violations against those zipcodes. The chart can be seen below.

![](ViolationsZipcode.png)


Here again, one can see that there is no direct correlation between the number of speed camera violations in a zip - code with the number of red-light camera violations.


**Implications**
- Based on these two findings, one possible explanation could be that red light enforcement is one of the oldest and universal traffic rules. That could explain why the number of violations are significantly smaller than Speed Camera Violations. Speed Camera enforcement is also present only in certain earmarked safety zones in the city and is enforced during certain hours of the day, which might be one of the causes of higher number of violations.

- Secondly, ticket values for Red Light violations are _$100_ whereas for Speed Camera violations tickets are _$35_ dollars for violations of 10 mph over the posted speed and _$100_ for violations of 11 mph and more. The slight irregularity and reduced ticket price could be one of the potential reasons for higher speed camera violations. (I could not find tickets dataset on the website to corroborate this insight. It would be interesting to see how many tickets are issued for less than 10 mph violations and how many are issues for violations of 11 mph and higher.)

**Actions** 
- Increasing awareness about Speed Camera Enforcement program, increased signage, advertisements and  campaigns can help reduce the number of speed-camera violations.
- The city can also consider increasing the ticket value for speed camera violations and see if that helps reduce the number of violations committed especially in zipcodes with the highest number of speed violations. 


This does however leave questions unanswered about why some zipcodes have highest number of violations. This can be explored further using demographics or traffic datasets. I plan to explore some datasets in the second phase of this analysis.

<br/>
  
### Q.2. Number of Speed Enforcement Cameras and Speed Violations - Does the number of speed enforecement cameras help reduce the number of the violations?

Speed Camera Dataset lists more than one camera for an address or zipcode. I was interested to understand why did some Zip codes have more number of cameras than others. Also, how many cameras were in operation between 2015-18 and whether any changes in the number of cameras has an impact on the number of violations.

I first created a calculated field to count the distinct number of cameras. Tableau lets users create a calculated field by clicking on the field and selecting "Calculated Field" option from the drop-down menu. A formula can then be entered is the dialog box and Tableau lets users know if the formula is correct and can be applied.
I used the formula in the image below which is similar to COUNT (DISTINCT *) in MySQL. 

![](CalcField.png)

Next I plotted the number of speed enforcement cameras from 2015 - 2018 and the average number of violations committed for the same time period.

![](NumCam_NumVioltn.png)

In the above chart one can see that the number of cameras have remained constant, but the average number of violations have declined. This means that the speed enforcement program has a general declining trend. However, it is not clear if that is due to number of cameras. It also does not explain why the city decided to increase the number of installed cameras in 2018 when the number of violations continued to decline.

I tried to explore this further by first plotting the number of cameras and the number of zip codes using bar charts. To identify the cameras that were added in 2018, I created a group of such cameras, renamed the group as 'Cameras added after 2018' and used that as a color to identify the additions in the chart below. These cameras are depicted in blue color.

![](Picture1.png)

In the chart, one can see that even though there are outliers, there is an overall decline in the average number of violations as the number of cameras increased. However, the difference by addition of new cameras is not quite evident.


I then created a scatter plot between the average number of speed violations committed and the number of speed enforcement cameras to see if there was any correlation that was missed in previous charts. I added Zipcodes for increased granularity. 

![](ScatterPlot.png)

The chart above depicts that there is an overall decline in the number of violations as the number of cameras increases, however there is significant variation especially in Zipcodes with lower number of cameras. 


**Implications**
- Based on the above charts, one can see that number of Speed Violations committed have been declining consistently from 2015 to 2018 (years for which complete data is available), which is a positive sign. However, since the number of cameras installed has remained constant through majority of this period, it is not clear whether the program is witnessing success due to number of cameras installed or is it a general decline. 
- From the scatter plot it is appears that as the number of cameras increases, the average number of violations committed per zipcode decreases. However, there are outliers with high number of average violations which need to be studied further. 

**Actions**
- Zipcodes with high number of violations need to be studied to identify the reason for such high violations and if required, increased surveillance can be adopted as one of the methods to help reduce the number of violations.


I also plan to group Zipcodes with highest number of violations and study the trend of number of violations with respect to the number of cameras; and compare that with Zipcodes with lower number of violations and see if that can provide any interesting findings.

<br/>

### Q.3. Comparing Speed  data with Traffic Crashes - Does Speed Camera enforcement lead to reduction in number of traffic crashes and resulting fatalities?

I wanted to understand the success of the speed enforcement program by studying the number of crashes in Speed Enforcement zones over the same time period. Chicago Data Portal's [website](https://data.cityofchicago.org/) provides two datasets: 
- [Traffic Crashes - Crashes](https://data.cityofchicago.org/Transportation/Traffic-Crashes-Crashes/85ca-t3if) : This dataset has information about each traffic crash on city streets within the City of Chicago limits and under the jurisdiction of Chicago Police Department (CPD) 
- [Traffic Crashes - People](https://data.cityofchicago.org/Transportation/Traffic-Crashes-People/u6pd-qa9d) : This dataset contains information about people involved in a crash and if any injuries were sustained.

I worked on these two datasests to understand the different attributes and performed data cleaning using Excel to get rid of unwanted columns. The original datasets had 48 columns ( Traffic Crashes) and 29 columns ( People dataset). 

<br/>
My cleaned Traffic Crashes dataset had 15 columns including RD_No (unique id for each records, helpful to join the traffic crashes with people involved in the crash), Crash Date, Speed Limit, Primary Contributory Cause (to identify speed and non- speed related crashes), Injuries, Crash hour and time, and location related columns.


![](Crashes.png)

<br/>
The cleaned People dataset consisted of the following columns. I split Crash Date column to separate time and date. I retained this field to be able to use this sheet independently if needed.


![](People.png)

<br/>
I tried to visualize traffic crashes and resulting fatalities on the map of Chicago and see whether there is any overlap with Speed Camera Violations. Below is a snapshot of my dashboard.

![](Map.png)



One can see that locations with speed camera enforcement and higher number of violations tend to have less number of fatalities as compared to other locations. 

Unfortunately, the Traffic datasets can only be combined with Speed Camera violations dataset using Latitude and Longitude fields to map crashes that occured in Speed Camera Enforced locations. I plan to do that in the second phase of this analysis and be able to use attributes of the Traffic Crashes dataset to explore crashes due to speeding, crashes involving pedestrians and cyclists in these locations.

**Implications**
- Speed enforcement can lead to reduced fatalities during traffic accidents since speed is a big contributing factor in severity of an accident. The maps above indicate success of the program through reduced fatalities in speed enforcement locations with higher number of violations.

**Actions**
- Traffic Crashes dataset can be explored further to identify locations prone to accidents due to speeding and introduce speed camera enforcement to make them safer for public.



## Part 3 : Documentation of recreating the dashboard

### Dashboard 1: Comparison between Red Light and Speed Camera Violations

Compared to my previous dashboard on this analysis, I have made the following changes:

1. I have merged the datasets using Jupyter notebook to ensure accurate records are reflected in my visualizations. Tableau joins might not be the best option when working with datasets with little or no common attributes. For Tableau beginners, Tableau joins might not be the best way to combine data from multiple sources. I realized the difference in my joined datasets when I performed the same merge using Python and tried to recreate it in Tableau. Also , an added benefit is speed of data processing and not unnecessarily slowing down my Tableau desktop file due to live/ extract join based data sources.

2. The second major change I made was using combined axis charts to replace my previous charts.

3. I also added two charts to the analysis. One is on the trend of average speed and red light violations over the time period of study. This not only allowed me to use some cool analytics features in Tableau but also present an interesting finding in addition to the ones presented previously.

4. Lastly, based on my previous analysis I was trying to understand whether any correlation existed by speed and red light violations and that is another addition to this week's dashboard.

So below is a detailed walkthrough of each chart, including preparing data sources using Jupyter notebook and creating the chart and the dashboard for the first finding.

**Combining data sources**
Link to data sources: 

**Python code for joining the datasets**

**Adding Data Sources to Python**
- Editing datasources by replacing xx and removing Traffic Crashes.
- Defining names of fields --> Red Camera Violations and Speed Camera Violations
- Creating Calculated fields--> Num Speed Camera
- Categorizing Dimensions and Measures

#### Preparing Chart1: Comparison between Speed Camera and Red Light Camera Violations over the years

Compared to my previous chart, I have used combined axis charts to better explain the difference between Speed and Red light violations. 

**Steps to replicate the chart**
- Drag Violation Date field to columns since we are observing a trend, rotate lables if not rotated already to improve readability.
- Click on Year and select Show Filter to generate a filter card on the right side and use that to filter out years 2014 and 2019 from the analysis for which complete data is not available.
- Drag the renamed field Speed Camera Violations and place it under rows. Drag second renamed field, Red  Light Violations and hover it on the y axis until the cursor shows two green bars which implies shared axes. This lets me display the number of Speed Camera Violations next to Red Light Violations and show the difference in bar size more clearly as compared to the chart in Part 2. 
- At this step Tableau also creates two new entities- Measure names and Measure Values. Measure names is available under the Filter Card on the right and Measure Values on Rows.
- Edit the name on the y-axis from Values to "Number of Violations (in thousands)".
- To change the color of the charts, hold down 'Command' button on MacBoock (Ctrl for Windows) and drag the Measure names from Columns to Color. Click on the Color button and then click on Edit Colors to see the option for changing colors for the bars. I have chosen blue for Speed Camera Violations and red for Red Light Violations.
- Click on the dropdown button on 'Measure name' filter card on the right, and select Edit Title. Enter the new title as 'Violation Type'. 
- Changed sheet name to P_No of violations over years
- Changed title to be the warrant/ claim for the chart and added the previous title and description under Caption. Double click on the chart title and edit text in the dialog box that appears. Use the options available for formatting like reducing font size which is useful when adding charts to dashboards, I have use font size 11 for title and formatted text in bold.
- Edit filter title to Year / Hide filter card.
- Remove gridlines by right click anywhere on the chart and selecting Format from the dropdown. Click on the 'Lines' icon and click on Rows tab. Against Gridlines select none to remove the gridlines on rows.


The chart currently looks like this:
< insert chart image>

I want to remove the titles in the bottom axes because the information is represented using the Violation Type legend on the right. To remove the axes: right click on the axis and click on Show Header to deselect it. This hides the bottom axes and makes the chart look cleaner.

- The bottom axis which contains a repetition of the 

<insert before and after charts>


#### Chart 2: Moving Average Chart


- Drag Violation Date to Columns and Speed Camera Violations to Rows. Click on SUM(Speed Camera Violations) to display the dropdown menu and change Measure (SUM) to Average.
- Drag Red Light Violations to the y axis and hover until two green bars are diplayed and create a combined axes chart. Observe the same Measure names and Measure Values are created by Tableau as in the previous chart. 
- Follow same steps as mentioned in Chart 1 to add and edit the color of the lines. Oh yes! since this is going to be a moving avergae chart make sure the Chart type is set to 'Line'.
- Edit title and add "But the average number of speed violations have continued to decline over the years".
- Rotate the x-axis.
- Hide year filter card
- Rename sheet and add caption

- **Calculating moving average**: On Measure Values card, click on the button AVG(Speed Camera Violations) to see the dropdown menu and click on Quick Table Calculation. Select Moving Average from the list of calculations available. Repeat this step for AVG(Red Light Violations).
By adding moving average calculations, a smoother line is observed in the chart for average Speed Camera and Red Light Violations committed over the years. 

*Additional Tip**: Moving average calculation can be modified to change the years for which the average is calculated by clicking on Edit Table Calculation in the dropdown menu. And updating the required year in the Previous and Next fields. 

- **Add Trend line**: On the left pane of the worksheet, click on Analytics tab and press down on Trend Line to drag it to the chart. Select Linear from the options and add trend line to the moving average. Hover over the trend line to see the R-squared and P-values of the trend line. Observe the P-value for trend line of the Speed Camera violations Moving Average line. See how the P-values is <0.0001. This implies that this is a significant change and cannot be attributed to mere chance. Thus, we conclude that average number of Speed Camera Violations have continued to decline since 2014 (year from which data is available). At the same time, P-value for the trend line for Red Light Violations has a higher value of 0.111 which is not statistically significant. Thus, we can also remove this trend line since it does not attribute to a statistically significant change in Red Light violations.

Also, notice that the difference in the average number of red light violations committed. A flat trend indicates that there will always be some red light violations committed. This could be because of people who might be rushing to get somewhere.
- Edit y axis name to 'Average Violations'.
- Edit filter Card Measure names and rename it to Violation Type.
- Edit Legend names to 


#### Chart 3: Violations in zipcodes
- Plot Average number of Speed violations against zipcode x. Right click on the chart and select View Data. From the table that appears, click on Export All and select the folder where you want to create the csv file for this dataset. Repeat the same for average number of Red Light violations.
- Now combine the number of Violations across Zipcodes using Jupyter notebook. I am doing this exercise because I realized that if you perform a join in tableau using Violation Date and Zipcode as columns for joining, the resulting number of rows are not accurate. Same holds for trying to join the two datasets on Violation Date. Performing the join using Jupyter notebook helped me understand these errors which occur due to duplication of rows. At the same time, using combined dataset with accurate number of rows does not provide the chart I am intending to replicate from the previous week because the Zipcode y values against Zipcode x values are null and vice versa. 

Code snippet below:

I performed a left join since I am interested in Zipcodes where Speed Camera VIolations have been recorded and study Red Light violations in these zipcodes.


(**Tip**: Save the exported files as CSV UTF-8 (Comma Delimited) files to successfully read the files on Jupyter notebook.)


- Create a new worksheet and add th new csv files as a data source. We will be using this file for charts 3 and 4. Delete or hide the previous worksheet since we will not be using it.

- Rename dimension Zipcode x to Zipcodes, and measures to Average Red Light Violations and Average Speed Camera Violations. This step can be optional since these changes can be made in the chart as well. But I have adopted a practice to rename dimensions and measures to avoid any confusion.
- Drag ZipCodes to columns, Average Speed Camera Violations to Rows and use the same steps followed above for a combined axis chart and add Red Light Violations. Note that there is only one value against each zipcode, hence using Sum, Average, Minimum or Maximum will all return the same average number in the original data source.
- Click on the descending order sort icon on the top or on the Y-axis to sort zipcodes by highest average speed violations. 
- Click on nulls on the chart and click on Filter to remove null values.
- Add Measure names to color and edit the colors to use the same color scheme used in previous charts for speed camera and red light violations.
Note that we now get a chart with single stacked bars for speed camere and red light violations and shows that Zipcodes with highest speed violations might not necessarily have the highest red light violations. Thus there appears to be no correlation between the two.

< insert chart image>


Let's make remaining changes to the chart.

- Edit y axis and rename it to 'Average Violations'.
- Hide field label Zipcodes using right click and selecting 'Hide Field Label for Column...' option.
- Rotate x axis label if it does not occur automatically to fit the chart on the worksheet.
- Edit title of Measure name filter card to Violation Type and edit legend alisases to Speed Camera and Red Light. 
- Remove gridlines as done for previous charts.




#### Chart 4: Scatter Plot between Average Speed Violations and Average Red Light Violations in Zipcodes

- Use ZipCode violations as data source for the worksheet.
- Drag Average Speed Camera Violations to Columns and Average Red Light Violations to Rows to create a scatter plot. 
- Drag ZipCodes on Label and Average Speed Violations on Size. Edit the shape to circle. This populates data on the scatter plot by adding circles based on average number of speed violations committed.
- Click on nulls on the chart and filter out null values.
- Click on the ZipCodes filter card and select Hide Card to remove it from the chart.
- Click on Tooltip to edit aliases for values displayed when a user hovers on a circle on the chart. Use Zipcode, Average Speed Violations and Average Red Light Violations in the same order as aliases. (**Tip**) Order can be changed by cutting and pasting the entire row in the desired order.) 
- Remove gridlines.
- Edit title of the Speed Violations size card on the right to 'Average Speed Violations'.


< chart image>

From the scatter plot one can clearly see there is no correlation between speed camera violations and red light violations in a zipcode. Zipcodes with the highest and lowest speed violations have nearly the same average number of red light violations. If there was a correlation then as the average number of speed violations would increase, the number of red light violations would increase too. Thus there would be more circles as one would move to right and top of the chart. But that relationship does not exist here.


- Add title 'There is no correlation between Speed violations and Red Light Violations among zip codes where these violations occurred'.
- Add Caption 'Average Speed Camera and Red Light Camera Violations across ZipCodes, 2014-19'. 

#### Create Dashboard for first finding

From the analysis and visualizations created above we see that there are no common grounds between the two automated enforcement programs run by the City of Chicago- Speed Camera and Red Light. There is a stark difference in the number of these violations committed and the overall trend over time period of study. 

Additionally, there is no relationship between zipcodes with high speed violations and their corresponding red light violations. Thus  these two programs are very distinct. Even though they are under the same umbrella of automated enforcement, they need to be treated differently. This is most important from a fund allocation perspective. Maybe the city can consider dividing the programs into disitnct intiatives to ensure proper fund allocation to meet each program's needs. 

**Creating the dashboard**
To create a dashboard for this finding, open a new dashboard worksheet in Tableau. Change the Dashboard layout to Floating which allows the user to resize and freely place charts on the dashbord. 
- Select P_No of violations over years sheet and drag it onto the dashboard. Resize to fit it to the upper left corner below title. Chart can be moved around the dahsboard by clicking on the sheet until the drag icon appears.
- Add the remaining worksheets in the same order of charts created above. I have added the charts in left to right direction of reading.
- Hide all filter and legend cards except Violation Type legend card from chart 3 and Average number of violations legend from Chart 4.
- Add title to the dashboard with a clear message about the finding. 
- Add captions to charts if not displayed automatically. I have not added Caption for the Average Violations by Zipcode chart since the chart seemed self-explantory and adding Caption was taking a lot of space on the dashboard.
- Captions should be center aligned to display right below the x-axis. Looked better than left alignment.
- Chart titles should be font size 11. I removed bold formatting from the titles and found that the dashboard looked more clean and easier to read. I didn't want to the get distracted by individual chart titles and not read the overarching message of the dashboard.
- Axis labels can be formatted by right clicking on the label and selecting Format. In the Axis Option, under Title, click on Font and change font size to 8.
- Move the legends to the right, and onto white space. Since I have used the same color scheme for all my charts, one legend would suffice to explain the difference in colors. 
Add the four charts created above to a dashboard.






