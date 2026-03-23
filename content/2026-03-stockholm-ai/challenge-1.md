# Challenge 1: Regional Emission Intensity Analysis

:::{note} Starting Point
You have access to the Statistics Sweden (SCB) data through the MCP server. You can query environmental and economic data using the scb_* tools. The goal is to analyze and compare emission intensity across Swedish regions.
:::

::::::{challenge}
Calculate and compare the gross emission intensity (tonnes of CO2 equivalents per million SEK of economic output) for at least 3 Swedish regions (e.g., Stockholm, Gotland, Norrbotten) for the years 2019-2021

**Expected Output**
- A table showing emission intensity by region and year
- Analysis of trends and comparisons between regions
- Identification of regions with highest/lowest emission intensity

Compute emission intensity using the formula: `Intensity = Emissions (tonnes) / GRDP (million SEK) * 1000`

:::{tip} Data to use
1. Emissions data: Retrieve air emissions by region and substance (GHG in tonnes CO2 equivalents) from table TAB4357
2. Economic data: Retrieve Gross Regional Domestic Product (GRDP) by region from table TAB3138
:::

:::::::


:::::::{challenge} Optional Challenges
1. **Interactive Visualization**: Create an interactive plot showing emission intensity trends over time for multiple regions.

:::{tip}
- 
- Instruct which library to use:
  - Generate a Python library like Plotly, Matplotlib, Gradio, Streamlit etc,
  - Use Javascript (either front-end only or full-stack) app which uses D3.js, Chart.js
:::

2. **Extended Analysis**: Extend the analysis to include more years (e.g., 2015-2023) or more regions to identify longer-term trends and regional patterns.
3. **Sector Analysis**: If available, break down emission intensity by economic sector to understand which industries contribute most to emissions in each region.
:::::::
