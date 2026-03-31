# benchmark-grinder

A reusable Codex skill for autonomous benchmark optimization.

`benchmark-grinder` turns repeated score-chasing into a disciplined engineering loop:

- establish a baseline
- verify datasets, checkpoints, and benchmark assets
- restrict edits to an approved scope
- run one hypothesis at a time
- log every run to a machine-readable ledger
- keep docs in sync
- continue iterating until explicitly stopped

This is designed for benchmark-driven work across CS domains, including:

- LLM training and evaluation
- computer vision
- retrieval and ranking
- systems and inference optimization
- other measurable research or engineering loops

Typical use cases:

- improve LLM answer quality against an eval set or judge model score
- improve CV metrics such as accuracy, mAP, IoU, or FID
- improve retrieval quality such as recall, nDCG, or MRR
- improve systems or kernel performance such as latency, throughput, memory, or utilization
- iterate on low-level operator kernels in an environment such as NVIDIA-style performance work

## Repo layout

```text
skills/
  benchmark-grinder/
    SKILL.md
templates/
  benchmark.md
  results.tsv
```

## What the skill does

The skill provides a general operating protocol for autonomous benchmark work:

1. define the metric and optimization direction
2. verify the setup and benchmark assets
3. run the untouched baseline first
4. iterate on one experimental idea at a time
5. log outcomes and keep only justified improvements
6. update project docs while the loop runs
7. do not stop after each run unless blocked or interrupted

## How to use it

### Quick start (auto-discovery)

1. Install the skill (see Install section below)
2. Start Claude Code or Codex in your benchmark project
3. Say: "Use benchmark-grinder to optimize [your metric]"

The skill will automatically:
- Find evaluation scripts and benchmark commands
- Identify editable vs frozen files
- Infer the target metric
- Create a `benchmark.md` contract for your review
- Start the optimization loop

### Manual setup (optional)

For more control, create a `benchmark.md` contract yourself:

- the benchmark name
- the primary metric
- the canonical run command
- the editable files
- the forbidden changes
- asset download/setup steps
- timeout rules
- result logging format

Use the templates in `templates/benchmark.md` and `templates/results.tsv` as starting points.

## Install

### One-line install

```bash
git clone https://github.com/zedong-peng/benchmark-grinder.git ~/.claude/skills/benchmark-grinder
```

That's it. The skill is now available in Claude Code.

### Usage

In your benchmark project:

```bash
claude-code
```

Then say:
```text
Use benchmark-grinder to optimize [your metric]
```

The skill will auto-discover your project structure and start optimizing.

### Alternative: Manual contract (optional)

If you want explicit control, copy the template first:

```bash
cp ~/.claude/skills/benchmark-grinder/templates/benchmark.md .
```

Edit it with your project specifics, then start Claude Code.

## Recommended project files

For each benchmark repo using this skill, keep these files near the code:

- `benchmark.md`: benchmark contract and operating rules
- `results.tsv`: machine-readable run history
- `notes.md` or `progress.md`: short qualitative takeaways
- per-run logs: crash details, metrics, resource usage

## Example scenarios

### LLM answer scoring

A target repo might define:

- benchmark command that runs eval on a held-out set
- metric such as win rate, accuracy, judge score, or reward-model score
- editable scope such as prompts, inference parameters, data formatting, retrieval, model code, or training loop
- frozen scope such as eval questions, labels, and scoring harness

Then you run Claude Code in that repo and say:

```text
Use benchmark-grinder. Optimize answer score on this eval without changing the evaluator or gold data. Log each run to results.tsv and continue until I stop you.
```

### Kernel or systems optimization

A target repo might define:

- benchmark command that runs correctness checks and performance measurement
- primary metric such as throughput or latency
- secondary metrics such as memory footprint, occupancy, or compile time
- editable scope such as kernel code, launch config, tiling strategy, or scheduling
- frozen scope such as correctness tests and benchmark harness

Then you run the agent with a prompt like:

```text
Use benchmark-grinder. Optimize this kernel benchmark for throughput while preserving correctness. Keep a baseline, log every run, and continue autonomously until interrupted.
```

## Positioning

This repo is not a benchmark implementation.

It is a reusable operational skill for running autonomous benchmark-improvement loops safely and consistently.
