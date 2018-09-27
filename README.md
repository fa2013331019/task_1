# Task_1
My approach to solve Task 1 is as follows.

# First step:
First I analyzed the structure of "bdjobs.com". There is almost 200 pages in this website. Each of those page contains 20 jobs. These 200 pages might be found by scraping the "next" links in the webpage. And when one page is found then the 20 job links containing that single page can be found. Using those links it is possible to extract information from those job postings.

# Second step:
Then I selected the following features to extract.
1) Title
2) Category
3) Company Name
4) Job Responsibility
5) Vacancy
6) Employment Status
7) Educational Requirement
8) Additional Requirement
9) Job Location
10) Salary
11) Job Source

# Third step:
To implement my solution I wrote two spiders. One spider will crawl the "next page" links and save them in a text file. Another spider will fetch those links as start_urls and run through those job postings to extract feature.

# Problem with third step:
After writing those two spiders I realized that the "next page" link in every page wasn't actually a page. bdjobs.com is one among those ASP.NET sites which uses javascript buttons to create a form and load data in that form. So I couldn't get those "next page" attributes as links. Those were actually javascript forms.

I took following measures to virtually click on "next page":

1) Tried to use process_value(value) function in scrapy. But didn't succeed because this function assumes value will be a .html attribute hidden under a javascript function. In my case it was a form.

2) Tried to use splash. But didn't succeed because  clicking on the "next page" button no link attribute can be found. So splash didn't offer solution to my problem.

3) Googled a bit and found that the only way to click on those "next page" buttons was to do browser automation. I forked some browser automation tools like puppeteer to learn how to do this.

By this point a signification amount of time in my project completion time span had been elapsed. So I reminded a famous quote from Randy Pausch which was "Engineering isn't about perfect solutions; it's about doing the best you can with limited resources." and I decided to launch a brute force attack on the link patterns.

# Fourth Step:
Analyzed the link patterns I found that every job has a link in form of "http://jobs.bdjobs.com/jobdetails.asp?id=[int]&fcatId=1&ln=1" where int has a range between 780000 and 799999. So I wrote a spider which iterate a loop in this range to load the start_urls.

By this approach it took 1 hour to crawl informations from job postings. I scraped features from 25000 job posting . Which was about 70% of the crawlable jobs(jobs which don't contain info in image form). Feautures were extracted by analyzing the xpath patterns.

# Fifth step:
Then I organized my .txt file in a json format so that it is easy to analyze and work on this data set. We can load csv from this json array saved in the text file.

An entry in the .txt file named "results" is structured as follows: 


{"Title": "Assistant Supervisor/ Supervisor- Finance", "Category": "Accounting/Finance", "Company Name": "Intertek Bangladesh", "Vacancy": " 02 ", "Job Responsibility": "Manage overall operations of Accounts receivable process.", "Employment Status": "Full-time", "Educational Requirement": "Bachelor of Commerce (BCom)", "Additional Requirement": "Both males and females are allowed to apply", "Job Location": "Dhaka", "Salary": "Negotiable", "Job Source": "Bdjobs.com Online Job Posting", "Application Deadline": "October 26, 2018"},

This data set doesn't any error and the runtime for the spider is less than 1 hour.
I tried to use modularizing and documenting in my code as much as I could for better understanding and readability.  
Thus I concluded task 1.
