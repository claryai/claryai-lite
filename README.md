# Clary AI Lite

Clary AI Lite is the entry-level tier of the Clary AI document processing platform, providing basic document processing capabilities without pre-integrated LLM models.

## Overview

Clary AI Lite offers essential document processing functionality, allowing users to extract and analyze text from various document formats. This tier is designed for users who want to use their own LLM models or who have simpler document processing needs.

## Features

- Basic document processing
- Text extraction from multiple document formats
- Document structure recognition
- Simple API for integration
- Self-hosted deployment via Docker
- Extensible architecture

## Tier Comparison

| Feature | Lite | Standard | Professional |
|---------|------|----------|--------------|
| Document Processing | ✅ | ✅ | ✅ |
| Text Extraction | ✅ | ✅ | ✅ |
| Structure Recognition | ✅ | ✅ | ✅ |
| Pre-integrated LLM | ❌ | ✅ (Phi-4) | ✅ (Cloud) |
| Advanced Analytics | ❌ | ✅ | ✅ |
| Cloud LLM Support | ❌ | ❌ | ✅ |
| Enterprise Features | ❌ | ❌ | ✅ |

## Repository Structure

```
claryai-lite/
├── core/                 # Core submodule
├── src/                  # Lite-specific source code
│   ├── api/              # API components
│   ├── models/           # Lite-specific models
│   ├── utils/            # Utility functions
│   └── config/           # Configuration management
├── tests/                # Test suite
│   ├── unit/             # Unit tests
│   └── integration/      # Integration tests
├── docs/                 # Documentation
└── scripts/              # Utility scripts
```

## Installation

### Prerequisites

- Docker and Docker Compose
- Git

### Setup

1. Clone the repository with submodules:
   ```bash
   git clone --recursive https://github.com/claryai/claryai-lite.git
   cd claryai-lite
   ```

2. Build and run with Docker Compose:
   ```bash
   docker-compose up --build
   ```

3. Access the API at `http://localhost:8000`

## Development

1. Set up a virtual environment:
   ```bash
   python -m venv venv
   source venv/bin/activate  # On Windows: venv\Scripts\activate
   ```

2. Install dependencies:
   ```bash
   pip install -r requirements.txt
   ```

3. Run tests:
   ```bash
   pytest
   ```

## Upgrading to Higher Tiers

To upgrade to a higher tier:

1. Standard Tier: [Clary AI Standard](https://github.com/claryai/claryai-standard)
2. Professional Tier: [Clary AI Professional](https://github.com/claryai/claryai-professional)

## License

This repository is licensed under the terms specified in the LICENSE file.

## Contact

For questions or support, please contact the Clary AI team.
