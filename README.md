# CSCE-676-Data-Mining-Project
Performing Text Mining on Jeopardy! questions dataset
# Jeopardy! Dataset Analysis & Generation

## Overview
This project analyzes ~200k historical *Jeopardy!* questions to study category trends, question difficulty, and content structure, and to support automatic generation of Jeopardy-style question boards.

## EDA Summary
Main exploratory steps:
- Inspected dataset structure and missing values.
- Cleaned prize values and converted them to numeric format.
- Removed rows with invalid values.
- Standardized category names to remove formatting inconsistencies.
- Analyzed question distribution across rounds.
- Studied category trends over time.
- Profiled categories using average question value as a difficulty proxy.

## Goals
- Discover thematic patterns in questions.
- Analyze topic evolution over time.
- Group semantically similar questions.
- Generate playable Jeopardy-style question sets automatically.

## Methods
- Text mining and embeddings (course methods)
- Topic modeling and transformer-based embeddings (beyond course)
- Automated question/board generation pipelines

## Outcome
The project demonstrates how large-scale text datasets can be cleaned, analyzed, and reused for semantic analysis and automated content generation.
