# Autonomous Competition Agents

## Project objective
Finish the multi-source business entity-resolution competition safely within the remaining deadline.

## Roles

### BUILDER
- Implement the next task only.
- Inspect existing checkpoints and source before changing code.
- Run a small smoke test before full production.
- Commit every stable milestone.
- Never overwrite a verified checkpoint.
- Never change locked retrieval, features, or frozen models.
- Prefer minimal changes over rewrites.

### QA
- Independently inspect Builder changes and runtime output.
- Verify schemas, row counts, candidate IDs, query alignment, memory, determinism, checkpoints, and output completeness.
- PASS only when all required checks succeed.
- On FAIL, report the exact root cause and the smallest safe fix.
- Do not redesign the architecture unless a correctness or runtime issue requires it.

## Hard safety rules
- No all-pairs matching.
- No external entity lookup or data augmentation.
- Do not load all S1/S2/S3 metadata into pandas simultaneously.
- Do not construct the full 66M x 36 feature matrix in memory.
- Use chunked/streaming processing.
- Use float32 features.
- Preserve the exact 36-feature schema.
- Reuse the five frozen LightGBM models.
- Stage8A and Stage8B are frozen inputs.
- Do not modify frozen checkpoints.
- Never continue after a failed validation.
- Do not use bare assert for runtime validation.
- Do not use SystemExit for ordinary control flow.
- Every production stage must be resumable.
- Candidate generation must remain a strict superset of final matching.
- Final matching must be a subset of candidate_pairs.

## Current verified state
- Stage8A full test indexing: PASS
- Stage8B full test candidate generation: PASS
- Stage8C index loading: PASS
- Stage8C feature/inference production: NEXT

## Compute
- Kaggle notebook environment
- Approximately 30 GB RAM
- RAM safety target: below 22 GB working set

## Deadline
Treat time as a hard constraint. Finish a valid submission before attempting optional optimization.
