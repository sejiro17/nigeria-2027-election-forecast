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

**Matching state names across datasets**
When I compared the 2023 results with the 2027 register, the FCT didn't match: Wikipedia wrote it as "F.C.T." and the register uses "FCT". I standardised it to "FCT" in the cleaning notebook.

Lesson learned: my first "Run All" silently stopped at an old error cell, so the cleaned file never re-saved. I deleted that cell, re-ran, and confirmed the fix.

## 2027 Voter Register (preliminary, INEC, Oct 2026)

**Where the data came from**
INEC only published the figures as an image, with no state-by-state table. So I built the CSV by hand from news reports quoting the INEC chairman: Punch (via Substack) for all 37 states, plus ThisDay, Daily Trust and others for exact figures.

**Exact vs rounded**
15 states have exact figures. The other 22 were only reported rounded to the nearest 10,000, so I added a `precision` column to mark which is which.

**Conflicts I found**
- Yobe: one outlet listed 1,733,641 under Ondo instead. Punch puts Ondo at 2.12 million, so 1,733,641 belongs to Yobe.
- Gombe: outlets disagree, 1,768,566 vs 1,768,560. Marked "disputed".

**Sum check**
Total: 103,456,535 vs INEC's 103,428,715, a difference of 27,820 (0.03%). That's within the range expected from rounding 22 states, so no typos.

**Zone check**
I added geopolitical zones and compared each zone's total with INEC's official figures. All six are within about 14,000, and the gaps add up to exactly 27,820, the same as the national sum check. The South East has the biggest gap because all five of its states are rounded figures.

**To update**
This is the preliminary register. INEC publishes the final one on 15 December 2026, so I'll swap in the official figures then.

## 2027 Oxford-Metro Poll (by zone)

**Where the data came from**
The poll was only reported in a news article (P.M. News), not as a table, so I built the CSV by hand from the zone figures in the text.

**Filling the gaps**
The article left out some zone numbers. For Tinubu and Obi, only one zone was missing each, so I worked it out as their national total minus the zones I had:
- Tinubu, South East: 694
- Obi, North West: 1,613

I sanity-checked both: the three candidates' numbers stayed below the zone's participants. Atiku had two missing zones (North Central and South West), so there's no way to split them. I left those blank.

**Checking the percentages**
I calculated each candidate's share per zone and compared it with the article's figures, for example Tinubu North West 43.10%, Obi South East 63.97% and Atiku North East 55.46%. All matched.

**Limitations**
- The zones add up to 69,054, not the 69,110 total, so 56 responses have no zone. My two filled numbers could be off by up to 56.
- It's a self-selected online poll and not weighted. Lagos and the FCT make up over half the responses, and the North East has only 2,227.
- Because of this, I use the poll to nudge the 2023 baseline, not to replace it.