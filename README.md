# Supplemental Material - Overview

## Experimental Results

This directory contains all raw results from the experimental studies as tab-separated files.

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

Note: In order to compute the diefficiency for Comunica we made two additions to the original code. First, added a log message with the timestamp when the engines is called (in `actor-init-sparql/bin/query.js`). Second, for each answer that is produced, we also logged the timestamp (in `ActorSparqlSerializeJson.js`).

- Diefficiency: Raw results for all engines and queries including the elapsed time for each answer that is produced (`11_diefficiency_raw_results.tsv`)
- Diefficiency: dief@t (t = maximum runtime across all engines per query) for all queries and engines (`12_diefficiency_at_tmax_per_query.tsv`)

## Source Code

This directory contains the source code for the implementation of CROP.
We re-used the code of the nLDE engine implemented in Python 2.7 and additional implemented our cost-model, robustness computation and the query plan optimizer to compute the query plans to be executed.

### Installation

In the directory, a virtual environment (`venv` directory) is provided to execute the engine.
*Alternatively*, you can install the requirements provided in the `requirements.txt` file to a local Python using pip:
```bash
pip2 install -r requirements.txt
```

It is advised to use a virtual environment for the installation.
Once the requirements are installed, the engine can be executed using the command line.

### Usage

Example: 
```
venv/bin/python crop.py -f example.rq -s http://fragments.dbpedia.org/2014/en 
```
(Note that the engine currently only supports conjunctive SPARQL queries.)


### Help

You can find the help using:
```bash
venv/bin/python crop.py -h
```
and get the usage options:
```bash
usage: crop.py [-h] [-s SERVER] [-f QUERYFILE] [-q QUERY] [-r {y,n,f,all}]
               [-e EDDIES] [-p {NoPolicy,Ticket,Random}] [-t TIMEOUT]
               [-v {INFO}] [-d HEIGHT_DISCOUNT] [-c COST_THRESHOLD]
               [-u ROBUST_THRESHOLD] [-k K] [-a {True,False}] [-b TOP_T]

CROP: An nLDE-based TPF Client with a cost model-based robust query plan
optimizer

optional arguments:
  -h, --help            show this help message and exit
  -s SERVER, --server SERVER
                        URL of the triple pattern fragment server (required)
  -f QUERYFILE, --queryfile QUERYFILE
                        file name of the SPARQL query (required, or -q)
  -q QUERY, --query QUERY
                        SPARQL query (required, or -f)
  -r {y,n,f,all}, --printres {y,n,f,all}
                        format of the output results
  -e EDDIES, --eddies EDDIES
                        number of eddy processes to create
  -p {NoPolicy,Ticket,Random}, --policy {NoPolicy,Ticket,Random}
                        routing policy used by eddy operators
  -t TIMEOUT, --timeout TIMEOUT
                        query execution timeout
  -v {INFO}, --verbose {INFO}
                        print logging information
  -d HEIGHT_DISCOUNT, --height_discount HEIGHT_DISCOUNT
                        Discount for NLJ higher in the plan (Optional)
  -c COST_THRESHOLD, --cost_threshold COST_THRESHOLD
                        Cost threshold for the query plan optimizer(Optional)
  -u ROBUST_THRESHOLD, --robust_threshold ROBUST_THRESHOLD
                        Robustness threshold for the query plan
                        optimizer(Optional)
  -k K, --k K           Parameter k in IDP (Optional)
  -a {True,False}, --adaptive_k {True,False}
                        Adaptive k (Optional)
  -b TOP_T, --top_t TOP_T
                        Top t plans to consider in IDP
                        (Optional)
```


## Queries

This directory contains all queries used for the experimental studies.

- nLDE Benchmark: Selection of queries from the nLDE benchmark used for the evaluation. Benchmark 1: Q1-Q10; Benchmark 2: All queries.
- WatDiv: Queries for the WatDiv benchmark created using the provided CLI with query-count=5.
- Custom Benchmmark: Additional benchmark with 10 queries for 3 datasets (DBpedia 2014, GeoNames, DBLP) that include either a subject-object and or an object-object join and 3-4 triple patterns. Query files include a brief comment explaining the query.
