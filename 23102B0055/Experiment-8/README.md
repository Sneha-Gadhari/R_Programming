# Experiment 8: High Performance Big Data Analytics using R

**Course:** R Programming, B.E. Semester VII, Computer Engineering
**Institute:** Vidyalankar Institute of Technology, Department of Computer Engineering
**Student:** Sneha Gadhari (Roll No. 23102B0055)
**Faculty:** Prof. Sanjeev Dwivedi
**Platform:** Google Colab (R runtime)

---

## Objective

Build a high-performance and scalable analytics workflow in R on the NYC Yellow Taxi Trip dataset (about 9.4 million trips, January to March 2023). The experiment compares functional, vectorized, `data.table`, sequential and parallel implementations using execution time, memory use and scalability, and extracts demand, fare, route and payment patterns from the data.

## Folder Contents

```
Experiment-8/
├── R_Prog_Exp_8_23102B0055.ipynb                   # Complete R notebook (code and outputs)
├── R_Prog_Experiment-8_23102B0055_Sneha_Gadhari.pdf # Lab report (objective, description, outputs, conclusion)
└── README.md
```

## Dataset

| Dataset | Source | Format |
|---|---|---|
| Yellow Taxi Trip Records (Jan to Mar 2023) | [NYC TLC Trip Record Data](https://www.nyc.gov/site/tlc/about/tlc-trip-record-data.page) | Parquet |
| Taxi Zone Lookup Table | Same TLC page | CSV |

Both files are downloaded automatically by the notebook, so nothing needs to be uploaded manually.

## Tools and Packages

`data.table`, `ggplot2`, `foreach`, `doParallel`, `microbenchmark`, `bench`, `purrr`, `lubridate`, `scales`, `nanoparquet`

## How to Run

1. Open `R_Prog_Exp_8_23102B0055.ipynb` in Google Colab.
2. Go to **Runtime → Change runtime type** and select **R**.
3. Run all cells from top to bottom. The first cell installs the required packages, which takes a few minutes.
4. If Colab runs out of memory, reduce `1:3` to `1:2` in the `months` line of section 2.1.

## Workflow Summary

1. **Environment setup:** install and load packages, set seed.
2. **Data preparation (Task 1):** download and import data, inspect structure, detect missing and duplicate values, clean invalid records, convert types, extract hour, day, weekday and month, drop unneeded columns, and join pickup and drop-off zones.
3. **Transportation analytics (Task 2):** trips by hour, weekday and month, average fare and revenue by period, most frequent and highest-revenue routes, distance vs fare, payment methods by borough, and additional patterns (tipping, airport trips, speed).
4. **Functional vs vectorized vs data.table (Task 3):** `lapply`, `purrr::map`, `apply`, `map2`, `tapply`, vectorized base R and `data.table`, compared on time and memory.
5. **Parallel computing (Task 4):** 21 month × weekday partitions, bootstrap regression run sequentially and with `foreach` + `doParallel`, speedup and efficiency.
6. **Benchmarking (Task 5):** base R vs functional vs `data.table`, comparison table and scalability test.
7. **Visualization (Task 6):** `ggplot2` charts for demand, fare, revenue, zones, routes, payment types and distance vs fare.
8. **Analysis (Task 7):** fastest method per task and parallel speedup summary.

## Key Results

### Data Preparation

| Metric | Value |
|---|---|
| Raw trips | 9,384,487 |
| Clean trips | 8,763,337 (93.38% retained) |
| Memory after dropping timestamp columns | 787.6 MB → 702 MB |

### Analytics Highlights

- Demand peaks at 6 PM (628,711 trips) and is lowest at 4 AM (44,683 trips).
- Thursday is the busiest day (15.96%) and Monday the quietest (12.17%).
- March is the busiest month (3.17M trips, $89.5M revenue).
- Highest-revenue routes are airport routes, led by JFK Airport to Outside of NYC ($1.74M).
- Fare is strongly linked to distance (correlation 0.964, R² = 0.931, about $3.71 per mile plus $6.01 base).
- Credit card accounts for about 82% of trips and cash for about 17%.
- Airport trips are about 10% of all trips with an average fare of $55.70, against $14.49 for other trips.

### Performance Benchmarks (median times)

| Task | Method | Time | Relative to fastest |
|---|---|---|---|
| Average fare per hour (8.76M rows) | `lapply` | 1243.10 ms | 3.8× |
| | `purrr::map` | 1239.71 ms | 3.8× |
| | `tapply` | 659.00 ms | 2.0× |
| | vectorized `rowsum` | 348.61 ms | 1.1× |
| | `data.table` | 324.84 ms | 1.0× |
| Row-wise tip % (100k rows) | `apply` | 1169.50 ms | 653.4× |
| | `purrr::map2` | 254.10 ms | 142.0× |
| | vectorized `ifelse` | 3.06 ms | 1.7× |
| | `data.table` `fifelse` | 1.79 ms | 1.0× |
| Grouped mean (1M rows) | `aggregate` | 695.90 ms | 14.4× |
| | `split` + `lapply` | 560.03 ms | 11.6× |
| | `tapply` | 83.33 ms | 1.7× |
| | `data.table` | 48.25 ms | 1.0× |

Memory allocated for the hourly average: `lapply` and `map` used 1.67 GB, while vectorized `rowsum` and `data.table` used about 230 to 250 MB.

### Sequential vs Parallel

| Sequential | Parallel (2 cores) | Speedup | Efficiency |
|---|---|---|---|
| 29.88 s | 28.15 s | 1.06× | 53.1% |

The small gain is due to limited cores, the cost of copying partitions to workers, and uneven partition sizes. Results from both runs were identical.

## Notes and Limitations

- The route `N/A -> N/A` in the route tables refers to trips with unknown pickup and drop-off zones (zone IDs 264 and 265 in the lookup table).
- Cash tips are recorded as 0 in the source data, so average tip percentage reflects credit-card payments only.
- `data.table` ran with a single thread on the Colab runtime, and the machine had 2 CPU cores, which limits the parallel speedup.
- The `already exporting variable(s): boot_fit` warning in the parallel step is harmless.

## Conclusion

`data.table` gave the best performance in every benchmark: up to about 650 times faster than `apply` and 14 times faster than base `aggregate`, with about one-seventh of the memory of the `lapply`/`map` versions on the full dataset. Vectorized operations came a close second, while functional approaches are better kept for heavy per-group work. Parallel processing gave only a 1.06× speedup on 2 cores, which shows that parallelism does not always help when communication overhead is high. For large-scale analytics in R, `data.table` with vectorized column operations is recommended, with `foreach`/`doParallel` added only after measuring that the speedup is worth it.
