# E-Commerce Database Analysis Project

## The Situation

I have just been hired as an eCommerce Database Analyst for **Maven Fuzzy Factory**, an online retailer which has just launched their first product.

## The Brief

As a member of the startup team, I will work with the CEO, the Head of Marketing, and the Website Manager to help steer the business.

I will analyze and optimize marketing channels, measure and test website conversion performance, and use data to understand the impact of new product launches.

## The Objective

Use SQL to:
- Access and explore the Maven Fuzzy Factory database
- Become the data expert for the company, and the go-to person for mission critical analyses
- Analyze and optimize the business’ marketing channels, website, and product portfolio


## 📌 Analyzing Traffic Sources

<img width="500" alt="image" src="https://github.com/rohaanzuberi/Maven_Analytics/blob/main/Images/1.jpeg" width="500" height="400" />

```SQL
SELECT
  utm_source,
  utm_campaign,
  http_referer,
  COUNT(DISTINCT website_session_id) AS session
FROM website_sessions
WHERE created_at < '2012-04-12'
GROUP BY
  utm_source,
  utm_campaign,
  http_referer
ORDER BY session DESC;
```

