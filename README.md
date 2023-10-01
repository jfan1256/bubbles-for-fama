# bubblefacto
Bubbles in Fama

## Introduction
This repo replicates Bubbles for Fama (Greenwood et al.). https://scholar.harvard.edu/files/shleifer/files/bffs_20170217.pdf. I recommend reading this paper before running this code. 

There are 9 factors that they create:
1. Volatility: Each month, we compute volatility of daily returns of each stock in the industry. Let X denote the percentile rank of volatility in the full cross-section of firms. Industry volatility is the value-weighted mean of X for that industry. For example, following the 100% price run-up over a two-year period in March 1928, the volatility rank of Automobiles was 0.63, meaning that 63% of firms had lower volatility than the average firm in the Automobile industry at that time.
2. Turnover: Turnover is shares traded divided by shares outstanding. For Nasdaq stocks, due to the well-known double counting, we divide turnover by two (Anderson and Dyl 2007). To compute industry turnover, we percentile rank monthly turnover for every stock in CRSP, and then compute the value-weighted turnover rank for each industry. For example, turnover of the software industry in March 1999 was 0.86, meaning that value-weighted turnover of the industry was higher than 86% of all listed stocks.
3. Age: Firm age is measured as the number of years since the firm first appeared on Compustat or on CRSP, whichever of these came first. To compute industry “age”, we percentile rank age for every stock in CRSP, and then compute the value-weighted rank for each industry. 
4. Age Tilt: Because industry definitions are imperfect, this variable is meant to capture whether the price run-up occurred disproportionately among the younger firms in the industry. Age tilt is the difference between the equal-weighted industry return and the age-weighted industry return.
5. Issuance: Percentage of firms in the industry that issued equity in the past year. A firm is said to have issued equity if its split-adjusted share count increased by five percent or more. Issuance was elevated in many, but not all, price run-ups. In March 1999 in the Software industry, Issuance was 48%, meaning that 48% of the firms in the industry had either gone public or issued at least 5% new stock in the most recent year. 
6. Book-to-market ratio: We use book-to-market ratio mainly because we can compute it for all stocks going back to the 1920s, relying on Ken French’s book equity data for firms between 1925 and 1965. Fama and French provide book equity value for firms between 1926 and the 1960s (when they become available more broadly on Compustat), allowing us to compute book-to market ratios for most industries in our sample.
7. Sales growth: For firms with at least two years of revenue data ending in the month of the price run-up or before, we calculate the one-year sales growth based on the most recent two observations, and then compute the value-weighted rank for each industry. By construction, this omits information on newly listed firms for which we do not have two years of data.  
8. CAPE: The cyclically-adjusted market price-earnings ratio in the month in which the price run-up is identified, available on Robert Shiller’s website. International CAPE series are available through Global Financial Data, covering 30 countries in our sample. 
9. Acceleration: This measures the convexity of the price path. We define it as the difference between the two year return and the return for the first year of that two year period Rt24→t  - Rt-24→t-12. This measures how much of the price appreciation has occurred most recently. 

## Data
1. cape.csv is retrieved from this link http://www.econ.yale.edu/~shiller/data.html. I would recommend copying and pasting the date column and CAPE column from the last tab called "Data" into a new excel file.
2. curr_be.csv is retrieved from WRDS CRSP after 1960 where it becomes available (choose the search the entire database option).
3. fama_48.csv, fama_ewr.csv, fama_vwr, fama_be, 48IndFama is retrieved from http://mba.tuck.dartmouth.edu/pages/faculty/ken.french/data_library.html. For fama_ewr and fama_vwr, I recommend also copying and pasting the data into new individual excel files. fama_be is a txt file which is tedious and annoying, but the code handles that for you. 48IndFama are the industries categories that this code and the paper utilizes the categorize each stock into a industry using their SIC code.
4. month_price is retrieved from WRDS CRSP after 1926 on a monthly interval (choose the search the entire database option).
5. revenue is retrieved from WRDS CompuStat after 1950 on an annual interval (choose the search the entire database option).
6. daily_price is retrieved from WRDS CRSP after 1926 on a daily interval (choose the search the entire database option).

## Note
When downloading from WRDS use these categories:
- Ticker (ticker)
- CRSP Permanent Company Number (permco)
- Share Code (shrcd)
- Nasdaq Issue Number (issuno)
- SIC Code (siccd)
- Price (prc)
- Share Volume (vol)
- Holding Period Return (ret)
- Number of Shares Outstanding (shrout)
- Factor to Adjust Shares (facshr)
