# Analyzing-Crime-In-Los-Angeles
A Data-Driven Approach to Understanding Urban Crime Patterns

## 📖 Overview

Los Angeles, California — The City of Angels — is famous for its sunshine, beaches, and entertainment industry. However, like any major city, it faces significant challenges with crime.
This project explores real-world crime data from the Los Angeles Police Department (LAPD) to uncover patterns in criminal activity, helping optimize resource allocation and enhance public safety.

Using the crimes.csv dataset, this analysis applies Python and pandas to answer key questions about when and where crimes occur, and how victim demographics correlate with criminal incidents.

## 🎯 Objectives

The main goal of this project is to identify patterns in crime frequency across time, location, and victim demographics. Specifically, it answers:

### 🕐 Which hour has the highest frequency of crimes?
→ Store as: peak_crime_hour (integer)

### 🌃 Which area has the highest frequency of night crimes
(between 10 PM and 3:59 AM)?
→ Store as: peak_night_crime_location (string)

### 👥 How many crimes were committed against victims of different age groups?
→ Store as: victim_ages (pandas Series)
with the following index labels:

"0-17", "18-25", "26-34", "35-44", "45-54", "55-64", "65+"

## 🧩 Dataset Description

File: crimes.csv
Each record represents a reported crime in Los Angeles and includes details such as:

Column	Description
DR_NO	Crime record number
DATE_OCC	Date and time of the crime
AREA_NAME	Police area or district
VICT_AGE	Victim's age
VICT_SEX	Victim’s gender
CRIME_CODE_DESC	Description of the crime
LOCATION	Location type or description
## 🧠 Methods & Approach

Data Cleaning:

Parsed date and time columns

Removed missing or invalid entries

Feature Engineering:

Extracted the hour of occurrence

Defined “night crime” as occurring between 22:00 and 03:59

Created age group bins for victims

Exploratory Analysis:

Counted total crimes by hour and location

Aggregated crimes per age group

Results stored as Python variables:

peak_crime_hour = 22
peak_night_crime_location = "Hollywood"
victim_ages = pd.Series({
    "0-17": 320,
    "18-25": 1020,
    "26-34": 980,
    "35-44": 720,
    "45-54": 460,
    "55-64": 280,
    "65+": 150
})


(values above are examples — they will vary with your dataset)

## 🧰 Tools & Libraries
Tool	Purpose
Python	Data processing and analysis
pandas	Data manipulation and grouping
NumPy	Numerical computations
Matplotlib / Seaborn (optional)	Visualization of crime patterns
## 📊 Example Code
import pandas as pd

#### Load the dataset
df = pd.read_csv("crimes.csv")

#### Extract hour
df["hour"] = pd.to_datetime(df["DATE_OCC"]).dt.hour

#### 1. Hour with the highest crime frequency
peak_crime_hour = df["hour"].value_counts().idxmax()

#### 2. Area with highest night crime frequency (10pm–3:59am)
night_df = df[(df["hour"] >= 22) | (df["hour"] <= 3)]
peak_night_crime_location = night_df["AREA_NAME"].value_counts().idxmax()

#### 3. Crime frequency by victim age groups
bins = [0, 17, 25, 34, 44, 54, 64, 200]
labels = ["0-17", "18-25", "26-34", "35-44", "45-54", "55-64", "65+"]
df["age_group"] = pd.cut(df["VICT_AGE"], bins=bins, labels=labels, right=True)

victim_ages = df["age_group"].value_counts().reindex(labels)

## 💡 Insights

Crime peaks at night, especially around 10 PM – midnight.

Certain areas (e.g., Hollywood, Central LA) experience higher rates of nighttime crimes.

Younger victims (18–34) are the most frequent targets, suggesting higher exposure in nightlife or commuting hours.

## 🏁 Future Work

Add spatial mapping (e.g., using folium or geopandas) to visualize hotspots.

Perform seasonal or day-of-week analysis for time-based crime trends.

Integrate predictive modeling for resource planning.
