# 📊 U.S.-Energy-Analysis-Dashboard

## Overview

This Power BI dashboard project analyzes the U.S. energy landscape by visualizing key metrics such as total electricity generated, CO₂ emissions, and the split between renewable and non-renewable energy sources. The dashboard is designed to provide insights into the current energy mix and its environmental impact, helping stakeholders make informed decisions about sustainability and policy improvements.


![image](https://github.com/user-attachments/assets/c10e8f17-1990-4de1-9473-1cbecdc5ebaf)


## Features

- **Electricity Generation**: Displays total electricity generated (in GWh) using a custom DAX measure.
- **CO₂ Emissions**: Aggregates CO₂ emissions (in KtCO₂) from various energy sources.
- **Renewable vs. Non-Renewable Energy**: Segregates and calculates the share of renewable energy in the total electricity generation.
- **Interactive Visualizations**: Dynamic charts and graphs built in Power BI for easy exploration of the data.
- **Advanced DAX Measures**: Utilizes functions like CALCULATE, SUM, VAR, DIVIDE, and COALESCE to create meaningful metrics.
  

## DAX Measures

Below are some key DAX measures used in the dasboard:

```DAX
// Electricity Generated
Electricity Generated = 
    CALCULATE(SUM(Fact_EnergySource[Value]), Fact_EnergySource[Unit] = "GWh")

// CO₂ Emissions
CO2 Emissions = 
    CALCULATE(SUM(Fact_EnergySource[Value]), Fact_EnergySource[Unit] = "KtCO2")

// Renewable Energy
Renewable Energy = 
VAR RenewableGwh =
    CALCULATE(
        SUM(Fact_EnergySource[Value]), 
        Fact_EnergySource[Unit] = "GWh",
        NOT(Fact_EnergySource[Energy Source] IN {"Fossil", "Gas and Other Fossil", "Coal", "Gas", "Other Fossil", "Nuclear", "Clean"})
    )
RETURN
    COALESCE(RenewableGwh, 0)

// Non Renewable Energy
Non Renewable Energy = 
    CALCULATE(
        SUM(Fact_EnergySource[Value]), 
        Fact_EnergySource[Unit] = "GWh",
        (Fact_EnergySource[Energy Source] IN {"Fossil", "Gas and Other Fossil", "Coal", "Gas", "Other Fossil", "Nuclear", "Clean"})
    )

// % Renewable Energy Share
% Renewable Energy Share = 
VAR RenewableEnergyShare =
    DIVIDE([Renewable Energy],[Electricity Generated],0)
RETURN 
    COALESCE(RenewableEnergyShare, 0)

```
## 📊 Key Metrics Analyzed
-Total electricity generated and renewable energy share.

-Comparison between states in terms of renewable energy generation and usage.

-Historical evolution of electricity generation.
CO₂ emissions by state.

## 🎯 Key Findings
Texas leads in electricity generation, followed by California and Florida.

The share of renewable energy remains low (16%).

Some states exhibit high CO₂ emissions, indicating areas for sustainability improvements.


