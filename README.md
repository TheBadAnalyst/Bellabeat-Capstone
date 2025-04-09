
# **Bellabeat Case Study: Data Analysis & Insights**  
📊 *Google Data Analytics Capstone Project*  

## **📂 Project Overview**  
### **The Task**  
As a junior data analyst at Bellabeat, my goal is to analyze fitness data from smart devices to uncover user behavior insights. These insights will help refine Bellabeat’s marketing strategy, which I will present to the executive team.  

### **About Bellabeat**  
Bellabeat is a growing tech company founded by Urška Sršen and Sando Mur. It specializes in developing wellness products for women, including the **Leaf, Time,** and **Spring**—smart devices that track health metrics to improve users’ quality of life.  

### **Data Source**  
This analysis is based on the **highly credible** [FitBit Fitness Tracker Data](https://www.kaggle.com/datasets/arashnic/fitbit), collected via an Amazon Mechanical Turk survey from December 3–5, 2016. The dataset provides valuable insights into user activity, sleep, and health trends, making it an excellent resource for this study.  

## **📜 Datasets**  
- **Raw Data:** [Uncleaned Fitbit data 1.](dailyActivity_merged.csv)
- **Raw Data:** [Uncleaned Fitbit data 2.](hourlyCalories_merged.csv)

dailyActivity_merged and hourlyCalories_merged were both cleaned in excel
   
- **Cleaned Data:** [Fitbit data 1.](BellaBeat-DailyActiveCLEAN.csv)
- **Cleaned Data:** [Fitbit data 2.](BellaBeat-HourlyCaloriesCLEAN.csv)

## **🛠 Tools**  
- **Excel** – Initial data cleaning 
- **SQL** (MySQL Workbench) – Analysis  
- **Tableau Public** – Data visualization  
 

## **🔎 Key Insights**  
### **Activity & Calorie Trends**  
- **Calorie peaks**: 9 AM (primary) & 5-8 PM (secondary).
- **Sedentary users**: 1 in 4 users averaged less than 5000 steps a day.   

## **📊 Data Visualizations**  
- **[Calories By Hour](#)** *([Tableau Link](https://public.tableau.com/views/BellaBeatsInsights-caloriesbyhour/CaloriesByHour?:language=en-GB&publish=yes&:sid=&:redirect=auth&:display_count=n&:origin=viz_share_link))* 
- **[User Distribution by Activity Group](#)** *([Tableau Link](https://public.tableau.com/app/profile/jonathan.byrne7960/viz/UserDistributionbyActivityGroup/UserDistribution?publish=yes))*  

## **⚙️Coding and Queries** 
To identify peak activity times, I used this SQL query to extract hourly calorie burn data.

```sql
SELECT 24htime, SUM(calories) AS calories
FROM hourlycaloriesclean
GROUP BY 24htime 

```

[Catrine Tudor-Locke's study](https://pubmed.ncbi.nlm.nih.gov/14715035/#:~:text=Authors,1%20%2C%20David%20R%20Bassett%20Jr) proposes categorizing individuals into five activity levels based on their daily step count: Sedentary (<5000), Low Active (5000-7499), Somewhat Active (7500-9999), Active (10000-12499), and Highly Active (>12500). 
For simpler analysis, users were grouped into three broader categories – Sedentary, Normal, and Active – using the following SQL query 
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

Catrine Tudor-locke's study suggests putting people into 5 buckets.

 - Sedentary
 - Low Active
 - Somewhat Active
 - Active
 - Highly Active
## **📌Reccomendations**

### Marketing Recommendations Based on User Activity Levels and Peak Activity Times:###

To optimize user engagement and promote healthier habits, we recommend implementing targeted strategies for different activity levels, considering the identified peak activity times around 9 am and 5-8 pm .

**Push Notification Timing:**

Push notifications should be strategically delivered around 8 am and 4 pm. These times precede the daily calorie burn peaks, suggesting users may be more receptive to activity prompts leading up to their naturally more active periods.

Targeted Strategies for Each User Group:

Each user group will be engaged with tailored approaches:

1. Targeting the 'Normal' Group:

This group represents over 50% of our market, warranting a significant portion of our marketing efforts. Strategies for this segment will include:

* Milestone tracking to celebrate progress.
* Community-based competitions to foster engagement and motivation.
* Daily goals and challenges to encourage consistent activity.
  
2. Targeting the 'Sedentary' Group:

Comprising 25% of our users, this group is of critical importance due to the significant health risks associated with a sedentary lifestyle. Our primary goal is to guide these users towards the 'Normal' activity group. We can achieve this by:

* Gamifying the user experience with reward systems for achieving small activity goals.
* Offering bonus rewards for logging activities completed with a friend to encourage social support.
3. Targeting the 'Active' Group:

These users are already invested in their fitness. Our strategy for this group will focus on:

* Promoting a premium account that offers advanced health metric tracking for deeper insights.
* Encouraging users to share their achievements on social media using Bellabeat products for a chance to win prizes, leveraging their enthusiasm for fitness and social recognition.
By implementing these targeted strategies, Bellabeat can effectively engage each user segment with relevant and motivating content, ultimately fostering a more active and healthier user base.
