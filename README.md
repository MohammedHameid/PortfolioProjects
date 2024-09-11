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
order by 3,4;

