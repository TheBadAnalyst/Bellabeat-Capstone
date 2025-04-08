
# **Bellabeat Case Study: Data Analysis & Insights**  
📊 *Google Data Analytics Capstone Project*  

## **📂 Project Overview**  
### **The Task**  
As a junior data analyst at Bellabeat, my goal is to analyze fitness data from smart devices to uncover user behavior insights. These insights will help refine Bellabeat’s marketing strategy, which I will present to the executive team.  

### **About Bellabeat**  
Bellabeat is a growing tech company founded by Urška Sršen and Sando Mur. It specializes in beautifully designed wellness products for women, including the **Leaf, Time,** and **Spring**—smart devices that track health metrics to improve users’ quality of life.  

### **Data Source**  
This analysis is based on the **highly credible** [FitBit Fitness Tracker Data](https://www.kaggle.com/datasets/arashnic/fitbit), collected via an Amazon Mechanical Turk survey from December 3–5, 2016. The dataset provides valuable insights into user activity, sleep, and health trends, making it an excellent resource for this study.  

## **📜 Datasets Used**  
- **Raw Data:** [Uncleaned Fitbit data 1.](dailyActivity_merged.csv)
- **Raw Data:** [Uncleaned Fitbit data 2.](hourlyCalories_merged.csv)  
- **Cleaned Data:** [Fitbit data 1.](BellaBeat-DailyActiveCLEAN.csv)
- **Cleaned Data:** [Fitbit data 2.](BellaBeat-HourlyCaloriesCLEAN.csv)

## **🛠 Tools**  
- **Excel** – Initial data cleaning 
- **SQL** (MySQL Workbench) – Analysis  
- **Tableau Public** – Data visualization  
 

## **🔎 Key Insights**  
### **Activity & Calorie Trends**  
- **Calorie peaks**: 9 AM (primary) & 5-8 PM (secondary). (keep this)
- **Too many Sedentary users**: 25% of users were found to be Sedentary.   

## **📊 Data Visualizations**  
- **[Calories By Hour](#)** *([Tableau Link](https://public.tableau.com/views/BellaBeatsInsights-caloriesbyhour/CaloriesByHour?:language=en-GB&publish=yes&:sid=&:redirect=auth&:display_count=n&:origin=viz_share_link))* 
- **[User Distribution by Activity Group](#)** *([Tableau Link](https://public.tableau.com/app/profile/jonathan.byrne7960/viz/UserDistributionbyActivityGroup/UserDistribution?publish=yes))*  

## **⚙️Coding and Queries** 
The query used to find out the calories burnt by hour to find out when people are most active in the day
```sql
SELECT 24htime, SUM(calories) AS calories
FROM hourlycaloriesclean
GROUP BY 24htime 

```

Based on [Catrine Tudor-Locke's study](https://pubmed.ncbi.nlm.nih.gov/14715035/#:~:text=Authors,1%20%2C%20David%20R%20Bassett%20Jr) 

Which defines less than 5000 daily steps as a sedentary lifestyle, and over 10000 as an active lifestyle. Users were grouped into 3 buckets, Sedentary, Normal and Active, using this SQL query 
```sql
SELECT id,
ROUND(AVG(totalsteps),0) AS avg_steps,
CASE
    WHEN ROUND(AVG(totalsteps),0) < 5000 THEN 'Sedentary Group'
    WHEN ROUND(AVG(totalsteps),0) BETWEEN 5000 AND 10000 THEN 'Normal Group'
    ELSE 'Active Group'
END AS activity_group
FROM dailyactiveclean
GROUP BY id
ORDER BY avg_steps
```

