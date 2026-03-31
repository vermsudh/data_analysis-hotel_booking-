Data Analysis Project

Steps

* ﻿﻿Create a Problem Statement.
* ﻿﻿Identify the data you want to analyze.
* ﻿﻿Explore and Clean the data.
* ﻿﻿Analyze the data to get useful insights.
* ﻿﻿Present the data in terms of reports or dashboards using visualization.

---

Making the jupyter Notebook

1) Importing all the important libraries.

   ***import pandas as pd
   import matplotlib.pyplot as plt
   import seaborn as sns
   import warnings
   warnings.filterwarnings('ignore')***
2) Loading the dataset
   ***df = pd.read_csv('hotel_booking.csv')***
3) Exploratory Data Analysis and Data Cleaning
   In order to read the data, we can use
   df = pd.read_csv('hotel_booking.csv')

    You can use df.head() to see the first five rows and cols
	Similarly, you can see df.tail() to observe the last five rows and cols.
	If you pass a value to in it, you can see that many rows. ex: df.head(10) will display 10 rows from top

    df.shape will tell you how many total rows and col are present in the dataset (csv file)
    df.columns will assist you to view all the col in the csv files.
    df.info() can help you to provide the information on database that is being used.

    Now, we have observed that we dont have the reservation_status_date in right format which should be datetime
	We will conver this first by***df['reservation_status_date'] = pd.to_datetime(df['reservation_status_date'])) ref: 		       image_2**
*
	In order to see the object values, we can use describe function
		df.describe(include = 'object')
	

In order to find the categories in the object col, for that we would have to use a for loop.
	**for col in df.describe(include = 'object').columns:
              print(col)
              print(df[col].unique())
		**

    #unique is a function that we can use in the dataframe.

***Now, We will check the missing values :* **

    df.isnull().sum() : This will return all the columns and the total values of each rows which are missing.

When we ran this statment, we found out that the missing data is majorly in two cols : agent and company

Since, we do not need this data, we are going to remove these two columns.

In order to do that, we are going to use :

    df.drop(['company', 'agent'], axis = 1, inplace = True)

    axis=1 : In order to make changes in the dataframe

    df.dropna(inplace = True) : This will remove all the cols that have missing values.

In order to view the summary stastics : we will use -> df.describe()

Now, we are going to remove the outliars

4) Data anlysis and visualization
   Lets check the amount in the dataset which are cancelled.
   For that we can use:
   **cancelled_perc = df['is_canceled'].value_counts(normalize = True)
   cancelled_perc**

    value_counts is a function that returns category_name and how many times it is present in the column.


**plt.figure(figsize=(8,4))
ax1 = sns.countplot(x='hotel', hue='is_canceled', data=df, palette='Blues')**

**ax1.legend(bbox_to_anchor=(1,1))**

**plt.title('Reservation status in different hotels', size=20)
plt.xlabel('hotel')
plt.ylabel('number of reservations')**

**plt.show()**

This wil tell us the visual representation of the data.

Now, in order to find the percentage oh how many hotels we being canceled.

***resort_hotel = df[df['hotel'] == 'Resort Hotel']
resort_hotel['is_canceled'].value_counts(normalize = True)***

***resort_hotel = df[df['hotel'] == 'City Hotel']
resort_hotel['is_canceled'].value_counts(normalize = True)***
