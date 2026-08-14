# DiMba

**DiMba (Distilled Mamba)** is a query-aware, sentence-level context-compression framework for resource-constrained language models.

> **Status:** Active research and development. The implementation, configurations, and model checkpoints will be released progressively.

## Overview

DiMba learns continuous sentence-importance scores from teacher-generated supervision. It preserves complete sentences and models document-level relationships using a bidirectional Mamba architecture.

The intended pipeline is:

1. Segment the input context into sentences.
2. encode the query and sentences using a text encoder;
3. model sentence relationships using bidirectional Mamba;
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
