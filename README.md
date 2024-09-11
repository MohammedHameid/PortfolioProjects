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
order by 3,4
```
### Total Cases vs Deaths
```sql
select Location, Date, total_cases, total_deaths, (total_deaths/total_cases)*100 as DeathPercentage
from PortfolioProject..CovidDeaths
where location like '%states%'
and continent is not null
order by 1,2;
```

### Total Cases vs Population
```sql
select Location, date, population, total_cases, (total_cases/population)*100 as PercentPopulationInfected
from PortfolioProject..CovidDeaths
order by 1,2;

```
### Highest Infection Rates
```sql
select Location, population, max(total_cases) as HighestInfectionCount, max(total_cases/population)*100 as PercentPopulationInfected
from PortfolioProject..CovidDeaths
group by Location, population
order by PercentPopulationInfected desc;

```
### Highest Death Counts
```sql
select Location, max(cast(total_deaths as int)) as TotalDeathCount
from PortfolioProject..CovidDeaths
where continent is not null
group by Location
order by TotalDeathCount desc;

```

### Continental Analysis
```sql
select continent, max(cast(total_deaths as int)) as TotalDeathCount
from PortfolioProject..CovidDeaths
where continent is not null
group by continent
order by TotalDeathCount desc;

```
### Global Statistics
```sql
select sum(new_cases) as total_cases, sum(cast(new_deaths as int)) as total_deaths, sum(cast(new_deaths as int))/sum(new_cases)*100 as DeathPercentage
from PortfolioProject..CovidDeaths
where continent is not null
order by 1,2;

```
### Vaccination vs Population
```sql
with PopvsVac (Continent, location, date, population, new_vaccinations, RollingPeopleVaccinated)
as (
select dea.continent, dea.location, dea.date, dea.population, vac.new_vaccinations
, sum(convert(int, vac.new_vaccinations)) over (partition by dea.location order by dea.location, dea.date) as RollingPeopleVaccinated
from PortfolioProject..CovidDeaths dea
join PortfolioProject..CovidVaccinations vac
	on dea.location=vac.location
	and dea.date=vac.date
where dea.continent is not null
)
select *, (RollingPeopleVaccinated/population)*100
from PopvsVac;

```
### Temp Table
```sql
drop Table if exists #PercentPopulationVaccinated;
create Table #PercentPopulationVaccinated
(
continent nvarchar (255),
Location nvarchar (255),
Date datetime,
Population numeric,
new_vaccination numeric,
RollingPeopleVaccinated numeric
);

insert into #PercentPopulationVaccinated
select dea.continent, dea.location, dea.date, dea.population, vac.new_vaccinations
, sum(convert(int, vac.new_vaccinations)) over (partition by dea.location order by dea.location, dea.date) as RollingPeopleVaccinated
from PortfolioProject..CovidDeaths dea
join PortfolioProject..CovidVaccinations vac
	on dea.location=vac.location
	and dea.date=vac.date;

select *, (RollingPeopleVaccinated/population)*100
from #PercentPopulationVaccinated;

```
### View Creation
```sql
create view PercentPopulationVaccinated as 
select dea.continent, dea.location, dea.date, dea.population, vac.new_vaccinations
, sum(convert(int, vac.new_vaccinations)) over (partition by dea.location order by dea.location, dea.date) as RollingPeopleVaccinated
from PortfolioProject..CovidDeaths dea
join PortfolioProject..CovidVaccinations vac
	on dea.location=vac.location
	and dea.date=vac.date
where dea.continent is not null;

select *
from PercentPopulationVaccinated;

```
## Technologies Used
SQL Server
Portfolio Project Database (CovidDeaths, CovidVaccinations)
## How to Run the Queries
Load the datasets (CovidDeaths and CovidVaccinations) into your SQL Server environment.
Run the queries in the specified order.
Review the results for each query to gain insights into the data.
## Conclusion
This project helps visualize the impact of COVID-19 across different countries and continents, shedding light on critical statistics such as death rates, infection rates, and vaccination progress.
