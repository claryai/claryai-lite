# Clary AI Lite

Clary AI Lite is a lightweight document processing platform with agentic capabilities, built on open source AI models.

## Overview

Clary AI Lite provides basic document processing capabilities without pre-integrated LLM models, allowing users to configure their own model connections if needed. It is designed to be self-hosted via Docker containers and offers a commercial API service that clients can connect to.

## Features

- **Basic Document Extraction**: Extract structured data from documents
- **API Access**: REST API for document processing
- **Self-Hosted Deployment**: Deploy on your own infrastructure
- **Privacy-Focused**: Keep your data on-premises
- **Bring Your Own LLM**: Configure your own LLM connections

## Hardware Requirements

- **CPU**: 2+ cores
- **RAM**: 4GB minimum, 8GB recommended
- **Storage**: 5GB for installation, plus storage for documents
- **GPU**: Not required

## Getting Started

### Prerequisites

- Docker and Docker Compose
- 4GB+ RAM
- 5GB+ free disk space

### Installation

1. Clone the repository:
   ```bash
   git clone https://github.com/your-org/claryai-lite.git
   cd claryai-lite
   ```

2. Initialize and update the submodule:
   ```bash
   git submodule init
   git submodule update
   ```

3. Create a `.env` file:
   ```bash
   cp core/.env.example .env
   ```

4. Start the services:
   ```bash
   docker-compose up -d
   ```

5. Access the application:
   - Web UI: http://localhost:3000
   - API: http://localhost:8000

## Documentation

For detailed documentation, see the [docs](core/docs/) directory, particularly:

- [Architecture Overview](core/docs/architecture.md)
- [API Documentation](core/docs/api.md)
- [Deployment Guide](core/docs/deployment.md)

## Upgrading to Higher Tiers

Clary AI Lite can be upgraded to higher tiers (Standard or Professional) to access additional features:

- **Clary AI Standard**: Adds advanced document extraction, table extraction, and pre-integrated Phi-4 Multimodal model
- **Clary AI Professional**: Adds custom templates, Llama 3 8B model, and cloud LLM support

See the [Upgrade Path](core/docs/upgrade_path.md) documentation for details on upgrading.

## License

This project is licensed under the [MIT License](LICENSE).
