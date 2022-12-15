# LGBTQ-Laws-Text-Analysis
By Mack Campbell, mack.campbell@pitt.edu
December 15, 2022

## Project overview

This research project analyzes pro- and anti-LGBTQ+ legislation from the US to see what statistical connection there is between the language used in the legislation and measures of equality per state for its LGBTQ+ population.

## Where the data come from

I looked at the equality index for each state as assigned by [Equaldex](https://www.equaldex.com/equality-index) and its overall LGBTQ+ Policy tally as calculated by the [Movement Advancement Project](https://www.lgbtmap.org/equality-maps). These measure different aspects of equality and legal protections. [Freedom for All Americans](https://freedomforallamericans.org/legislative-tracker/) has a list of Pro and Anti LGBTQ+ legislation that I used to guide what legislation I included in my analysis. The Freedom for All American's website had the legislation on their site as a widget from [BillTrack50](https://www.billtrack50.com/). I gained permission to scrape BillTrack50's website, otherwise all scraping is prohibited in their TOS. On BillTrack50's website each bill page links to the state's page that houses the PDF text of the bill. This is finally where I pulled in all the text to analyze.


## Repo organization

* [Final Report](./final_report.md) explains my data, my analysis of it, and some of my methodology. The entire methodology can be seen in the analysis walkthrough ([rmd](./analysis_walkthrough.Rmd)) ([md](./analysis_walkthrough.md)).
* [Data](/data) has all the data files used in the analysis.
* [State Bill csvs](/data/State-Bill-csvs) is separated into [Anti](/data/State-Bill-csvs/Anti) and [Pro](/data/State-Bill-csvs/Pro).
* [BillTrack DF](/data/statetextdf.csv) is a dataframe of BillTrack information, to avoid scraping.
* [State Text DF](/data/statetextdf.csv) is a dataframe of bill texts, to avoid having to scrape and compile the data.
* [Data Visualization](/data_visualization) includes all graphs generated from my analysis walkthrough ([rmd](./analysis_walkthrough.Rmd)) ([md](./analysis_walkthrough.md)).
* Analysis Walkthrough ([rmd](./analysis_walkthrough.Rmd)) ([md](./analysis_walkthrough.md)) goes through all the code I used to collect and manipulate my data.
* [License](./LICENSE.md) details how you may use and share the data and code in this repo.
* [Presentation](./Presentation.pdf) is a copy of the presentation given of this project on December 8, 2022.
* [Progress Report](./progress_report.md) details progress made on the project through the Fall semester of 2022.
* [Project Plan](./project_plan.md) is the original project plan. Compare to the end of the [final report](./final_report.md#process-notes) to see changes made.
