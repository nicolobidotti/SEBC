## Spreadsheets adjustments

Change memory for DataNode to 5GB (cell B10) to account for caching memory (1GB process + 4GB cache).

Change "yarn.scheduler.maximum-allocation-vcores" (cell F6) from 4 to 8 to better support workloads that like more cores per container (eg Spark Executors).

Change calculation for "yarn.scheduler.maximum-allocation-mb" (cell F9) to be # of cores times 2048 to better support workloads that are memory-intensive (eg Spark Executors for applications with a lot of data cached in-memory).

Change "yarn.app.mapreduce.am.resource.mb" (cell F19) from 1 to 1024 as it is in MB.

Change formulas for "-D mapreduce.job.maps" and "-D mapreduce.job.reduces" (cells F27 and F28) to multiply workload factor by # of spindles and not nodes.

Note: Gateway settings double memory resources for mappers and quadruple them for reducers.

## Workload factor

The workload factor is used to account for how much a workload is CPU or IO bound; it should be lower for CPU-bound (say 1) and higher for IO-bound (say 4). 2 is adequate for most workloads.
