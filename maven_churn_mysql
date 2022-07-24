# in this analysis, our goal is to improve retention by identifying high value customers and churn risks

# I will analyze the churn by revenue, I think this is the most impactful way to analyze churn and improve retention
# my thought process goes like this: 
# 1. who are our most valuable customers - what are their profile/how are they spending their money (with us)
# 2. why are they leaving and how do we retain them


-- with the above in mind, we shall begin exploring

# Total churn (by total revenue)
select
  sum(Total_Revenue) as total_revenue,
  sum(case when Customer_Status = 'Churned' then Total_Revenue else null end) as churned_revenue,
  sum(case when Customer_Status = 'Churned' then Total_Revenue else null end) / sum(Total_Revenue) as churned_rev_perc
from
  customer
;
# churned customers are responsible for 17% of the company's total revenue, that is significant

# what are customers churning for? (churn category) using window functions to show %

select 
  Churn_Category,
  count(*) as no_cust,
  count(*)/sum(count(*)) over () as pct
from
  customer
where
  Customer_Status = 'Churned'
group by
  Churn_Category
order by
  no_cust desc
;

# I also want to look at churn category from the revenue standpoint
select
  Churn_Category,
  sum(Total_Revenue) as churned_rev,
  sum(Total_Revenue)/sum(sum(Total_Revenue)) over () as pct
from
  customer
where
  Customer_Status = "Churned"
group by
  Churn_Category
order by
  churned_rev desc
;

# quite consistent with what was found with # of customers

# Total revenue is still not ideal in measuring the value the business loses when a customer churns
# I want to use average monthly revenue from a customer, take the average per churn category
# to see which kind of churn costs the company the most

select
  Churn_Category,
  avg(Tenure_in_Months),
  avg(Total_Revenue/Tenure_in_Months) as monthly_rev_churned
from
  customer
where
  Customer_Status = "Churned"
group by
  Churn_Category
order by
  monthly_rev_churned desc
;

# monthly rev numbers are quite clear to each other but Competitor remains the most expensive kind of churn
# average tenure by the time of churn is quite close to each other as well
# looks like customers generally care the least about Price but most about Attitude

# out of curiosity, what are the exact reasons when we lose customers
select
  Churn_Reason,
  Churn_Category,
  count(Customer_ID) as no_cust,
  count(Customer_ID)/sum(count(Customer_ID)) over () as pct
from
  customer
where
  Customer_Status = "Churned"
group by
  Churn_Reason,
  Churn_Category
order by
  no_cust desc
;

# by average monthly rev?
select
  Churn_Category,
  sum(Total_Revenue/Tenure_in_Months) as avg_mo_rev
from
  customer
where
  Customer_Status = "Churned"
group by
  Churn_Category
order by
  avg_mo_rev desc
;



# so the main reasons we lose customers are:
# to competitors are "better devices" and "better offer"
# our support person has bad attitude

# for reason #1 (better devices), it's logical to conclude and suggest that we work on the quality of our own
# for reason #2 we are going to look at which one of our offers were 'not enough' to retain customers

select
  Offer,
  count(Customer_ID) as no_cust,
  count(Customer_ID)/sum(count(Customer_ID)) over () as pct
from
  customer
where
  (Customer_Status = 'Churned' and Churn_Reason = 'Competitor made better offer')
group by
  Offer
order by
  no_cust desc
;
# about 56% of customers who churned because of better offers elsewhere had either no offer
# another 25% of them had Offer E

# for reason #3 - Attitude of support person, let's look at the Premium_Tech_Support col
select
  Premium_Tech_Support,
  count(Customer_ID) as no_cust
from
  customer
where
  Customer_Status = 'Churned'
group by
  Premium_Tech_Support
;
# majority of them did not have premium tech support


# next I want to take a look at contract type of churned customers
select
  Contract,
  count(Customer_ID) as no_cust
from
  customer
where
  Customer_Status = "Churned"
group by
  Contract
order by
  no_cust desc
;

# aha, vast majority of customers who churned were on a month-to-month deal with us

select
  distinct Churn_Reason
from 
  customer
where 
  Churn_Category = 'Other'
;






