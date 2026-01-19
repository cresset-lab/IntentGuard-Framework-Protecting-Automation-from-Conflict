# IntentGuard-Framework-Protecting-Automation-from-Conflict
An Agentic AI Framework for Conflict-Aware Smart Home Automation via Natural Language

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)

This repository contains the experimental artifacts for the paper **"An Agentic AI Framework for Conflict-Aware Smart Home Automation via Natural Language"** accepted at SANER 2026 ERA Track.

## 📋 Overview

This proof-of-concept demonstrates an AI-powered framework that:
- Translates natural language requests into SmartThings-compatible JSON rules
- Performs semantic conflict detection across automation rules
- Provides explainable conflict resolution strategies

## 📂 Repository Structure
```
├── configs/              # Flowise and tool configurations
├── data/                 # SmartThings capabilities and example rules
└── evaluation/           # Test cases used in evaluation
```

## 🗂️ Contents

### Configurations (`configs/`)
- **Flowise_chatflow.json**: Complete Flowise workflow configuration with Tool Agent, retriever tools, and memory
- **save_generated_rule-CustomTool.json**: Custom JavaScript tool for rule persistence (requires local Flowise)
- **pinecone_config.txt**: Pinecone vector database configuration details

### Data (`data/`)
- **smartthings_data.txt**: 134 SmartThings device capabilities extracted from official documentation, split into 306 text chunks
- **test_rules.json**: Example generated automation rules with metadata (rule IDs, timestamps)

### Evaluation (`evaluation/`)
- **test_cases.pdf**: Nine test cases covering three conflict categories:
  - Direct Contradictions (3 cases)
  - Temporal Illogicality (3 cases)
  - Condition Overlaps (3 cases)

## 🛠️ Setup Requirements

### Prerequisites
- **Flowise** 
- **Google API Key** for:
  - Gemini-2.0-Flash (LLM)
  - text-embedding-004 (embeddings)
- **Pinecone Account**
- **Pinecone API KEY**

### Pinecone Configuration

**No manual Pinecone setup required** Flowise automatically manages everything:

1. **Get a Pinecone API Key**
   - Sign up at [Pinecone](https://www.pinecone.io/)
   - Generate an API key (free tier)
   - Add it to Flowise credentials

2. **Flowise Auto-Creates**:
   - Index: `flowise` (768 dimensions, cosine metric, AWS us-east-1)
   - Namespace 1: `smartthings-capabilities` (306 chunks)
   - Namespace 2: `generated-rules` (134 chunks)

3. **Upload via Flowise Document Stores**:
   - SmartThings store → upload `smartthings_data.txt` → 306 chunks
   - GeneratedRules store → upload `test_rules.json` → 39 chunks

See `configs/pinecone_config.txt` for detailed configuration.

**Current State**: 440 total vectors across 2 namespaces in the "flowise" index.

## 🚀 Quick Start

1. **Import Flowise Workflow**
   - Open your Flowise instance
   - Import `configs/Flowise_chatflow.json`

2. **Configure API Keys**
   - Add your Google API key in Flowise UI
   - Add your Pinecone API key in Flowise UI

3. **Create Document Store to Flowise**
   - Create `smartthings-capabilities` document store
   - Crate `generated-rules` document store

4. **Run the Workflow**
   - Use natural language inputs from `evaluation/test_cases.pdf`

For detailed setup instructions, see `SETUP_NOTES.txt`.


## 📊 Evaluation Results

The system achieved:
- **88.9% conflict detection accuracy** (8/9 test cases)
- **100% JSON schema compliance** for generated rules
- **100% accuracy** for Direct Contradictions and Condition Overlaps
- **66.7% accuracy** for Temporal Illogicality

See paper Section IV for detailed results.

## 🔒 Security Note

All API keys have been removed from the configurations. Researchers must substitute their own credentials following the setup instructions.


## 📧 Contact

For questions about this research, please contact:
- Sayyada Aisha Mehvish - amehvish@torontomu.ca
- Manar H. Alalfi - manar.alalfi@torontomu.ca

## 📜 License

This project is licensed under the MIT License - see the LICENSE file for details.
