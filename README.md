# k6-lab

ITDS362 Software Quality Assurance and Testing: Performance Testing with Grafana k6.

## Results

See [RESULTS.md](RESULTS.md) for Part 0 observations, the A1–A5 results table, and all nine Part B answers.

Download the HTML reports and open them in a browser:

- [A2: Average load](reports/a2-average.html)
- [A3: Stress](reports/a3-stress.html)
- [A4: Spike](reports/a4-spike.html)
- [A5: Soak](reports/a5-soak.html)

## Run

Run from this folder with k6 installed. Run one test at a time; never exceed 5 VUs against this shared QuickPizza site. The 11-minute, 2-VU soak test is the exercise's only exception to the three-minute limit.

```sh
k6 run a1-smoke.js
k6 run --out web-dashboard=export=reports/a2-average.html a2-average.js
k6 run --out web-dashboard=export=reports/a3-stress.html a3-stress.js
k6 run --out web-dashboard=export=reports/a4-spike.html a4-spike.js
k6 run --out web-dashboard=export=reports/a5-soak.html a5-soak.js
```

A4 stages: 1 VU for 30s, rise to 5 in 5s, hold 30s, fall to 1 in 5s, hold 60s, fall to 0 in 10s. A5 stages: rise to 2 in 30s, hold 10m, fall to 0 in 30s. All Part A scripts import the same `journey.js`.

`07-requirement.js` preserves the deliberately tightened `p(95)<1` requirement from Step 0.7; it is expected to fail. `08-bug-hunt.js` contains the corrected case-sensitive exclusion names. A threshold failure produces exit code 99; do not remove a threshold just to make a report pass.

## Test evidence

Runs were collected on 30 October 2026 (Asia/Bangkok), using k6 v2.3.0 on macOS. A2/A3 retain the original reports; A1, A4/A5 and missing Part 0 measurements were collected later. These are separate runs against a shared public site.

`reports/data/` is optional supporting evidence, not a required deliverable in the exercise. It is retained to verify the numbers in `RESULTS.md`: console logs, exit codes, JSON summaries, and compressed A4/A5 request metrics. A2/A3 summaries are decoded from the original HTML reports; trend arrays are ordered `avg, max, med, min, p(90), p(95), p(99)`.

The saved phase summaries use request completion timestamps relative to the dashboard start and linearly interpolated percentiles. Soak comparisons use equal two-minute windows at 2 VUs; spike recovery uses ten-second windows. Small samples and internet/shared-site variability limit causal conclusions.

A1 and A5 passed their thresholds. A2, A3 and A4 exceeded the home-page p95 threshold; these measured failures are retained in the results. A4 exited with code 99. Original A2/A3 console exit codes were not saved, so their threshold outcomes are read from the HTML reports.
