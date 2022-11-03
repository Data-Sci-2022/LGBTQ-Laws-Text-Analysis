# Data Overview

## Data Source

The legislation I am including in my analysis comes from a list of laws compiled on [Freedom for All American Legislative Tracker](https://freedomforallamericans.org/legislative-tracker/). They track pro-LGBTQ legislation as well as anti-LGBTQ legislation. The amount of legislation is not equal across these two categories. I am not sure if I will make them the same size or if I will collect all legislation listed across both categories. Pro-legislation has 24 laws and anti- legislation has 264 laws.

Each legislation lives on the state's respective websites. The links to the legislation is collected and consolidated to one location on [BillTrack50](https://www.billtrack50.com/).

The linguistic data from the legislation above is compared to the states [MAP Score](https://www.lgbtmap.org/equality-maps) and [Equality Index](https://www.equaldex.com/equality-index).

## Data Structure

Each legislation will be its own tibble.
There will be a tibble for metadata, including the US State, whether the law is pro- or anti-LGBTQ rights, status of the bill, and a link to the law.
There will also be a tibble of each US State and its corresponding MAP Score and Equality Index.
