CLASSIFY: L2(qlv SI1语义应答·vinf代铸轨SEMANTIC-RESPONDER-01·覆写权归原线)
# outbox/ANS-SEM-TASK-BEAT173-LINEAGE-COLLAB-01-qlv-20261121.md

应卡: inbox/TASK-BEAT173-LINEAGE-COLLAB-01-qlv-20261121.md
引擎: DEEPSEEK_API_KEY/deepseek-chat usage={"prompt_tokens": 39, "completion_tokens": 451, "total_tokens": 490, "prompt_tokens_details": {"cached_tokens": 0}, "prompt_cache_hit_tokens": 0, "prompt_cache_miss_tokens": 39}

Understood. To proceed I need the specifics of what "upstream minimal data fixture" and "validator" refer to in your project. I don't have enough context yet to supply either correctly, and guessing would risk giving you a fixture/validator that doesn't match the real task. Please provide the following, and I'll return:

1. **A minimal upstream data fixture** — labeled `SYNTHETIC` if it's generated/stand-in, with a note that the real-data scientific task remains `OPEN`.
2. **An executable validator** — a runnable script (I'll pick the language/form based on your stack) that checks the fixture against the inferred contract (schema, units, ranges, invariants, provenance fields).

To do that, I need:

- **The pipeline/context**: what upstream stage produces the data, what downstream consumes it, and the file format(s) involved (JSON/CSV/Parquet/NetCDF/HDF5/etc.).
- **The data contract**: expected fields, dtypes, units, allowed ranges, required provenance metadata, and any invariants (e.g., monotonic timestamps, no NaNs in key columns, checksum stability).
- **Validator environment**: language/runtime you want (Python/Node/Rust/…), whether it must run in CI, exit-code conventions, and any existing schema files (JSON Schema, Pydantic, Pandera, Avro, etc.) to conform to.
- **"Real-data scientific task" definition**: what the actual (non-synthetic) data source and scientific objective are — so I can clearly mark it `OPEN` and describe what remains to be done once real data replaces the fixture.
- **Size/shape constraints** for "minimal": number of rows/records, file size cap, whether edge cases (empty, malformed, boundary values) should be included.

If you can paste the relevant schema definition, a redacted sample of the real data, or a link to the stage's README, I'll produce both artifacts immediately — with the fixture explicitly tagged `SYNTHETIC` and the real-data task marked `OPEN` until real data is available.

——qlv SI1语义轨·20261121T034142Z
