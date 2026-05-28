# Maintainer Guide

This project publishes certification requirements as both a human-readable documentation site and an LLM-consumable text file (`llms-full.txt`).
These two outputs serve different audiences but are generated from the same source files.
Understanding how they relate is important when making changes.

## How the site and llms-full.txt are built

Both outputs are configured in `mkdocs.yml`:

- The `nav:` section controls what appears on the built documentation site and in what order.
- The `llmstxt` plugin `sections:` control what gets concatenated into `llms-full.txt`.

Requirement pages listed in `nav:` should also appear in the `llmstxt` plugin `sections:` so that the LLM-facing output stays in sync with the site.
However, the reverse is not true.
Some files exist only in `llms-full.txt` and intentionally do not appear on the site.

## The review summary table

`docs/review_summary.md` contains a summary table that an LLM uses as the output format when reviewing a collection.
It has one row per certification requirement section.
This file is included in `llms-full.txt` via the `llmstxt` plugin but is deliberately excluded from `nav:` because it is not intended for human readers.
It is instructions for LLM reviewers only.

## When you add or remove a requirement

If you add, remove, or rename a certification requirement section:

1. Create or update the markdown file in `docs/`.
2. Add or remove it from `nav:` in `mkdocs.yml` so the site reflects the change.
3. Add or remove it from the `llmstxt` plugin `sections:` so `llms-full.txt` reflects the change.
4. Update the table in `docs/review_summary.md` to add, remove, or rename the corresponding row.

Steps 2, 3, and 4 are all driven by changes in step 1.
The review summary table must stay aligned with the requirement sections because LLM-based reviewers use it to structure their findings.
A missing row means that requirement gets no explicit pass/fail in the review output.

## Why it works this way

The certification review skill that invokes LLM-based reviews is intentionally minimal.
It fetches `llms-full.txt` at the start of each session and relies entirely on that document for both the checklist of requirements and the output format.
This means the skill never needs to be updated when requirements change.
All changes are contained in this repository.
The tradeoff is that maintainers need to keep the review summary table in sync with the requirement sections.
