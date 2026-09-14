# BIDIMBA

**BIDIMBA** is a query-aware, extractive **context compression** framework for large language models. It uses supervision from a LLM and a bidirectional Mamba architecture to identify the context units which are the most relevant to a query and retains them within a token budget. The project is under active development, with code, experiment configurations, and model checkpoints planned for progressive release; the estimated release is **October 2026**.

## Overview

BIDIMBA preserves complete context units and handles the long sequence of context, using a bidirectional Mamba architecture.

The intended pipeline is:

1. Segment the input context into context units.
2. encode the query and units using a text encoder (Shared MordernBert);
3. Estimating scores using bidirectional Mamba;
4. predict continuous sentence-importance scores;
5. select the highest-utility sentences under a token budget; and
6. provide the compressed context to a downstream language model.

## Dataset

The teacher-labeled data is maintained independently in the
[DiMba-Dataset](https://github.com/TurgudValiyev2002/DiMba-Dataset) repository.

The dataset is derived from FinQA, ConvFinQA, and TAT-QA and contains sentence-level importance supervision for query-aware financial context compression.

## Repository Structure

```text
configs/             Experiment configurations
docs/                Technical documentation
examples/            Usage examples
notebooks/           Exploratory analysis
scripts/             Training and evaluation entry points
src/dimba/           Core Python package
tests/               Automated tests
``` 

## Reproducibility

Installation, data preparation, training, inference, and evaluation instructions will be added as the implementation is finalized.

## Authors

Turgud Valiyev, Kolichala Rajashekar, Radu Prodan, and Dumitru Roman.
