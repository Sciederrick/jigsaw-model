# health-data-linkage tool

- CLI and web-based interface to complete record linkage tasks - single click execution.

- Pre-trained models to allow reuse when used by similar datasets

**Implementation**

- Schema matching: automated field type detection

- Preprocessing: data cleaning; each field has a custom cleaning function. Cleaning can be invoked from the CLI.

- Blocking: fuzzy search (using Ultra-fast search algorithm) to group similar records to avoid cartesian product comparisons. Block records based on patient names (by default). Specify custom block sizes (e.g 10, 20, 30 etc)

- Comparison: utlize more than one algorithm for string matching. Output a matrix of scores for each of the utilized string matching algorithms

- Scoring - use pre-trained models (e.g., random forest) to aggregate comparison results into a single probabilistic score (0-1)

- Evaluation - ascertain the quality of the linkage. E.g., use AUC, Precision, Recall. Leverate truth dataset or estimate from the synthetic datasets.

- Output: keep only matches above a certain probability threshold. Store results in a target file (e.g., CSV, XLSX). Return top records for clerical review.

Input(2CSV files) --> Schema --> Preprocess --> Block --> Compare --> Score --> Evaluate --> Output(target file with matched records)

| Input | Schema | Preprocess | Block | Compare | Score | Evaluate | Output
|---|---|---|---|---|---|---|---|
| 2 datasets | standardize columns | clean data | filter records to compare using fuzzy search on select columns | apply comparison algorithms, output a matrix of scores from the algorithms | use the matrix of scores from the algorithms as an input for a machine learning algorithm, output a probability score (0-1) | Use a truth dataset to measure accuracy (AUC-ROC, Precision, Recall), output top-N rows for clerical evaluation | Store result in another file or table |

```bash
hdl-tool run --src file.csv --target out.csv
```


