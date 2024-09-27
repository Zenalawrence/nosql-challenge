# nosql-challenge

## Summary

This assignment involves data exploration and analysis utilizing PyMongo. The data is sourced from the UK Foods Standard Agency, which assesses various establishments across the United Kingdom and assigns them a food hygiene rating. The task is to analyze some of the ratings data as requested by the editors of the food magazine, Eat Safe, Love to determine the focus for future articles.

The assignment is divided into three parts. 
1. Establish the database and connection to each collection in NoSQL_setup_solved.ipynb.
2. Modify specific records and fields within the database collection.
3. Exploratory analysis on the documents within the databases done in NoSQL_analysis_solved.ipynb.



## Part 1: Database and Jupyter Notebook Setup

The data was loaded from the establishments.json file, which was imported the terminal using the code

`mongoimport --type json -d uk_food -c establishments --drop --jsonArray establishments.json`.

The dependencies PyMongo and Pretty Print were then imported and an instance of the Mongo Client is created. The databases in MongoDB are listed to confirm that "uk_food" is present and their collections to ensure that "establishments" is included. To ensure everything is functioning correctly, one of its documents is printed for review using find_one().



## Part 2: Update the Database

The database was updated to include a new Halal restaurant in Greenwich, "Penang Flavours".

A new dictionary was created with details about the restaurant, and then inserted into the existing collection using insert_one(). A query was then done to identify the BusinessTypeID for "Restaurant/Cafe/Canteen," which was then used to update the BusinessTypeID for "Penang Flavours".

All Dover establishments were removed as per the magazine's request using delete_many(). 

Lastly, latitude and longitude data were converted from string to float, and RatingValue to integer using update_many().



## Part 3: Exploratory Analysis

A thorough analysis was conducted to respond to specific inquiries from the magazine to know where to visit and avoid.

**RatingValue**: The overall rating determined by the Food Authority, ranging from 1 to 5; higher values indicate better ratings. 
**Hygiene, Structural, and ConfidenceInManagement Scores**: High scores indicate worse conditions in these areas and vice versa.

The database is explored to answer the following questions:

**1. Which establishments have a hygiene score equal to 20?**
This was done by creating a query to find all hygiene scores = 20. Count_document() was then used to determine how many establishments contain this score and the first document was printed. The results were transformed into a Pandas DataFrame, and the number of rows is printed.

**2. Which establishments in London have a RatingValue greater than or equal to 4?**
A query was created to find all establishments located in London with a RatingValue of 4 or higher. Count_document() was then used to determine how many establishments contain this score and the first document was printed using pprint. This data was then transformed into a Pandas DataFrame.

**3. What are the top 5 establishments with a RatingValue of 5, sorted by lowest hygiene score, nearest to the new restaurant added, "Penang Flavours"?**
The latitude and longitude of "Penang Flavours." were found and then a search to find the closest locations within 0.01 degree. A query was then done to find establishments near "Penang Flavours" with a RatingValue of 5, sorted by the lowest hygiene score and limited to five results. 

**4. How many establishments in each Local Authority area have a hygiene score of 0? Sort the results from highest to lowest, and print out the top ten local authority areas.**

A pipeline was created with a match, group, and sort query. A match query to identify establishments with a hygiene score of 0, a group query to categorize them by their Local Authority Area and aggregated all documents in each group to calculate the total number of establishments with a hygiene score of 0 in each area.  Lastly, a sort query to sort the values from highest to lowest.