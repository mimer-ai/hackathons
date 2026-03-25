# Challenge 3: Electricity Production and Use Analysis

:::{objectives}
You have access to the Statistics Sweden (SCB) data through the MCP server. You can query energy data using the scb_* tools. The goal is to analyze and compare electricity production and use in Sweden.
:::

## Use case

::::::{exercise} Challenge
Retrieve and analyze the electricity supply and use data for Sweden for the years 2010-2024. Focus on the following aspects:
- Total production by energy source (Hydro power, Wind power, Solar, Nuclear power, etc.)
- Production and use (including exports).
- Total use by sector (Manufacturing industries, Services, Agriculture, Households, Exports)

Calculate the percentage contribution of each energy source to the total production and visualize the trends.
:::::::

:::{important}

**Example workflow**
- Start by searching for tables showing electricity supply and use data.

**Ground truth**: [SCB report: Electricity supply and use 2001–2024 (GWh)](https://www.scb.se/en/finding-statistics/statistics-by-subject-area/energy/energy-supply-and-use/annual-energy-statistics-electricity-gas-and-district-heating/pong/tables-and-graphs/electricity-supply-and-use-20012024-gwh/)

:::

The required tables can be easily retrieved using the search function in the MCP server. However, just in case you get stuck,
here is a hint:

:::{hint}
:class: dropdown

The following tables to use:
1. Electricity supply use data: Retrieve from table TAB1010
2. Electricity use data: Retrieve from table TAB991
:::

## Further improvements

:::::::{exercise} Optional Challenges
1. **Interactive Visualization**: Create an interactive plot showing the trends of electricity production and use over time.

:::{tip}
- Instruct which library to use:
  - Generate a Python app which uses libraries like [Plotly](https://plotly.com/python/), [Matplotlib](https://matplotlib.org/), [Gradio](https://gradio.app/), [Streamlit](https://streamlit.io/), [Holoviz](https://holoviz.org/), [Altair](https://altair-viz.github.io/), [Seaborn](https://seaborn.pydata.org/), or [Bokeh](https://bokeh.org/)
  - Use Javascript (either front-end only or full-stack) app which uses [D3.js](https://d3js.org/), [Chart.js](https://www.chartjs.org/), [Vega-Lite](https://vega.github.io/vega-lite/), [Observable Plot](https://observablehq.com/plot/), or [Pico.css](https://picocss.com/)

  For data handling, SCB returns JSON-stat responses which can be processed using:
  - Python: [pyjstat](https://pypi.org/project/pyjstat/)
  - JavaScript: [jsonstat-toolkit](https://www.npmjs.com/package/jsonstat-toolkit)
:::

2. **Renewable Energy Analysis**: Analyze the contribution of renewable energy sources (Hydro power, Wind power, Solar) to the total production.

3. **Price correlation**: Compare against data for **Electricity grid prices** and **electricity prices for households and non-households**. What is driving this trend? Productions vs use or exports?

:::{tip}
Use multiple charts to make a mini investigation. You can choose to compile it into a report or a slidedeck.
You can use tools like Pandoc to generate a PDF or Reveal.js to make a presentation.
:::

:::::::
