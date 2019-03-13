---
layout: project_single
title:  "Kaggle Popularity"
slug: "kaggle"
---


## Background:

Kaggle is an online community of data scientists and machine learners that was acquired by Google in 2017. Kaggle allows users to find and publish data sets, explore and build models in a web-based data-science environment, work with other data scientists and machine learning engineers, and enter competitions to solve data science challenges.

### Scraping Work:

For this scraping project, I wanted to scrape a website that wasn't scraped many times before. It took quite a number of tries to get the right framework for what I wanted to do. I started working with Json calls but switched over to  Scrapy, Beautiful Soup, and finally made the decision of utilizing Selenium for this project as the infinite scroll of Kaggle Kernels page was creating problems with other frameworks. You can see my code here.

### Data Collected:

I scraped over 5000 kernels, sorted by vote count as well as ~1500 user pages. I also scraped ~100K kernels as supporting data to combine with the data I scraped so that I could see more finely tuned results. The data included:

#### Kernels
* User Name
* Author Performance Tier
* Best Public Score
* Language
* Execution Time
* Medal
* Output Types
* Date Created
* Kernel Name
* Comment Count
* Vote Count

##### Users (Utilized the user profile URL from the kernels I scraped)
* User Name
* Date Joined
* Follower_count
* Title
* Location
* User Type
* Bio

### Challenges:

My first try with Scrapy left much to desire since the website uses infinite scroll, and I needed to utilize a plug in of Scrapy called Scrapy Splash. My research about the Splash package showed me that it wasn't very easy to use or efficient, so I needed to find another  framework that would work more quickly and efficiently. Thus, Selenium came into the mix.

Another challenge was uncovering the tags. I had difficulty at first because the way Kaggle's html is structured,  the tags are buried deep under other tags. Consequently I didn't always get the text/attributes I needed. With a little tweaking and a new loop, I started getting the data I needed, albeit slowly, as I didn't want to overload the website with my requests.

### Scraping Work:

I wanted to scrape both the top Kernels page as well as the user profiles who submitted the Kernels. To achieve that  I created two  loops.  The first scraped the Kernels page while collecting the URL of the profiles of users, and the second loop scraped the user pages with URLs from the Kernels scrape work. This approach made it easy to track what was being scraped while maintaining  data integrity.

### Analysis:

Once the data was cleaned, the first step was to take a look at the correlation between the numbers in the data to see what I should be focusing on in my analysis.

![Heatmap](static/projects/k_heatmap.png){:class="img-responsive"}

As expected, the vote count and the comment count are directly correlated. I thought about including the follower count of users in this analysis but decided against it because only the handful of top users have a decent number of followers and even those numbers are too small to be meaningful.

From the ~100k kernels I used in my analysis, it was interesting to see that there are 5 times more tier 5 users than tier 4 users. Kaggle defines performance tiers based on the amount of work a user puts in in kernels, competitions and discussions.

Kaggle having more kernels written in Python is not surprising as Python is arguably the most popular language for data science.

Vote count per performance tier

This graph shows the mean vote count per performance tier. This is very interesting as I'd expect the performance tier 5 users to collect more votes compared to other users. As the second part of this project, I will be looking more  deeply into the reasons of this finding.

The graph above shows us the mean vote count for each language. Unexpectedly, we see that kernels written with R collected more votes compared to kernels written with Python. What we learn here is that even though Python is the most preferred language in kernels, it didn't always translate into more votes. I will be spending more time on this data in the second part of my project. There may be outliers which skew the data.

Another surprising result. For visualizations,the  Kaggle community prefers R over Python. Again, this will be an area I'll be investigating further.
In the last part of my analysis, I wanted to create a map of the locations for the top 1000  Kaggle users. Normally, this is an interactive map, and the interactive part will be updated later in the blog. In the second part of my project, I will be doing a deeper dive and create more maps that show where different user groups (based on their Kaggle status) contribute to Kaggle.

To be investigated further: (with more data)
How does the follower & following count impacts the distribution of votes & comments a user receives?
More detailed user tier distribution
Distribution of vote count per user tier and why Tier 4 users collect more votes per kernel?
Why kernels written in R collect more votes compared to kernels written in R? Are there outlier kernels that have an impact on this finding?
Why the R users create more visualizations compared to Python users?
The distribution of user types from each country. For example, are more kernel experts to be found in the USA or in India? 
