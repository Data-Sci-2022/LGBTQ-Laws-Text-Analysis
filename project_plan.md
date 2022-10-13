# A Linguistic Analysis of LGBTQ+ Legislation

## Summary

This research project will analyze pro- and anti-LGBTQ+ legislation from the US to see what statistical connection there is between the language used in the legislation and its equality index as assigned by [Equaldex](https://www.equaldex.com/equality-index) and its overall LGBTQ Policy tally as calculated by the [Movement Advancement Project](https://www.lgbtmap.org/equality-maps).


## Data

I will use an automated web scraping process to gather all the data, to save time from downloading all the data by hand. The text data will come from the [Freedom for All American Legislative Tracker](https://freedomforallamericans.org/legislative-tracker/). All the legislation is linked to [Billtrack50](https://www.billtrack50.com/) which should streamline the scraping process. There are various metadata (state of bill, date of bill, etc.) associated with the legislation that will be collected and may be used in the analysis. All legislation will be tagged with location, whether the bill is pro- or anti-LGBTQ+, and potentially tagged for topic, i.e. Trans rights, sports, education, marriage, adoption, etc.


## Analysis

I will be doing text analysis on the laws with packages like `tidytext` and `quanteda`. Additionally, I will run statistical tests to see what relationship exists between the language used in the laws and the respective equality index of that state. My primary focus will be lexical items, but other linguistic features worth analysis may arise in the data wrangling process. In addition to the statistical tests, by analyzing pro- and anti-LGBT laws I may also be able to compare linguistic features across these lines and see if any significant distinctions exist between the two. 
