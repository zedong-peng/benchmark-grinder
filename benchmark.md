# LoCoMo Benchmark Contract

## Benchmark
LoCoMo (Long Context Memory Optimization)

## Target Metric
- Primary: Accuracy (higher is better)
- Secondary: F1 score, precision, recall

## Run Command
```bash
benchmark-grinder run experiments/grinder_config.json
```

## Setup
```bash
pip install benchmark-grinder
export OPENAI_API_KEY="your-key"
```

## Editable Scope
- `experiments/grinder_config.json` - all configuration parameters
- Memory source settings (conversation, dataset, hybrid)
- Model selection (gpt-4o-mini, gpt-4o, claude-3-5-sonnet-20241022)
- Retrieval settings (top_k, use_embeddings)
- Worker counts (sample_workers, question_workers)
- Timeout values

## Frozen Scope
- Evaluation code (benchmark-grinder package)
- Test datasets
- Scoring logic

## Timeout
- Per-run: 30 minutes
- Hard timeout: 60 minutes

## Result Logging
Append to `experiments/results/grinder_results.jsonl`:
```json
{
  "commit": "abc123",
  "timestamp": "2026-03-31T14:45:00Z",
  "config": {...},
  "metrics": {"accuracy": 0.85, "f1": 0.82},
  "status": "keep|discard|crash|timeout",
  "description": "Brief change description"
}
```

## Baseline Rule
Run current config first to establish baseline.
