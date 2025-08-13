# ADS4SJ

## Overview

Since 2014, CAHOOTS has acted as an alternative to 911 calls regarding welfare checks, mental health issues, and other emergencies. For over ten years they were the sole operators alongside Eugene PD until August 2024 when Mobile Crisis Services of Lane County (MCSLC) started service in Eugene.

MCSLC is similar to CAHOOTS - 911 operators could route calls to MCSLC that they thought might be a better fit than the police. MCSLC aimed to provide services to people experiencing immediate behavioral health crises. Though MCSLC focuses more specifically on mental health calls, the goal of my project was to explore the impact of MCSLC's services in Eugene on CAHOOTS call volume for the eight months that CAHOOTS and MCSLC were both in service in Eugene from August 2024 - March 2025.

By finding these associations, we can better understand how CAHOOTS and MCSLC could work together in the most efficient way to provide services to the people of Eugene.

**Research Question:** How did CAHOOTS call volume change in August of 2024 with the addition of Mobile Crisis Services of Lane County?

## Data

Rori Rofls from CAHOOTS provided the data for this project. It contained twelve individual CSVs of CAD data, one for each year from 2014 to 2025. The columns that I focused on in the data were:

- **Call time**
- **Prime unit**

I concatenated all the individual CSVs into one master CSV and then filtered all the rows to only calls where CAHOOTS was the primary unit. You can find my notebooks and scripts on GitHub, linked here.

## Methods

### Packages Used
- **Pandas**
- **NumPy**
- **Regular Expressions**
- **Seaborn**
- **Matplotlib**
- **SciPy Stats**
- **Statsmodels**

### Data Processing
The first thing I did after combining all the CSVs was begin to explore and clean the data. At the beginning of my project, I wasn't sure exactly where my project would take me so I:

1. **Cleaned the 'nature' column** - combining all unique natures that didn't make over 1% of the data into an 'other' category
2. **Cleaned the zip column** - in case I wanted to analyze where calls were being called from
3. **Engineered new time-based columns** - used the call time column to create new columns of hour, day of the week, month, and year so I could explore CAHOOTS call volume through time

### Analysis Approach
Moving onto my analysis, I plotted the associations between call volume and:
- Hour of the day
- Day of the week
- Month of the year
- Year

The first thing I noticed was the difference in CAHOOTS call volume through the years. From 2019 to 2022 CAHOOTS received a visually significant amount of calls over 2023-2024.

I decided to only look at CAHOOTS call volume from:
- **Pre-MCSLC:** August 2023 - August 2024
- **Post-MCSLC:** August 2024 - March 2025

The reason for this is I didn't want my analysis to be skewed by higher call volumes in 2022. Additionally, I didn't want to make my time frame any shorter to account for any seasonal bias in call volume.

**Important Note:** There was only post-MCSLC data for 8 months because those were the only 8 months CAHOOTS and MCSLC were in service in Eugene at the same time.

After filtering my data into these 20 months and labeling pre and post-MCSLC, I decided to conduct:
1. **Two-sample T-test**
2. **Difference in differences analysis**

To determine if the change in call volume was significant and the magnitude of the change. To do this I bootstrapped both daily and monthly call volume means from pre and post-MCSLC to compare against each other.

## Results

### Key Findings
- From 2020 until CAHOOTS stopped their services in Eugene in March 2025, CAHOOTS averaged about **51 calls per day**
- From August 2023 - August 2024 (pre-MCSLC): CAHOOTS averaged about **46-47 calls per day**
- After MCSLC started services in Eugene (post-MCSLC): CAHOOTS' call average went down to around **44-45 calls per day**

### Statistical Analysis
From this data we can see a difference in call volume, though the significance of the difference was determined through statistical testing.

In my analysis, I found that there was a **negative association** between MCSLC's services starting in Eugene and CAHOOTS call volume.

My two sample t-tests performed on bootstrapped daily and monthly averages pre and post-MCSLC showed that there was a **significant difference** in the call volume between the two samples with a **0.00 P-value**.

My difference in differences analysis concluded that there were:
- **1.7 fewer CAHOOTS calls per day** on average
- **60 fewer CAHOOTS calls per month**

After MCSLC started their service in Eugene, both with a **0.00 P-value**.

## Discussion

There are a couple of things to note about my results, as well as further analysis that I would like to do if the data became available.

### Interpretation of Results
My results showed that the introduction of MCSLC in Eugene resulted in a **decrease in CAHOOTS call volume**. However, I don't necessarily think that this is a bad thing. Though CAHOOTS and MCSLC are similar, I think that there's a way for them to coexist in Eugene that is beneficial to the public.

For example, we already know that:
- **MCSLC** is focused more on mental health calls
- **CAHOOTS** responds to a variety of different calls

### Limitations and Future Work
The issue right now is there's **not enough data** where CAHOOTS and MCSLC were both in service in Eugene. The data that we do have (which is only from CAHOOTS) does not describe the call type clearly and will often combine call types into broader categories.

With more time of both agencies operating in Eugene, and clearer data from both Eugene and MCSLC showing what type of calls they're responding to, I think an analysis could be done that could:

1. **Split up calls** more effectively
2. **Make both agencies run more efficiently**
3. **Optimize resource allocation** between the two services

## Usage

### Data Processing
- **`data_clean.ipynb`**: Must be in the same directory with a folder 'new_data' and have every year of new CAD data to run. This notebook will clean the CSV data.

### Analysis
- **`data_analysis.ipynb`**: Use `clean_data.csv` that will be saved to your working directory by running `data_clean.ipynb` to do the analysis on the now cleaned CAD data.

### Prerequisites
Must have these libraries installed:

```bash
pip install pandas numpy matplotlib seaborn scipy statsmodels
```


