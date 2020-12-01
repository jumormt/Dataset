# DeepWukong

> This is the repo for "DeepWuKong: Statically Detecting Software Vulnerabilities using Deep Graph Neural Network".

## Overview

We present XFG which contains both control-flow and data-flow information. We harvest a comprehensive vulnerability benchmark dataset from Software Assurance Reference Dataset (SARD), which hosts a large number of known realworld security flaws and create [a benchmark dataset for xfg](https://github.com/DeepWukong/DeepWukong/blob/master/data) related to top 10 most common C/C++ CVEs. 

We have conducted our experiments by comparing DeepWukong with the traditional static vulnerability detectors and three recent learning-based bug detection approachs. Here is the [comparative experiments result](https://github.com/DeepWukong/DeepWukong/blob/master/result.json). 

## Benchmark format

The benchmark is in [data](https://github.com/DeepWukong/DeepWukong/blob/master/data). The benchmark for each vulnerability category is named by their CWE id(e.g. 020.7z). 

XFG is stored in json's format, e.g.:

```json
{
    "testcaseid": "75932",
    "target": 0,
    "nodes": [
        "static void good2()",
        "char data[150], dest[100];",
        "if(globalReturnsTrue())",
        "memset(data, 'A', 149);"
    ],
    "edges": [
        [0,1],
        [1,2],
        [2,3]
    ]
}
```

The meaning for each key of the json:

  - "testcaseid" stands for the unique id(defined by [SARD](https://samate.nist.gov/SARD)) of the source code from which the XFG is extracted. It's easy to get the source code from [SARD search tab](https://samate.nist.gov/SARD/search.php) using the "testcaseid" for indexing. 
  - "target" for 0 means correct and 1 for vulnerble. 
  - "nodes" shows all the nodes of the XFG. 
  - "edges" stands for all the edges of the XFG(noting the number in "edges" means the index of node in "nodes").
