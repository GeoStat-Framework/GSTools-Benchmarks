GSTools-Benchmarks — published performance history
===================================================

This repository contains the **published benchmark history** for
[GSTools](https://github.com/GeoStat-Framework/GSTools). It is **generated and
updated automatically by GSTools' CI** 

> Do not edit this repository by hand. Its contents (results, report, landing
> page) are overwritten by the GSTools publish workflow on every accepted
> change. Manual commits will be force-pushed over.

What this is
------------

GSTools tracks the runtime and peak memory of representative two-point
statistics workflows — variogram estimation, global kriging, and (conditioned)
random field generation — on the GSTools-Core (Rust) backend, across thread
counts. This repo stores one measurement per commit merged to GSTools `main`,
so the published site shows how performance evolves over the project's history.

Measurements are produced with [Airspeed Velocity (ASV)](https://asv.readthedocs.io).
For what each case does and how to run the benchmarks yourself, see the
benchmark guide in the main repository:
[`benchmarks/README.md`](https://github.com/GeoStat-Framework/GSTools/blob/main/benchmarks/README.md).

How it is updated
-----------------

The `asv-benchmark-publish.yml` workflow in `GeoStat-Framework/GSTools` runs on
every push to `main` that touches benchmark-relevant paths. For each accepted
commit it:

1. restores the cumulative results already stored here,
2. benchmarks the newly accepted commit on a fixed CI machine
   (`github-actions-ubuntu`),
3. appends the new result and rebuilds the report, then
4. commits and pushes the updated history back to this repository.

Pull-request benchmarks are **not** stored here — those run per-PR and are only
posted as PR comments. This history contains one clean data point per merged
commit.

Layout
------

```
index.html     redirect to asv/index.html (the landing page)
asv/           native ASV HTML report — interactive, per-commit history
results/       raw ASV result JSON — the source of truth
.nojekyll      disables Jekyll so the static site is served as-is
```

Reading the results
--------------------

- Compare performance **commit-over-commit on the same CI machine**. Absolute
  times are **not** comparable across different machines, so treat the numbers
  as relative trends, not hardware benchmarks.
- The PR comparison uses ASV's Mann-Whitney U test at a 5% threshold; a `~`
  marker means the ratio moved but the change was not statistically
  significant on the (shared, noisy) runner.
- `time_*` benchmarks measure runtime; `peakmem_*` measure whole-process peak
  memory.


Links
-----

- GSTools: https://github.com/GeoStat-Framework/GSTools
- Benchmark guide: https://github.com/GeoStat-Framework/GSTools/blob/main/benchmarks/README.md
- Airspeed Velocity: https://asv.readthedocs.io
