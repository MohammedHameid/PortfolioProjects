# COVID-19 Data Analysis Project

This project analyzes COVID-19 data using SQL queries. The data comes from two datasets: `CovidDeaths` and `CovidVaccinations`, and focuses on various aspects like total cases, deaths, vaccination rates, and population infection percentages.

## Table of Contents
- [Project Overview](#project-overview)
- [Queries Used](#queries-used)
  - [Data Selection](#data-selection)
  - [Total Cases vs Deaths](#total-cases-vs-deaths)
  - [Total Cases vs Population](#total-cases-vs-population)
  - [Highest Infection Rates](#highest-infection-rates)
  - [Highest Death Counts](#highest-death-counts)
  - [Continental Analysis](#continental-analysis)
  - [Global Statistics](#global-statistics)
  - [Vaccination vs Population](#vaccination-vs-population)
  - [Temp Table](#temp-table)
  - [View Creation](#view-creation)
- [Technologies Used](#technologies-used)
- [How to Run the Queries](#how-to-run-the-queries)
- [Conclusion](#conclusion)

---

## Project Overview

This project provides insights into the COVID-19 pandemic using SQL queries to explore different dimensions such as infection rates, death counts, and vaccination progress across countries and continents.

## Queries Used

### Data Selection

```sql
select *
from PortfolioProject..CovidDeaths
where continent is not null
order by 3,4;```

### Total Cases vs Deaths
sql
Copy code
select Location, Date, total_cases, total_deaths, (total_deaths/total_cases)*100 as DeathPercentage
from PortfolioProject..CovidDeaths
where location like '%states%'
and continent is not null
order by 1,2;
Total Cases vs Population
sql
Copy code
select Location, date, population, total_cases, (total_cases/population)*100 as PercentPopulationInfected
from PortfolioProject..CovidDeaths
order by 1,2;
... (Continue with the remaining queries)

Technologies Used
SQL Server
Portfolio Project Database (CovidDeaths, CovidVaccinations)
How to Run the Queries
Load the datasets (CovidDeaths and CovidVaccinations) into your SQL Server environment.
Run the queries in the specified order.
Review the results for each query to gain insights into the data.
Conclusion
This project helps visualize the impact of COVID-19 across different countries and continents, shedding light on critical statistics such as death rates, infection rates, and vaccination progress.

markdown
Copy code

5. **Preview the README**:
   - Once you’ve added the content, scroll down to the bottom of the GitHub editor, where you’ll see a **Preview** tab that shows how the file will look once published.

6. **Commit the File**:
   - After confirming everything looks correct, scroll down and click the **"Commit new file"** button to save the README to your repository.

### Resources for Learning Markdown:
- [GitHub Markdown Guide](https://guides.github.com/features/mastering-markdown/)
- [Markdown Cheatsheet](https://www.markdownguide.org/cheat-sheet/)

Once you've followed these steps, your README will appear just like the one I formatted earlier! Let me
