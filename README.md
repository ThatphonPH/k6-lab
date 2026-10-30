# k6-lab

ITDS362 Software Quality Assurance and Testing: Performance Testing with Grafana k6.

## Results

See [RESULTS.md](RESULTS.md) for test results and reflections.

Download the HTML reports and open them in a browser:

- [A2: Average load](reports/a2-average.html)
- [A3: Stress](reports/a3-stress.html)
- [A4: Spike](reports/a4-spike.html)
- [A5: Soak](reports/a5-soak.html)

## Run

With k6 installed, run these commands one at a time from this folder. The scripts use at most 5 VUs; the soak test runs for 11 minutes with at most 2 VUs.

```sh
k6 run a1-smoke.js
k6 run --out web-dashboard=export=reports/a2-average.html a2-average.js
k6 run --out web-dashboard=export=reports/a3-stress.html a3-stress.js
k6 run --out web-dashboard=export=reports/a4-spike.html a4-spike.js
k6 run --out web-dashboard=export=reports/a5-soak.html a5-soak.js
```
