# Cleaning Log

## 2023 Presidential Results (Wikipedia, table 33)

**Fixing the headers**
The table came in with headers stacked three rows deep, so I flattened them and gave every column a short, simple name like `tinubu_votes` and `obi_pct`.

**Cleaning up state names**
The state names had Wikipedia footnote numbers stuck to them, like "Abia[632]". I stripped those out so Tableau can recognise the states on a map.

**Removing rows that weren't states**
The table had 39 rows, but Nigeria has 36 states plus the FCT. The two extra rows were a "Total" row and a blank row, so I dropped them. 37 rows left.

**Turning text into numbers**
Every column, even the vote counts, was stored as text. I removed the % signs and commas and converted them to real numbers. Nothing got lost in the process.

**Checking that the votes add up**
For each state, I checked whether the candidates' votes added up to the total valid votes. Two states didn't:

- **Yobe (off by 2,000):** Wikipedia had Atiku on 196,567, but Vanguard's INEC-declared results show 198,567. I checked it myself, and it's a one-digit typo. Fixed to 198,567, and Yobe now adds up perfectly.
- **Kwara (off by 40):** Vanguard has slightly different numbers for Obi (31,166 vs 31,186) and Kwankwaso (3,142 vs 3,141), but that only explains 19 of the 40 votes. Vanguard has typos of its own too, so I'm not fully trusting either source here. Flagged for now until I can check INEC's official declaration.

I also recalculated every candidate's percentage from the votes, and they all matched Wikipedia's, including Atiku in Yobe. That means Wikipedia's percentage was worked out from 198,567, which backs up that the vote count was the only typo.

**Checking the percentages**
I recalculated each candidate's share from the raw votes and compared it to Wikipedia's figures. Every state matched to within rounding.