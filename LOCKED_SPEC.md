# Locked Competition Specification

## Frozen production inputs

### Stage8A
Path:
checkpoints/stage8a_test_indexing_v1

Status:
PASS

### Stage8B
Path:
checkpoints/stage8b_full_test_v1

Status:
PASS

Expected:
- Queries: 1,732,544
- Candidate IDs: 66,226,684
- Mean candidates/query: 38.225
- Maximum candidates/query: 100
- Chunk files: 35

## Candidate chunk schema

Each Stage8B .npz contains:
- q_start
- q_end
- n_queries
- candidate_counts
- candidate_ids

Decode candidate_ids using the cumulative candidate_counts within each chunk.

## Frozen feature schema

Exactly 36 features, in this order:

1. retrieval_rank
2. retrieved_by_A
3. retrieved_by_B
4. retrieved_by_C
5. retrieved_by_E_exact
6. retrieved_by_E_comp
7. A_rank
8. B_rank
9. A_and_B
10. A_and_C
11. B_and_C
12. E_and_name_match
13. c_overlap_count
14. c_idf_sum
15. c_max_idf
16. c_token_coverage
17. name_jw
18. lev_ratio
19. char_tri_jaccard
20. exact_name
21. token_jaccard
22. token_containment
23. token_set_equal
24. shared_token_count
25. first_tok_match
26. last_tok_match
27. q_tok_len
28. c_tok_len
29. tok_len_diff
30. char_len_diff_ratio
31. address_exact_match
32. postal_match
33. addr_token_jaccard
34. shared_addr_tokens
35. country_match
36. is_s2

## Frozen E_and_name_match rule

E_and_name_match is 1 when:
(E1a OR E1c) AND (exact_name OR name_jw >= 0.85)

Otherwise 0.

## Frozen model ensemble

Five saved LightGBM models.

Best iterations from training:
[494, 420, 391, 325, 495]

Use zero-shot inference. Do not retrain on test.

## Feature matrix policy

Never create the complete 66,226,684 x 36 matrix in RAM.

Process candidates in chunks and use float32.

Persist prediction outputs as:
q_idx, candidate_id, ensemble_probability

Do not persist every feature unless required for debugging.

## Final matching constraints

- Every matching pair must exist in Stage8B candidate_pairs.
- No generated match may bypass the candidate set.
- Candidate generation is frozen.
- Validate the final submission using the competition's official validator before upload.

## Forbidden changes during deadline

- No new blocking channel.
- No new model architecture.
- No model retraining.
- No feature-schema changes.
- No Stage8A rebuild.
- No Stage8B rebuild.
