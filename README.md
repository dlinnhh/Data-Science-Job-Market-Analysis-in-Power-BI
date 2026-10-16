# Analyzing-Data-Science-Job-Market-in-Power-BI


### Project Overview
In this Power BI case study, I analyzed a dataset of over 25,000 job postings to uncover key skills and hiring trends in data science for DataSearch, a fictional recruitment agency. Using Power Query, I cleaned and prepped the 17-column dataset to identify high-demand skills for Data Scientists, Data Analysts, and Data Engineers. I then used DAX to build dynamic metrics and created an interactive business dashboard to deliver actionable recruitment insights for the DataSearch team.

### Project Objectives
Investigate market trends for different data science roles.

* The context:
DataSearch, a recruitment agency needed actionable insights into the evolving data market.
* The task:
Discover trends and in-demand skills within the data science industry.
* The dataset:
Analyze 25,114 job postings containing 17 key attributes about each job posting (Title, Date, Industry, Skills, ... ).

### Work Journey:
1. Checking and Cleaning Data
3. Exploring Data
4. Analyzing and Visualizing Data
5. Dashboarding
6. Communicating Insights

## Step 1: Exploratory Data Analysis

I started this case study by importing the job posting dataset into Power BI and cleaning it using Power Query. During initial exploration, I found that **93% of the values in the Max Pay and Min Pay columns were null**, indicating that the majority of companies do not disclose salary ranges in their job postings.
Next, by sorting job postings by applicant volume in descending order, I identified the three most popular industries:
Marketing & Advertising,
Computer Software, and
Broadcast Media.

### Higher Experience, Higher Level

To understand how required experience scales with seniority, I evaluated the relationship between the Average Years of Experience and Job Position Level using a Bar Chart.

<!-- TODO your screenshot: ![Average years of experience by job position level (bar)](images/02-experience-by-job-level-bar.png) -->
<img width="1277" height="477" alt="Avg Ex Year by Job Level vor" src="https://github.com/user-attachments/assets/ac7ff2a9-d958-44ba-b8ec-05e6ecc691a4" />

- Executive Level: Required the highest average experience at 15.17 years.
- Internship Level: Required the lowest average experience at 0.37 years (under 5 months).
- Overall Range: Across all 6 position levels, required experience ranged from 0.37 to 15.17 years.

  
### Job Posting Trend Analysis

To analyze hiring trends over time, I plotted the Count of Job Posting IDs against the Job Posting Date.

<!-- TODO your screenshot: ![Count of job postings over time](images/03-posting-trends-over-time.png) -->
<img width="1134" height="594" alt="Count of job post over time vor" src="https://github.com/user-attachments/assets/e25f180a-fdba-4cb5-b571-f9ea2e58a9e5" />

- Job postings hit the lowest point in Q1 2020 due to the rise of Covid pandemic.
- From Q3 2020 - Q4 2021, the job posting counts for all levels fluctuated significantly, though the overall demand ended on an upward trend compared to previous years.

### Data Related Job Roles

Next, I filtered the dataset to focus specifically on these roles: Data Scientist, Data Analyst, Data Engineer, Machine Learning Engineer, and Data Science Manager.

<!-- TODO your screenshot: ![Count of job postings by data job title](images/04-job-title-posting-count.png) -->
<img width="1128" height="475" alt="Count of job posting by job title vor" src="https://github.com/user-attachments/assets/fba35c0f-74cb-48b5-82b0-8b27be48f6e4" />

- Data Engineers dominated the space with 3,462 postings (47.7% of all data roles).
Across all 5 filtered titles, posting volumes ranged from 23 to 3,462.

### Impact of Experience on Salary

Finally, I examined compensation trends across data roles relative to required experience.

<!-- TODO your screenshot: ![Years of experience vs offered salary](images/05-experience-vs-salary.png) -->
<img width="1133" height="592" alt="Avg of Avg Pay and Ex year" src="https://github.com/user-attachments/assets/fe43c526-858c-4adb-b6e9-063cf5df2704" />

- Obviously, the higher the position that doesn't mean the higher the salary. **However**, because over 93% of Max and Min pay entries were missing/null, these pay averages represent a limited sample and should be interpreted with caution rather than drawn as definitive industry conclusions.

## Step 2: Skills & Industry Analysis

Building on my initial EDA (Step 1 ), I used DAX modeling and specialized visualizations to analyze:
- Correlation between skills and job title
- Top industries and companies
- Potential recommendations
### Skill Extraction & Data Transformation
To analyze individual skill demand, I created a ```Job Skill``` table using only the two columns ```Job Posting ID``` and ```Job Skills``` in Power Query from the raw dataset:
- Cleaning: removed brackets [], quotes ", whitespace in each cell using Trim and Clean.
- Unpivoting: Split comma-separated skill lists into individual rows for each job posting.
  
Next, I visualized the count of Job Skills to gain an initial idea of the top 10 demanded skills.

<!-- TODO your screenshot: ![Count of job skills](images/06-job-skill-count.png) -->
<img width="1131" height="592" alt="Top 10 job skills" src="https://github.com/user-attachments/assets/810e4f21-724e-45dc-a71f-9fda44fb8dfe" />


### Skill Likelihood Modelling (DAX)
To measure the exact probability of a skill appearing in a job posting, I created three measures: 
- ```Skill Count```= count each ```Job Skills``` in Job Skill table. 
- ```Posting Count```= count each ```Job Posting ID```in Job Posting table.
- ```% of Skill in Posting```= ```Skill Count```/```Posting Count```.

Then I created a Matrix Visual with a Slicer so it would be easier to filter for a specific skill.

<!-- TODO your screenshot: ![Skill likelihood matrix with slicer](images/07-skill-likelihood-matrix.png) -->
<img width="966" height="527" alt="Skill likelihood" src="https://github.com/user-attachments/assets/af5e3f9b-cc28-4c47-9de5-2d719f9ca4c6" />



### Skill Trends Over Time
I built a Line Chart plotting ```% Skill in Posting``` against ```Posting Date```, and use ```Job Skills``` from ```Job Skill``` table as a legend. The top 10 core skills maintained steady, consistent demand over the 5-year period.

<!-- TODO your screenshot: ![Skills in demand over time](images/08-skills-over-time.png) -->
<img width="919" height="592" alt="Skill demand over time" src="https://github.com/user-attachments/assets/2ffd70ba-100c-434c-8e02-75d4ff37f694" />

### Company & Industry Deep Dive

To map hiring demand to specific sectors and employers, I designed two visual layouts:
1. Scatter Plot: Average Years of Experience vs. Company Industry, ```Job Level``` as Legend and ```Posting Count```as bubble size.

<!-- TODO your screenshot: ![Industry scatter: experience vs posting count](images/09-industry-scatter.png) -->
<img width="1022" height="576" alt="Avg year ex by industry" src="https://github.com/user-attachments/assets/cd20ae37-8a74-4894-a99b-eac1f5a6559c" />


2. Table: Posting Count by Company Name and Job Title.

<!-- TODO your screenshot: ![Company-level posting table](images/10-company-table.png) -->
<img width="384" height="549" alt="Job posting count table" src="https://github.com/user-attachments/assets/5c7b013b-703e-49aa-b19f-6bb33c93f3d6" />


## Step 3: Building Dashboard

To deliver an actionable, user-friendly report for the DataSearch recruitment team, I consolidated the analytical findings into a cohesive, three-page Power BI dashboard designed for seamless navigation and insight discovery.

### Home Page
Landing page, providing user-friendly navigation across the report.
<!-- TODO your screenshot: ![Dashboard layout / background design](images/11-dashboard-layout.png) -->
<img width="795" height="479" alt="Home Page" src="https://github.com/user-attachments/assets/d158165b-c088-4ee9-89ff-79d536a38480" />


### Job Overview Page
Highlights hiring trend, position level, and experience requirements across filtered data roles.
<!-- TODO your screenshot: ![Top skills for jobs page](images/12-jobs-page-top-skills.png) -->
<img width="987" height="554" alt="Job Overview" src="https://github.com/user-attachments/assets/9ba2f409-2b58-4f0e-8572-7f49111ba2b8" />


### Skill Overview Page
Focuses on skill prevalence, likelihood metrics, and tech tool requirment trends.
<!-- TODO your screenshot: ![Salary gauge for companies](images/13-company-salary-gauge.png) -->
<img width="985" height="555" alt="Skill Overview" src="https://github.com/user-attachments/assets/de1b33dc-639b-4ae1-a836-0fba2987492f" />


### Company Overview Page
Evaluates top-hiring companies, industry concentrations, and salary ranges.

<!-- TODO your screenshot: ![Dashboard - Company page](images/17-dashboard-company.png) -->
<img width="985" height="553" alt="Company Overview" src="https://github.com/user-attachments/assets/daee636d-4be5-45ab-8021-bc5953e03fa1" />






