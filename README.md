# Google-Analytics-certificate_LeonorDuarte
# Leonor Duarte - Portfolio
## About
Hi, I’m Leonor! I have a strong academic foundation in Management and Marketing Intelligence and am currently pursuing a Master’s in Data-Driven Marketing. My passion lies in combining data analytics and strategic insights to solve real-world problems. I am excited to bring my technical and analytical skills to the fields of data science and project management as an entry-level data specialist and project leader.

During my studies, I honed my ability to work with complex datasets and developed a knack for identifying patterns and actionable insights. I’ve also gained hands-on experience in data visualization, statistical analysis, and workflow optimization, which I believe are key assets in supporting impactful decision-making. Certifications like the IBM Data Science Specialization and Scrum Master further complement my skills.
This is a repository to showcase skills, share projects and track my progress in Data Analytics / Data Science related topics.

# Summary of This Repository
## Completed Courses 
- **Course 1:** Foundations: Data, Data, Everywhere
- **Course 2:** Ask Questions to Make Data-Driven Decisions
- **Course 3:** Prepare Data for Exploration
- **Course 4:** Process Data from Dirty to Clean
- **Course 5:** Analyze Data to Answer Questions
- **Course 6:** Share Data Through the Art of Visualization
- **Course 7:** Data Analysis with R Programming
- **Course 8:** Google Data Analytics Capstone: Complete a Case Study

In the **Google Data Analytics Professional Certificate**, I learned how to work with data from start to finish. I got a solid understanding of what data is, how to analyze it, and how it fits into a bigger ecosystem. The course taught me to think analytically—breaking down problems, asking the right questions, and using data to make decisions. I gained hands-on experience with tools like spreadsheets for organizing and calculating data, SQL for working with databases, and Tableau for creating visualizations to share insights. I also learned about cleaning messy data to make it usable and the importance of avoiding biases when collecting and analyzing information.
One of the highlights was diving into R programming, where I created visualizations and reports using R Markdown.

# Case Study 1: How Does a Bike-Share Navigate Speedy Success?
> In the Course 8: Google Data Analytics Capstone: Complete a Case Study, I was able to put into practice what I learned throughout the certificate. The scenario says I'm working at Cyclistic, a fictional company, and I must fulfil a business task. To do so, I will follow the six phases of the data analysis process: **ask**,**process**,**analyse**,**share**, and **act**. My analysis aims to provide actionable insights that can be leveraged to enhance Cyclistic’s marketing approach and drive the conversion of casual riders into more profitable annual members

## Scenario
I am a junior data analyst working in the marketing analyst team at Cyclistic, which is a bike-share company in Chicago. Lily Moreno who is the director of marketing and also my manager, believes the company’s future success depends on maximizing the number of annual memberships. Therefore, my team wants to understand how casual riders (Customers who purchase single-ride or full-day passes) and annual members (Customers who purchase annual memberships) use Cyclistic bikes differently. From these insights, my team will design a new marketing strategy to convert casual riders into annual members. But first, Cyclistic executives must approve my recommendations, so they must be backed up with compelling data insights and professional data visualizations.

**Stakeholders**
•	Primary: Director of Marketing, Marketing analytic team
•	Secondary: Cyclistic Executive team

## My Approach

To achieve our marketing goal of converting casual members, and ultimately profit, we asked three questions:
- HOW annual members and casual riders differ?
- WHY would casual riders buy a membership?
- HOW can digital media affect marketing tactics?

With these three questions, we set the stage going by the data analysis process roadmap (Ask, Prepare, Process, Analyse, Share, and Act). we used spreadsheets, SQL, Tableau, and R to address the cleaning, analysis and visual requirement at each phase of the project.
Documentation and reports were also provided to support our work and recommendations.

**Note:  Although it was advised to use only SQL, RStudio and Tableau, I decided to do also in Python for my own practice.**

[Python](https://github.com/leonorduarte/Google-Analytics-certificate_LeonorDuarte/blob/main/1.%20Complete%20Analysis_LD%20(1).ipynb)
[SQL](https://github.com/leonorduarte/Google-Analytics-certificate_LeonorDuarte/blob/main/Google%20Data%20Analytics%20Capstone_%20LD%20(1).md)


## Prepare
### Data Source
I will use Cyclistic’s historical trip data to analyze and identify trends from Jan 2023 to Dec 2023 which can be downloaded from [divvy_tripdata](https://divvy-tripdata.s3.amazonaws.com/index.html). The data has been made available by Motivate International Inc. under this [license](https://www.divvybikes.com/data-license-agreement).  
  
> This is public data that can be used to explore how different customer types are using Cyclistic bikes. But note that data-privacy issues prohibit from using riders’ personally identifiable information. This means that we won’t be able to connect pass purchases to credit card numbers to determine if casual riders live in the Cyclistic service area or if they have purchased multiple single passes.

### Data Organization
There are 12 files with naming convention of YYYYMM-divvy-tripdata and each file includes information for one month, such as the ride id, bike type, start time, end time, start station, end station, start location, end location, and whether the rider is a member or not. The corresponding column names are ride_id, rideable_type, started_at, ended_at, start_station_name, start_station_id, end_station_name, end_station_id, start_lat, start_lng, end_lat, end_lng and member_casual.

## Process

Here are the steps that I followed during this phase:
1. Combined all the tables into one data table
2.Check for null and duplicates
3. Cleaned the data
4. Additional columns and data transformation
4. Extract data for analysis

### Data Cleaning
[Python](https://github.com/leonorduarte/Google-Analytics-certificate_LeonorDuarte/blob/main/2.%20Data%20Cleaning_LD%20(2).ipynb)  
[SQL](https://github.com/leonorduarte/Google-Analytics-certificate_LeonorDuarte/blob/main/Google%20Data%20Analytics%20Capstone_%20LD%20(1).md)
  
## Analyse and Share

Data Visualization
[Python](https://github.com/leonorduarte/Google-Analytics-certificate_LeonorDuarte/blob/main/3.%20Data%20Visualization_LD%20(2).ipynb)  
[SQL](https://github.com/leonorduarte/Google-Analytics-certificate_LeonorDuarte/blob/main/dashboard%2C%20a%CC%80s%2022.04.55.pdf)

### Analysis Results
**How do annual members and casual cyclists use Cyclistic bikes differently?**
-The analysis indicates that annual members have more stable usage patterns, suggesting regular commutes, while casual cyclists show more pronounced variations, indicating more flexible and recreational use. Preferences for initial stations and distinct destinations suggest distinct needs.

**Why would casual cyclists purchase annual memberships from Cyclistic?**
-Strategies to attract casual cyclists to annual subscriptions include offering exclusive benefits, significant discounts for longer periods, and seasonal promotions to encourage conversion.

**How can Cyclistic use digital media to influence casual cyclists to become members?**
-Digital campaigns highlighting exclusive benefits, persuasive content shared on social media, and exclusive offers, such as free trial periods, can be effective in attracting casual cyclists.



## Act
Based on the analysis, which included exploring ride patterns across different times (hours, days, months), ride durations, and bike preferences, some clear trends emerged:
- Casual riders primarily used bikes for leisure activities.
- Members were more likely to use bikes for routine commutes, like going to work.
- Casual riders took rides that were 2.5–3 times longer than those of members.
- The busiest days for riders were weekends.
- The busiest months were in the summer (June–August), likely due to the warmer weather.

With the main objective of converting casual riders into annual members, here are **my top three recommendations**:
1. Offer special deals for longer ride durations
Since casual riders tend to take longer rides for leisure, introducing membership plans that cater to extended ride durations could appeal to them.
For example, an annual membership that includes perks like discounted hourly extensions or unlimited longer rides could attract these riders.
2. Introduce seasonal or weekend-specific membership offers
Casual riders are most active during summer months and on weekends, which suggests these times are ideal for targeted promotions.
Offer short-term memberships specifically for the summer or weekends. For instance, a three-month "Summer Pass" or a "Weekend Pass" could encourage casual riders to try memberships.
After the short-term memberships end, follow up with discounted upgrades to annual plans to retain these riders.
3. Enhance bike facilities during winter months
Winter conditions like snow and cold temperatures drastically reduce ridership. To address this, improving bike infrastructure can make riding more appealing.
Collaborate with local authorities or partners to ensure bike paths are cleared and maintained during winter. This would encourage year-round usage and make memberships more attractive for both casual and routine riders.


