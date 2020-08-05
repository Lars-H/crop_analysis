# CROP - Supplemental Material

Supplemental material to "CROP: Cost- and Robustness-based Query Optimization for Triple Pattern Fragment Clients". 


## Notebooks

The `notebooks` directory provides Jupyter Notebooks used for the analysis of the experimental results.
This included the analyses presented in the paper as well as additional analysis and results for further insights.

## Experimental Results

The `experimental_results` directory contains all raw results from the experimental studies as *tab-separated* files.

### Cost Model and IDP Parameters

- Cost Model Parameter: delta (`01_cost_model_parameter_delta.tsv`)
- IDP Parameter: block size k (`02_idp_parameter_block_size_k.tsv`)

### Robustness and Cost Threshold

- Query plan optimizer parameter: rho and gamma (`03_qpo_parameter_rho_gamma.tsv`)
- Custom benchmark: CROP (`04_custom_benchmark_crop.tsv`)

### Comparison to other TPF Clients

In addition to executing the engines and record the runtime, we also conducted an additional run to record the number of requests.
This avoids that the additional logging required to obtain the requests affects the runtime performance. 

#### Runtimes
- Runtimes: Comunica (`05_runtimes_comunica.tsv`)
- Runtimes: nLDE (`07_runtimes_nlde.tsv`)
- Runtimes: CROP (`09_runtimes_crop.tsv`)

#### Requests
- Requests: Comunica (`06_requests_comunica.tsv`)
- Requests: nLDE (`08_requests_nlde.tsv`)
- Requests: CROP (`10_requests_crop.tsv`)

#### Diefficiency

- Diefficiency: Raw results for all engines and queries including the elapsed time for each answer that is produced (`11_diefficiency_raw_results.tsv`)
- Diefficiency: dief@t (t = maximum runtime across all engines per query) for all queries and engines (`12_diefficiency_at_tmax_per_query.tsv`)

Note: In order to compute the diefficiency for Comunica we made two additions to the original code. First, added a log message with the timestamp when the engines is called (in `actor-init-sparql/bin/query.js`). Second, for each answer that is produced, we also logged the timestamps (in `ActorSparqlSerializeJson.js`).

#### Additional Results: nLDE Benchmark Q11-Q20
- Runtimes: CROP (`13_runtimes_nLDE_Q11_20_crop.tsv`)
- Runtimes: nLDE (`14_runtimes_nLDE_Q11_20_nlde.tsv`)
- Runtimes: Comunica (`15_runtimes_nLDE_Q11_20_comunica.tsv`)

## Queries

The `queries` directory contains all queries used for the experimental studies.

- nLDE Benchmark: Queries from the nLDE benchmark used for the evaluation.
- WatDiv: Queries for the WatDiv benchmark created using the provided CLI with query-count=5.
- Custom Benchmmark: Additional benchmark with 10 queries for 3 datasets (DBpedia 2014, GeoNames, DBLP) that include either a subject-object and or an object-object join and 3-4 triple patterns. Query files include a brief comment explaining the query.

## Source Code

The source code is provided in the [CROP Repository](https://github.com/Lars-H/crop).
