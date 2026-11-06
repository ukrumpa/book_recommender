# Experiment Results

These results were extracted from the saved outputs in `notebooks/book-recommender-system.ipynb`. The experiment was **not rerun** during extraction.

## Evaluation setup

| Setting | Value |
|---|---:|
| Rows available before sampling | 62,191 |
| Sampled rows | 25,075 |
| Sample fraction | 0.402 |
| Training rows | 17,605 |
| Validation rows | 3,725 |
| Test rows | 3,745 |
| Ranking cutoff | Top-10 |
| Relevant rating threshold | 8 |

## Best validation configurations

| Model | Selected parameters |
|---|---|
| ALS | `{"rank":12,"max_iter":15,"reg_param":0.05}` |
| FMRegressor | `{"factor_size":8,"reg_param":0,"step_size":0.05}` |
| XGBRanker | `{"n_estimators":30,"max_depth":4,"learning_rate":0.05,"min_child_weight":1}` |

## Final test performance

| Model | NDCG@10 | MAP@10 | Precision@10 | Recall@10 | Coverage | Eligible users | Users scored | Scored rows |
|---|---:|---:|---:|---:|---:|---:|---:|---:|
| ALS | 0.8416 | 0.8152 | 0.7194 | 0.9598 | 0.2096 | 120 | 130 | 785 |
| XGBRanker | 0.7007 | 0.6798 | 0.673 | 0.6752 | 1 | 139 | 144 | 3745 |
| FMRegressor | 0.5927 | 0.5582 | 0.6097 | 0.6165 | 1 | 139 | 144 | 3745 |

## Interpretation

- **ALS** achieved the highest NDCG@10 (0.8416), MAP@10 (0.8152), Precision@10 (0.7194), and Recall@10 (0.9598) on this saved test output.
- **XGBRanker** achieved full catalog coverage (1.0), with NDCG@10 of 0.7007.
- **FMRegressor** achieved NDCG@10 of 0.5927 and full catalog coverage (1.0).
- Coverage and ranking metrics should be interpreted together: the evaluated user/item candidate sets differ between approaches, as reflected in the eligible-user and scored-row counts. This makes direct comparisons less straightforward.

## Reproducibility

The saved notebook output reports a 70/15/15 random split with seed 42 and relevance threshold 8.0. See the notebook for preprocessing, model definitions, tuning grids, and metric implementation.

Files:
- `final_test_metrics.csv`: compact final test metrics.
- `results.json`: machine-readable split, selected parameters, metrics, and saved validation output.
- `validation_and_test_results.md`: this report.
