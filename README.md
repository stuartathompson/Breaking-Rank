Breaking Rank
======

An interactive tracking which MPs voted against a majority of their party

Coding, design and data work by Stuart A. Thompson

Written by Stuart A. Thompson and Bill Curry

See the live version here: http://www.theglobeandmail.com/news/politics/breaking-rank-how-often-do-mps-vote-against-their-own-party/article8141646/

See the related story here: http://www.theglobeandmail.com/news/politics/conservative-mps-break-ranks-more-often-than-opposition/article8156279/?cs

How it was made
-----

As part of The Globe’s new series “Reinventing Parliament,” we decided to investigate how often Members of Parliament voted against the majority of their party. The undertaking took weeks of number crunching, programming and visualizing to put together. The end product shows a clear trend: MPs rarely break ranks, with most voting along party lines more than 97 per cent of the time. But Conservative MPs are overwhelmingly more likely to break rank than members from other parties.

The project began by scraping 600 pages of parliamentary voting data. We designed a scraper in Python that trudged through these pages, scraping the MP’s name, party, riding and vote. All told, we had 162,280 votes between June 2, 2011 and Jan. 28, 2013.

The next step was determining whether the MP voted with or against their party. We first believed we could check this against the whip’s vote. But we ran into trouble when we realized the party whip was sometimes (unsurprisingly) absent. We decided to measure each MP’s vote against the majority of their party instead — a measure of 50 per cent plus one.

This was a two-step process. First, we ran another Python script on our scraped data to count the number of yeas and nays on each vote. We ran the resulting spreadsheet through another Python script to compare each MP’s vote. The script added a column to the original dataset indicating whether they voted the “same” as or “different” from the party.

This spreadsheet gave us the first usable data to measure party unity. We used Microsoft Access to run queries, starting by calculating the number of times an MP voted differently from their party. We ran another query to find the total number of votes for each MP. (While there are 600 votes total, each MP has a different attendance record.) Combined, we had a percentage score for party unity.

At each step of the process, we spot-checked and confirmed our results against the original raw data to ensure there were no irregularities. We found a few errors along the way and re-designed our queries or adjusted the Python scripts until we were confident the final data set had no errors.

Then we began the analysis. We started with a few questions. What was the most contentious vote? (It was No. 466, a motion to study the beginnings of life.) Who broke ranks most often? (By percentage, it was former NDP MP Bruce Hyer, who later became an independent MP. By raw total, it was Conservative MP James Bezan.) Did votes change with party leadership? (A few NDP MPs voted against the party before Thomas Mulcair became leader. Afterward, there were no dissenting votes.)

We supplemented this analysis with more parliamentary data. We scraped the information on each motion, which gave us more context like the purpose of the motion or who sponsored it. This made it easier to cross-reference party unity scores and explain the outliers. We also scraped information on all sitting MPs to add information like riding and title.

Finally, we created a short Python script for scraping MP photos from the Parliament website for use in the interactive. An arduous element of this step was correcting the file names for each MP, since they had to match MP names stored in the dataset so they could be dynamically added to the page when needed.

Then the process of visualizing the data began. We had three main goals with the visualization: 1) showing how many Conservatives voted against the majority of their party compared to MPs from other parties; 2) showing the high levels of party unity, despite the occasional dissenting vote; 3) allowing readers to see more detail about each motion or bill that the MP dissented on.

We settled on using D3, a JavaScript library that uses new web technologies to animate individual nodes in unique and interesting ways. The library also allowed us to re-arrange the data across several views. By colour-coding each node and separating MPs with some dissenting votes from those with none, we could immediately show the number of Conservative MPs who registered lower party unity scores.

D3 is a powerful library but it comes with one major caveat: its more advanced animations don’t display in Internet Explorer, which remains a pervasive browser among our readers. Other news organizations like the New York Times have previously not supported IE for these visualizations.

As a fallback, we decided to try Raphael, a fantastic JavaScript library that works in every browser but doesn’t have the more complex “force collision” capabilities of D3. We were able to export X and Y co-ordinates for each node and each view in the D3 visualization, giving us three sets of points from which we could build an entirely separate visualization. If a user visits the page in Internet Explorer, the code directs them through a Rapahel version of the script with animations and interactivity intact.

The end product is hopefully an engaging example of data journalism, which lets readers explore the data and become more informed about the inner workings of Parliament.
