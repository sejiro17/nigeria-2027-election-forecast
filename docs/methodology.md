# Methodology

## How the forecast works
1. Start from each state's actual 2023 result.
2. Add part of the zone swing from the Oxford-Metro poll (randomly between 20% and 80% of it), because the poll is a self-selected online sample.
3. Run 10,000 simulated elections, each with random nationwide shocks (about ±5 points per candidate), zone-level shocks (about ±3 points), and turnout changes (about ±10%).
4. A candidate wins outright with the most votes nationally and at least 25% in 24 of the 37 states plus FCT. Otherwise it's counted as a runoff.

## Online poll bias test
Online polls overstated Obi in 2023. Most pre-election projections predicted an Obi win, but Tinubu won with 36.61% (TheCable). An SBM Intelligence poll projected Obi would cross 25% in 25 states (Premium Times), but he won only 12 states. Oxford-Metro also describes its own 2027 poll as self-selected and unweighted.

Sources:
- https://www.thecable.ng/nigeriadecides2023-so-many-pre-election-projections-and-plenty-f9s/
- https://www.premiumtimesng.com/news/587189-nigerias-2023-presidential-election-inside-the-opinion-polls-that-got-it-wrong.html
- https://dailytrust.com/youths-influencers-and-2027-can-social-media-sway-votes/

So by default I subtract 3 points from Obi's poll swing. The 3 is my own assumption, not a figure from any source.
- With a 3-point correction: Tinubu 63.0%, Atiku 17.6%, Obi 0.3%, runoff 19.0%
- With no correction: Tinubu 61.8%, Atiku 17.1%, Obi 0.9%, runoff 20.3%

Finding: the correction barely changes the result. What really limits Obi is geography and the 25% rule. His support is concentrated in the South, so he rarely clears 25% in 24 states.

## Why I added nationwide shocks
My first version only had zone-level randomness, which mostly cancelled out and gave Tinubu 96.9%. That was overconfident, so I added nationwide shocks to reflect how real elections move.

## Kwankwaso's 2023 voters
Kwankwaso won over 1.5 million votes in 2023, mostly in Kano, but he isn't in the 2027 poll, so the model was ignoring those voters. In each simulation, I now split his 2023 share randomly between Tinubu, Obi and Atiku, because there's no data on where they'll go.

Result:
- Before: Tinubu 63.0%, Atiku 17.6%, Obi 0.3%, runoff 19.0%
- After: Tinubu 63.8%, Atiku 19.1%, Obi 0.7%, runoff 16.4%

Atiku gains the most, since Kwankwaso's base overlaps with his northern support. Runoffs drop because more candidates clear 25% in northern states. Tinubu remains the favourite.