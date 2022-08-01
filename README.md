# Maven Telecom - Customer Churn Analysis with SQL and Tableau

One of my favourite things about the field of data analytics is the process of turning data into actionable items that make a difference for businesses. A few weeks ago, thanks to Maven Analytics, I got my hands on the churn data of a telecom company, and performed a customer churn analysis with the goal of identifying high value customers/churn risks and improving customer retention in mind.

As usual, I love doing data pre-processing and EDAs in SQL before moving onto Tableau to share my findings.

## Data Exploration and Storytelling

The main question that drives the analysis is straightforward — how do we plug the hole of revenue loss resulting from customer churn, especially from the churn of high value customers.

With our main question in mind, I needed to have an idea of the KPIs to monitor. I chose to measure churn by revenue instead of number of customers. There are also more than one way to look at revenue — total (lifetime) revenue, average monthly revenue and monthly charges.

The first question I needed to answer was what makes a customer high value. The main factors are: tenure, number of referrals (which are very valuable to the business), how much they spend on our services, how much revenue potential they have. The vizQL (Tableau’s version of SQL) formula to determine whether a customer is high value looks like this:

IF [Total Revenue] > {FIXED: PERCENTILE([Total Revenue], 0.5)} 
AND [Contract] != “Month-to-Month” 
AND [Number of Referrals] > 0
THEN TRUE
ELSE FALSE
END

Next, I singled out the top five (not including “don’t know”) churn reasons and related each one of them to aspects of our business operations in order to come up with actionable items (for example: for customers who left for competitors due to download speed, I looked at their internet type). I drilled it down (in Tableau) to the value status of the customers.

Here’s the [SQL code](https://github.com/yao-sisi/maven_churn_analysis/blob/main/maven_churn_mysql_code) with my thought process as comments.

Here’s the [Tableau Viz](https://public.tableau.com/views/CustomerChurnAnalysis-Maven/Dashboard1?:language=en-US&:display_count=n&:origin=viz_share_link) presenting my findings and recommendations (interactive).

<img align="left" width="750" height="1500" src="https://miro.medium.com/max/700/1*HdZsw1V1tZ7O8J0y--403A.png">
