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

## Kwankwaso's voters now lean towards Obi
The SBM Intelligence report (June 2026) shows Kwankwaso left the ADC with Obi to form the NDC, so his 2023 voters are more likely to back Obi than to split evenly.

I changed the random split of his voters from equal (1, 1, 1) to leaning towards Obi (2, 6, 2), in the order Tinubu, Obi, Atiku. On average that sends about 60% to Obi and 20% each to Tinubu and Atiku, with variation in every simulation. These weights are my own assumption, not from a source.

Result:
- Equal split: Tinubu 63.8%, Atiku 19.1%, Obi 0.7%, runoff 16.4%
- Leaning to Obi: Tinubu 61.6%, Atiku 18.6%, Obi 1.2%, runoff 18.6%

Finding: the alliance barely helps Obi. Kwankwaso's 2023 votes were concentrated in Kano and nearby states, so they don't help Obi reach 25% in enough northern states.

## Coalition scenario: Atiku joins Obi
There are reports that Atiku may join Obi in the NDC (unconfirmed as of November 2026). To test it, I added a coalition option to the simulation: Atiku drops out, and a share of his voters moves to Obi, with the rest going to Tinubu. How many follow him is my own assumption, so I tested two ranges.

Results (10,000 simulations each):
- As things stand: Tinubu 61.6%, Atiku 18.6%, Obi 1.2%, runoff 18.6%
- Coalition, 60–90% of Atiku voters follow: Obi 82.2%, Tinubu 17.8%, runoff 0%
- Coalition, 40–70% of Atiku voters follow: Tinubu 66.3%, Obi 33.7%, runoff 0%

Finding: a coalition alone doesn't decide the election. The outcome flips depending on how many of Atiku's voters actually follow him to Obi. There are no runoffs, because in a two-way race the winner almost always clears 25% in 24 states.