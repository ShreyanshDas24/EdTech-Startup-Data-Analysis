# EdTech Course Analytics Dashboard

A Power BI dashboard built for a fictional EdTech startup that wants to expand its recorded-lecture catalogue. I cleaned a messy multi-site course scrape, answered nine business questions about it, and put the answers on a single dashboard. Everything is organised category-first, since that was the main thing the client cared about.


\---

## The brief

The startup pulled course data from several EdTech sites and didn't know what to do with it. They wanted to know:

* which course types to launch in which categories
* where viewers actually are (by category, sub-category and language)
* which skills are in demand
* whether subtitles, course length or skill variety move the needle on views
* which instructors are worth approaching

## About the data

|||
|-|-|
|File|`Online\_Courses.csv`|
|Raw size|8,092 rows x 45 columns|
|Sources|Coursera, FutureLearn, Udacity, Simplilearn|
|Usable rows|2,819 (the Coursera records, the only source with category, sub-category, viewers and rating filled in)|

The raw file is a stack of four differently shaped scrapes, so most columns are empty for most rows. Only the Coursera rows carry the fields the analysis depends on.

Main columns used: `Title`, `Category`, `Sub-Category`, `Course Type`, `Language`, `Subtitle Languages`, `Skills`, `Instructors`, `Rating`, `Number of viewers`, `Duration`.

## Cleaning steps

* Dropped rows with no category, plus the columns that were empty or belonged to the other sites' schemas.
* Standardised category names. A handful of rows had translated labels (Spanish, Portuguese, Chinese, Japanese) that were folded back into the English category they belong to.
* Turned `Number of viewers` (stored as text like `"10,438 "`) and `Rating` (like `"4.9stars"`) into numbers.
* Split `Skills` and `Instructors` (comma-separated lists) into one row per skill / instructor so they could be counted and ranked.
* Counted the languages listed in `Subtitle Languages` to create a `Subtitle\_Language\_Count` field.
* Converted `Duration` to hours. Month-based durations use **60 hours per month**, and flexible-schedule courses are set to **200 hours**, as the brief specified.
* Checked for duplicate URLs (none) and repeated titles, and handled missing viewer counts so they don't drag averages down.

## What the dashboard answers

|#|Question|Visual|
|-|-|-|
|1|Course type mix by category, plus course counts by category and sub-category|Course Type Popularity bar chart, Category slicer|
|2|Average views by category, sub-category and language|Courses as per Sub-Categories and Languages chart, category ranking table|
|3|Most in-demand skills per category|Demanding Skills word cloud|
|4|Language distribution of courses|Most Prominent Languages pie chart|
|5|Language preference for the top 5 categories by viewers|Ranking table (`rank\_category\_by\_views`) filtered to the top 5|
|6|Subtitles vs. views|Number of viewers by subtitle language count (line chart)|
|7|Top 3 instructors per category and sub-category by rating|Instructor rating bar chart (static, as requested)|
|8|Course duration vs. views|Average viewers by duration in hours|
|9|Skill variety vs. views|Average skill count and average viewers by category|

The Category and Sub-Category slicers filter every visual except the instructor chart, which is deliberately static.

## Key findings

These come straight from the dashboard.

* **Courses dominate.** Of the catalogue, about 2.3K are standalone courses against roughly 0.4K specializations. Projects and professional certificates are barely represented, which means there's open space there if the client wants to differentiate.
* **Data Science gets the most attention.** It averages around 6.4K viewers per course, well ahead of the rest. The top five categories by average views are Data Science, Information Technology, Computer Science, Personal Development and Language Learning.
* **English is almost the whole catalogue.** About 97% of courses are in English. Spanish is a distant second, followed by French and Japanese.
* **Subtitles matter.** Average views climb with the number of subtitle languages, and the curve gets steep at the high end (the 26-language courses average about 86K viewers). Worth remembering that those courses are probably also the big, well-known ones, so this is a strong correlation and not proof of cause.
* **Longer isn't automatically better.** Views are spread across durations, with a few large spikes at certain course lengths rather than a smooth rise.
* **More skills tends to go with more views.** Data Science and Personal Development lead on average skills per course (about 4.7 and 4.5) and are also among the highest on views. Language Learning is the exception: few skills per course but high views.
* **Top instructors** sit at 4.7 to 4.8 average ratings in the sample shown.

## Suggestions for the client

1. Put new launches in the high-view categories first (Data Science, IT, Computer Science), but check sub-category numbers before committing since averages hide a lot.
2. Specializations and professional certificates look under-supplied compared with single courses. Test them where demand is already strong.
3. Add multi-language subtitles to existing content. It's a cheap change and the data suggests a real engagement benefit.
4. Approach the top-rated instructors in each category for content partnerships.
5. Consider non-English content for Spanish, where there's clearly some demand but very little supply.

## Tools

* Power BI Desktop (data model, DAX measures, visuals)
* Power Query (cleaning and transformations)
* Python / pandas for early exploration of the raw file

## Repo structure

```
.
├── data/
│   └── Online_Courses.csv
├── assets/
│   └── dashboard.png
├── Dashboard.pbix
└── README.md
```

## How to open it

1. Clone the repo.
2. Open `EdTech\_Course\_Analytics.pbix` in Power BI Desktop.
3. If Power BI asks for the data source, point it to `data/Online\_Courses.csv`.

## Limitations

* Only Coursera records had the fields needed, so the analysis reflects one platform, not the whole market.
* Viewer counts are missing for part of the data, and averages are based on the rows that have them.
* Converting months to hours is an assumption (60 hours per month, 200 hours for flexible schedules), so the duration analysis depends on it.
* Correlations here (subtitles, skill count, duration) shouldn't be read as causes.

## Author

**Shreyansh Kumar Das**
M.Sc. Data Science | Python, R, SQL, Power BI
[LinkedIn](#) | [GitHub](#)

