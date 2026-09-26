# Autonomous Task Queue

Complete tasks in order. Do not start the next task until QA passes the current task.

- [ ] 8C.1 Implement low-memory streaming Stage8C inference
- [ ] 8C.2 Run 2,000-5,000 query smoke test
- [ ] 8C.3 QA smoke-test schema, alignment, runtime, and memory
- [ ] 8C.4 Run full 35-chunk Stage8C inference with resume
- [ ] 8C.5 QA all prediction chunks and exact row coverage
- [ ] 8D.1 Aggregate q_idx, candidate_id, probability
- [ ] 8D.2 Generate final query-wise matching
- [ ] 8D.3 Generate final candidate_pairs from frozen Stage8B output
- [ ] 8D.4 Run official validator
- [ ] 8D.5 Create final submission artifact
- [ ] 8D.6 Final independent QA and upload preparation

## Execution policy

The Builder owns implementation and production runs.

The QA agent owns validation.

If a task fails:
1. Do not mark it complete.
2. Record the failure.
3. Apply the smallest safe fix.
4. Re-run the failed task.
5. Re-run dependent validation.

## Time policy

Protect enough time for final validation and submission.

Do not spend the final hour on optional optimization.
