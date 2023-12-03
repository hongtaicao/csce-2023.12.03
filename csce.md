# CSCE
* Graph Clustering (C)
* Sequential Candidate Equivalence (SCE)

## Quick Start
* for ``Little Endian x86_64 Ubuntu 20.04.5 LTS`` machine
* Google Drive [https://drive.google.com/drive/folders/1_6798opIzweOpIDbTO9KxDJHrDkuwqWH?usp=sharing](https://drive.google.com/drive/folders/1_6798opIzweOpIDbTO9KxDJHrDkuwqWH?usp=sharing)
* download and unzip the dataset ``edgelist.zip`` (only in Google Drive)
* download and unzip the binary ``release.zip`` (only in Google Drive)
* download the test script ``csce.txt`` (also in the code ``script/sce.txt``)
* organize files as the following
```
root-directory
    + edgelist/
    + release/
        + bin/csce.txt
        + profiling.exe
        + release.exe
        ...
```
* command
```bash
bash bin/csce.txt
```

## Example
* command
```bash
./release-hprd-EdgeInduce.exe -isomorphism EdgeInduce -algorithm WCOJ -graph-storage CSR.1 -order-generator RIDataGraph -order-generator-add DAG -is-labeled 1 -data-file ../edgelist/hprd-VEQ/hprd.txt -query-file ../edgelist/hprd-VEQ/nonsparse/200/q0.txt
```
* command explanation
    - ``-isomorphism`` should match the release target, ``EdgeInduce/VertexInduce/Homomorphism``.
    - ``-algorithm WCOJ`` should not change. Otherwise, undefined behavior.
    - ``-graph-storage CSR.1`` enable the clustered CSR data structure.
    - ``-order-generator RIDataGraph`` enable our proposed heuristics of ``Eq.1`` and ``Eq.2``.
    - ``-order-generator-add DAG`` enable improved matching order by SCE DAG.
    - ``-is-labeled 1`` has to match the dataset, ``0/1``. Otherwise, undefined behavior.
* truncated output
```
...
DurationReadBinaryGraph(s)=0.087
Default: COUNTING
DurationExecutionCompile(s)=0.005 MatchCount=3456
...
```
* output explanation
    - DurationReadBinaryGraph(s)=0.087: the total reading time is 0.087 seconds
    - Default: COUNTING: output the number of results
    - DurationExecutionCompile(s)=0.005: the subgraph matching time
    - MatchCount=3456: the number of EdgeInduce subgraphs
    - Therefore the total time is 0.087 + 0.005 = 0.092 seconds.


## Compile the Program
* require ``make`` and ``g++``
* download and unzip ``sce.zip``
* go to the directory of ``Makefile``
* compile ``make release``
* compile file is ``release.exe``


## Dataset Format
* please find examples in Google Drive ``edgelist.zip``
* both are text files of the same format, can be either unlabeled or labeled
* including ``vertex id``, ``vertex label``, ``edge label``
* ``vertex id`` should be consecutive integers from 0
* ``vertex label`` should be consecutive integers from 0
* ``edge label`` should be consecutive integers from 0
* unlabeled graphs format
    - ``a b``
    - represent an edge a->b
    - an undirected edge a--b should be two lines, one for a->b, one for b->a
* labeled graph format
    - ``a b la lb le``
    - represent an edge a->b
    - vertex ``a`` label is ``la``, vertex ``b`` label is ``lb``
    - a directed edge a->b label is ``le``
    - an undirected edge a->b, b->a should have the same edge label

## Other Note
* Architecture ``lscpu``
* OS version ``cat /etc/os-release``
