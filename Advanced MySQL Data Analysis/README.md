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

# ✨ Analyzing Traffic Sources

## 📌 Finding Top Traffic Sources

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

<img width="500" alt="image" src="https://github.com/rohaanzuberi/Maven_Analytics/blob/main/Images/2.jpeg" width="500" height="200" />

The ```NULL``` records indicate traffic that has not been driven by a paid campaign.

<img width="500" alt="image" src="https://github.com/rohaanzuberi/Maven_Analytics/blob/main/Images/3.jpeg" width="500" height="400" />

## 📌 Traffic Source Conversion Rates

<img width="500" alt="image" src="https://github.com/rohaanzuberi/Maven_Analytics/blob/main/Images/4.jpeg" width="500" height="400" />

```SQL
SELECT
  COUNT(DISTINCT w.website_session_id) AS sessions,
  COUNT(o.order_id) AS orders,
  (COUNT(o.order_id) / COUNT(DISTINCT w.website_session_id)) * 100 AS CVR
FROM website_sessions AS w
LEFT JOIN orders AS o
USING (website_session_id)
WHERE
  w.created_at < '2012-04-14'
  AND utm_source = 'gsearch'
  AND utm_campaign = 'nonbrand';
```

<img width="500" alt="image" src="https://github.com/rohaanzuberi/Maven_Analytics/blob/main/Images/5.jpeg" width="500" height="100" />

<img width="500" alt="image" src="https://github.com/rohaanzuberi/Maven_Analytics/blob/main/Images/6.jpeg" width="500" height="400" />

## 📌 Traffic Source Trending

<img width="500" alt="image" src="https://github.com/rohaanzuberi/Maven_Analytics/blob/main/Images/7.jpeg" width="500" height="400" />

```SQL
SELECT
  -- YEAR(created_at) AS year,
  -- WEEK(created_at) AS week,
  MIN(DATE(created_at)) AS week_start_date,
  COUNT(DISTINCT website_session_id) AS sessions
FROM website_sessions
WHERE
  created_at < '2012-05-10'
  AND utm_source = 'gsearch'
  AND utm_campaign = 'nonbrand'
GROUP BY
  YEAR(created_at),
  WEEK(created_at);
```
<img width="400" alt="image" src="https://github.com/rohaanzuberi/Maven_Analytics/blob/main/Images/8.jpeg" width="500" height="200" />

<img width="500" alt="image" src="https://github.com/rohaanzuberi/Maven_Analytics/blob/main/Images/9.jpeg" width="500" height="400" />

## 📌 Bid Optimization for Paid Traffic

<img width="500" alt="image" src="https://github.com/rohaanzuberi/Maven_Analytics/blob/main/Images/10.jpeg" width="500" height="400" />

```SQL
SELECT
	w.device_type,
    COUNT(DISTINCT w.website_session_id) AS sessions,
    COUNT(DISTINCT o.order_id) AS orders,
    (COUNT(DISTINCT o.order_id)/COUNT(DISTINCT w.website_session_id)) *100 AS CVR
FROM website_sessions AS w
LEFT JOIN orders AS o
ON w.website_session_id = o.website_session_id
WHERE
  w.created_at < '2012-05-11'
  AND utm_source = 'gsearch'
  AND utm_campaign = 'nonbrand'
GROUP BY
  w.device_type
ORDER BY CVR DESC;
```
<img width="400" alt="image" src="https://github.com/rohaanzuberi/Maven_Analytics/blob/main/Images/11.jpeg" width="500" height="100" />

<img width="500" alt="image" src="https://github.com/rohaanzuberi/Maven_Analytics/blob/main/Images/12.jpeg" width="500" height="400" />

## 📌 Trending w/ Granular Segments

<img width="500" alt="image" src="https://github.com/rohaanzuberi/Maven_Analytics/blob/main/Images/13.jpeg" width="500" height="400" />

```SQL
SELECT
  -- YEAR(created_at) AS year,
  -- WEEK(created_at) AS week,
  MIN(DATE(created_at)) AS week_start_date,
  COUNT(DISTINCT CASE WHEN device_type = 'desktop' THEN website_session_id ELSE NULL END) AS desktop_sessions,
  COUNT(DISTINCT CASE WHEN device_type = 'mobile' THEN website_session_id  ELSE NULL END) AS mobile_sessions
FROM website_sessions
WHERE
  created_at < '2012-06-09'
  AND created_at >= '2012-04-15'
  AND utm_source = 'gsearch'
  AND utm_campaign = 'nonbrand'
GROUP BY
  YEAR(created_at),
  WEEK(created_at);
```

<img width="400" alt="image" src="https://github.com/rohaanzuberi/Maven_Analytics/blob/main/Images/14.jpeg" width="500" height="200" />

<img width="500" alt="image" src="https://github.com/rohaanzuberi/Maven_Analytics/blob/main/Images/15.jpeg" width="500" height="400" />

# ✨ Analyzing Website Performance


