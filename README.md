# nypd-driving-project

## Internal NYPD Files Related to Officers' Driving 

### Goals
I set out to use scraping and AI classification on a set of records that I was interested in finding out more about - officer DUI cases. I knew there was an existing database of internal NYPD police disciplinary records, but not a reliable way to count how many times officers had gotten flagged for driving under the influence. Ideally, I wanted to answer questions like, how many officers have gotten in trouble for driving (especially drunk driving) cases? How often are officers penalized for driving cases? What are the average punishments? 

### Data collection process
[Legal Aid Society](https://legalaidnyc.org/law-enforcement-look-up/) built a database of NYPD internal records via scraping. The one I'm referring to contains, according to Legal Aid, Internal Affairs Bureau Investigation reports, data scraped from the NYPD trial decision library, indices of police misconduct Legal Aid and other public defender orgs obtained and NYPD internal investigations scraped from the NYPD Officer Profile.

I initially tried to scrape the[ NYPD personnel website](https://nypdonline.org/link/personnel) myself and found there was an undocumented API that I could call. Using that, I was able to scrape the data from one tab, the ([the trial decision library](https://nypdonline.org/link/1016)), and I downloaded the relevant PDFs. I could've then used a pdf library to parse the PDFs, but there are multiple tabs containing records and the one with a profile for each officer likely would've required browser automation. Because Legal Aid Society's database appears to have records that aren’t on the NYPD site, I went with their already scraped data which is updated weekly.

### Overview of the data analysis process

The Legal Aid dataset of police discipline cases has more than 10,000 rows, but that doesn’t mean there are that many officers involved. One case can have multiple administrative charges associated with it, so officers appear multiple times in the database, sometimes for the same incident. I tried to account for the fact that officers' names appear multiple times and that officers have have administrative charges related to each incident. There are limitations to this data - for example, the most reliable way to link records is using an officers’ tax id, but 2,105 of those values are null.

I wanted to find out how many of these internal discipline cases had to do with driving, so I used Jeremy Merrill's method of AI classification, which involves handcoding a sample and checking the AI's work using various statistical methods. 

In addition to identifying driving cases, I also tried to categorize some other categories of misconduct - for my purposes here, use of force and integrity violations (lying, falsifying reports, etc). There is likely a way to do this with keywords, but the descriptions of charges vary considerably in their phrasing. I only used cases where the data contained a description for the charge. By eliminating those, I only ended up including cases where the disposition was “guilty”, “pleaded guilty” or "nolo contendre," (or no contest for those who don’t speak Latin). At this point, I had only 4,534 entries to classify. 

The AI had an 100% precision score, a 89% recall score and a 92% accuracy rate. That left me with a list 671 charges related to driving, corresponding to close to 320 unique officers. Because the penalties differed so much and often included multiple outcomes (like losing 15 days of vacation and undergoing counseling), it wasn't as easy as I had initially thought to come up with straightforward answers to my questions about common penalties.

### New skills/approaches

I was able to use the AI classification on a new set of records and experiment with undocumented APIs in the wild, which helped me solidify those new skills. I also continued to use pandas to analyze data.

### More to do

If I'd wanted to continue practicing more skills here, I would've gone through the pdfs and extracted the data from them that exists in the Legal Aid Society database. I probably could've used regex and pandas to come up with ways of categorizing penalties in a way that made sense. If I'd had more time, I could've used browser automation to go through the main personnel database, which involves clicking on a letter in the alphabet and then clicking through the various pages for each result.
