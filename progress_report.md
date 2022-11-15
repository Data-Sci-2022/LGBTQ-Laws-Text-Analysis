# Progress Reports for LGBTQ Laws Text Analsysi

## Initial Progress Report
### 10.11.2022 

Created GitHub repository and cloned to my computer. Made project_plan and progress_report documents. Narrowed down where the data will come from ([Freedom for All American Legislative Tracker](https://freedomforallamericans.org/legislative-tracker/)) and narrowed the scope from US and international laws to only US laws.

## First Progress Report
### 11.03.202

I have planned out how my data will be organized: each legislation will be its own tibble; there will be a tibble of metadata, including the US State, whether the law is pro- or anti-LGBTQ rights, status of the bill, and a link to the law; there will also be a tibble of each US State and its corresponding MAP Score and Equality Index. I have scraped the Equaldex and MAP tables per state.

I am running into issues in the scraping process. There are limited laws readily scrapeable from the Freedom for All American's tracker that I am using. For anti-LGBTQ+ rights there are more laws in the works, but access to them will be difficult to scrape. Even the laws that are more accessible for scraping are sourced from a widget from the BillTrack50 website, so this is another hurdle to overcome. From preliminary research I may need to use another R package (Selenium) to pull this data.

The TOU from BillTrack50 where all the various state laws are collected prohibit the automated collection of information from its website. I reached out asking for permission to run my script and was granted permission with some small and agreeable caveats.

Because the legislation is readily available online, and to save space, I will not provide the tokenized versions of the legislation, but I will provide the tibbles with the metadata and the various scores per state.


## Second Progress Report
### 11.15.2022

I am going to pursue using BillTrack's API to pull all the required metadata and bill information. This will alleviate me needing to work with the Selenium package or JavaScript. I am waiting to hear back from the folks at Bill Track to give me the remaining information I need to run the API to extract the information. While I wait for this, I have worked on tidying the legislation PDFs to be in tidy text format. I have decided to load the PDFs into R directly from the URL instead of downloading the PDFs and then reading them into R from my repo. This will help some with reproducibility, but may pose an issue if the webpages crash.

Based on a conversation with Lauren Collister from the Pitt Library, I am planning on loading each page into the way back machine to have a record of the page, especially as new politicians come into leadership, the longevity of these pages are at risk.

I have wrangled with the table data and gotten it almost into its final form. The MAP data took more to wrangle: I had to split each column, and pivot wider to separate information on Gender Identity and Sexual Orientation. Both tables had US territories included, so I did an anti-join on state names to filter out any non-state territories, as these will not have any correspoding legislation. I will preserve raw tables as well as the table that I have manipulated to fit my project.

Updated data sample with wrangling on tables and work with PDFs.
