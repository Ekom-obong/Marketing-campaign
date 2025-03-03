# Marketing-campaign
## Project Overview
The project involves querying and analyzing a dataset containing campaign details, audience demographics, geographic reach, and marketing channel performance. Through SQL-based analysis, the report addresses critical questions, including identifying the most effective campaigns, top-performing locations, and the best-performing marketing channels. Key findings highlight trends in customer engagement, cost efficiency, and marketing impact, providing data-driven recommendations for improved campaign performance.
## Data Source
Campaign data: The primary data source used for this anlysis is the "Marketing_campaign_dataset.xlsx" file containing detail information about each campaign

## Tools
- SQL(PostgreSQL)

## Data cleaning and Preparation
- Imported the dataset into the database named postgre.

- Table renamed from marketing_campaign_dataset.xlsx to campaigndata.

- Data cleaning included type adjustments for the Acquisition Cost and Date columns.

## Exploratory Data Analysis
1. What is the total number of impressions for each campaign?

2. Which campaign has the highest ROI?

3. What are the top three locations with the most impressions?

4. What are the average engagement scores by target audience?

5. What is the overall click-through rate (CTR)?

6. Which campaign is the most cost-effective?

7. Which campaigns have a CTR above a given threshold?

8. How do marketing channels rank based on total conversions?

## Data Analysis and Insights
What is the total number of impressions for each campaign?
```Sql
select campaign_id  , sum(impressions)as totalimpressions 
from campaigndata  
group by campaign_id ;
```
Which campaign has the highest ROI?
```Sql
select campaign_id  , company  , roi 
from campaigndata 
order by roi  desc 
limit 1 ;
```
What are the top three locations with the most impressions?
```Sql
select location ,sum(impressions)as totalimpressions 
from campaigndata 
group by  location
order by totalimpressions desc 
limit 3;
```
What are the average engagement scores by target audience?
```Sql
select target_audience , avg(engagement_score) as avgengagementscore
from campaigndata  
group by target_audience ;
```
What is the overall click-through rate (CTR)?
```Sql
select (sum(clicks)::decimal/nullif (sum(impressions),0)) * 100 as overallctr 
from campaigndata  ;
```
 Which campaign is the most cost-effective?
 ```Sql
select campaign_id ,company ,(acquisition_cost / nullif (conversion_rate ,0)) as costperconversion
from campaigndata  
order by costperconversion asc
limit 1;
```
Which campaigns have a CTR above a given threshold?
```Sql
select campaign_id ,company, (clicks :: decimal/nullif (impressions,0))*100 as ctr
from campaigndata 
where  (clicks :: decimal/nullif (impressions,0))*100 >5;
```
How do marketing channels rank based on total conversions?
```Sql
select channel_used, sum(conversion_rate)as totalconversions 
from campaigndata 
group by channel_used 
order by totalconversions desc ;
```
## Key Findings

### Campaign Performance

Highest ROI: Campaign ID 168 by NexGen Systems achieved an ROI of 8.0.

Most Cost-Effective Campaign: Campaign 101103 by Alpha Innovations had the lowest CPA of 33,346.67.

High CTR Campaigns: Several campaigns exceeded the 5% CTR benchmark, indicating strong audience engagement.

### Geographical Insights

Top 3 Locations by Impressions:

New York: 221,359,756

Miami: 221,347,726

Chicago: 219,999,352

### Audience Engagement

Highest Engagement Scores:

Men 18-24: 5.5150 (highest engagement)

Women 25-34: 5.4927

Men 25-34: 5.4920

### Marketing Channel Ranking by Total Conversions

Top-Performing Channel: Email marketing, followed by Google Ads and Website traffic.

## Recommendations

- Scale High-ROI Campaigns: Replicate NexGen Systems’ approach for cost-effective marketing.

- Target High-Impression Locations: Allocate resources strategically in New York, Miami, and Chicago.

- Enhance Audience Segmentation: Leverage high engagement insights to optimize ad content.

- Optimize Marketing Channels: Continue leveraging email marketing while exploring improvements in other channels.


