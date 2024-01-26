# Azure-cost-analysis-using-billing-data
## Overview
This project showcases my comprehensive solution for handling Azure billing data efficiently. Leveraging multiple CSV files, the project extracts pertinent information and transforms it into a format conducive to analysis. The extracted data is then utilized to construct a dynamic and interactive dashboard tailored to meet my client's specific requirements. Explore this repository to gain insights into effective utilization of Azure billing data and the creation of informative  dashboards to enhance decision-making processes.

## Client requirements
My client receives monthly billing data from Azure which comes in a csv file. He stores these csv files in the same directory. He wanted a Power BI dashboard to analyze Azure costs using this billing data. The dashboard was to enable flexible cost analysis based on "env" and "app" tags, as well as filters for month/year, subscription, resource, and resource type. The dashboard was also supposed to enable seamless loading of new CSV files, automatically updating the dashboard with new data i.e when a new csv file is added to the directory, the dashboard's data was supposed to be updated to include data from the new csv.<br><br>


I decided to use python to import the data into Power BI(Using the Python script source) so I can easily clean, transform, and concatenate the data from the different csv files using python, a tool that I understand its ins and outs clearly.

## Data cleaning and transformation

### The data
This is the format of the data in the CSV file. The contents are partially hidden to respect the client's privacy:<br><br>
![Excel file sample](./Images/ExcelFile.png)<br>
Each csv has the following columns and data for the month: ResourceGroup, ResourceGroupId, SubscriptionName, SubscriptionId, Resource, ResourceId, ResourceType, ResourceLocation, Tags, Cost, CostUSD,Currency , and Date for the month.


### Python Script
First, I imported the required modules;
1. Pandas: to clean, transform, and manipulate the data
2. Os: to read the csv files and interact with the files in directory

I also got a list of all the files in the directory/folder,<br><br>
![Modules and file import](./Images/ModulesImport.png)<br><br>

I created a dataframe called data that will store all the data from all the csv files.<br><br>
![Dataframe creation](./Images/Python2.png)<br><br>

I proceeded to read all csv files in the directory and append their data to the "data" dataframe. I added a column "filename" to show the filename of the csv where the data came from<br><br>
![Read all csv files](./Images/Python3.png)<br><br>

The "Tags" column contained data for the application and environment. In this row, for example, the application was mobapp and the environment was prd<br><br>
![Tags column](./Images/Python4.png)<br><br>

For each row, I had to extract the application and environment data from the tags data. This was a bit difficult because some tags were very long and complicated, like in this one.<br><br>
![Complicated tags column](./Images/Tagscomplicated.png)<br><br>

I created this workflow to handle this dynamic nature of the string. The code also had a try except block to prevent the code from breaking in case of null values or incomplete data.<br><br>
![Tags extraction code](./Images/Python5.png)<br><br>

I then added this extracted data into the "Application" and "Environment" columns of the "data" dataframe.<br><br>
![Adding the two columns](./Images/Python6.png)<br><br>

The client also wanted me to add two columns in the data; the price of each record's application for the previous two months from the date of the bill. For example a record in the November's bill,he wanted to know the price of the app in October and September. I used this code to find the price from the record in the respective two previous months.<br><br>
![Get previous months price](./Images/Python7.png)<br><br>

The data was now clean, well formatted, and ready to be used for visualization <br><br>

## Visualization using Power BI
### Data Import and cleaning
I imported the data using the python script method.<br><br>
![Power BI data import using Python script](./Images/PowerBIImport.png)<br><br>

Since the data was clean already, I used Power Query to ensure that the data had correct data types and had no errors.<br><br>
![Power Query](./Images/PowerQuery.png)<br><br>

### Visualization
These are the visualizations and insights I created, enriched with filters and drill-down capabilities.

#### Monthly trend
![Monthly trend](./Images/MonthlyTrend.png)<br><br>
#### Subscriptions
![Subscriptions](./Images/Subbscriptions.png)<br><br>
#### Resources
![Resource](./Images/Resources.png)<br><br>
#### Resource Types
![Resource types](./Images/ResourceTypes.png)<br><br>
#### Resource types Pie Chart
![Resource types Pie Chart](./Images/ResourceType2.png)<br><br>


In conclusion, this project reflects my proficiency in harnessing the power of Python for data cleaning, transformation, and extraction, and in file management, as well as showcasing my adept skills in crafting compelling data visualizations using Power BI. Through a blend of coding expertise and creative data storytelling, I have demonstrated the ability to turn raw datasets into meaningful insights. The project not only underscores my technical prowess but also reflect my commitment to delivering impactful solutions in the realm of data analytics. Your feedback and collaboration is always welcome as I continue to evolve and expand my capabilities in the dynamic field of data science.
