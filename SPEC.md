# Spec: Ultra-fast TSP/Routing Engine for RL (PufferLib Ocean env, C core)

Goal: Add a new Ocean environment implemented in C inside a fork of PufferLib, optimized for very high-throughput RL.
Primary interface is Ocean/PufferLib; no standalone separate package.

Deliverables:
- New env module: pufferlib/ocean/tsp_fast/
  - tsp_fast.h, tsp_fast.c, binding.c, tsp_fast.py (mirror existing C env patterns)
- Wired into Ocean registry (ocean/environment.py or current equivalent)
- Config ini under pufferlib/config/ocean so `puffer train puffer_tsp_fast` works
- Deterministic per-env RNG
- Batched reset/step; no per-step heap allocations
- Action masking (bitset internal + expanded output for frameworks)
- Obs buffers are contiguous and exposed without per-env copying where possible
- Bench: steps/sec for (B=1024,n=100) and (B=256,n=500)
- Tests: masking correctness, reward correctness, termination logic
