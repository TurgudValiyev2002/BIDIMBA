# BIDIMBA

**BIDIMBA** is a query-aware, extractive **context compression** framework for large language models (LLMs). Given a user query and its associated context, it selects relevant context units within a token budget **before the downstream LLM performs inference**. BIDIMBA inputs are a user query, the associated context, and a retention ratio. Its output is a composed context based on retention ratio. The framework uses LLM-generated supervision, a domain-adapted shared ModernBERT encoder, and a bidirectional Mamba scorer to estimate the importance of each unit. A protected hybrid selector retains complete units by considering both importance scores and token lengths. Finally, it restores their original order to form the compressed context. The project is under active development, with code, experiment configurations, and model checkpoints planned for progressive release; the estimated release is **October 2026**.


The intended pipeline is:

1. **Context decomposition.** Divide the context into meaningful units, such as sentences, bullet points, titles, subtitles, and table rows. Preserve each unit's original position so that the source order can be recovered after selection.
2. **Shared encoding.** Encode the query and context units with the same ModernBERT encoder to obtain their semantic representations.
3. **Feature construction.** Combine unit metadata with query-unit semantic interaction features, including element-wise products, absolute differences, and dot-product similarity between the query and unit embeddings.
4. **Feature projection.** Project each unit's combined feature vector through 512- and 256-dimensional representations. This reduces the feature dimension while preserving the sequence of context units.
5. **Bidirectional importance scoring.** Process the unit sequence in forward and backward directions using a bidirectional Mamba architecture. Fuse both directional representations and apply a scoring MLP to predict a continuous, importance score for each context unit.
6. **Protected hybrid selection.** Use the predicted importance scores and unit token lengths to select complete units within the token budget. Combine a protected allocation with an exact 0/1 knapsack selection over the remaining candidates and available budget.
7. **Original-order recovery and inference.** Restore the retained units to their original order, assemble the compressed context, and pass it with the user query to the downstream LLM for answer generation.

LLM-generated importance supervision is used to train the compressor; the pipeline above describes how the trained compressor prepares context for downstream inference.

## Dataset

The teacher-labeled data is maintained independently in the
[BIDIMBA-dataset](https://github.com/TurgudValiyev2002/BIDIMBA-dataset) repository.

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
