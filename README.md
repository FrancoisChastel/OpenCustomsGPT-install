# OpenCustomsGPT Installation Guide

This repository contains the necessary configuration to deploy OpenCustomsGPT using Docker Compose.

## Prerequisites

- Docker and Docker Compose installed
- Access to the OpenCustomsGPT Docker repository (required)
- Git installed
- PostgreSQL database with:
  - Schema `sydonia_mg` containing tables `sad_item` and `sad_gen`
  - A read-only user account for safety (recommended as the system will execute LLM-generated SQL queries)

## Installation Steps

1. Clone this repository:

```bash
git clone https://github.com/FrancoisChastel/OpenCustomsGPT-install.git
cd OpenCustomsGPT-install
```

2. Request access to the Docker repository by:

- Contacting the repository administrators
- Providing your Docker Hub username
- Waiting for approval

3. Configure your environment:
  
```bash
cp .env.sample .env
```

4. Edit the `.env` file with your credentials and configuration:

```env
DB_URI=postgresql+psycopg2://readonly_user:password@host.docker.internal:5432/imf_sydonia
OPENAI_API_KEY=YOUR_OPENAI_API_KEY
BASE_URL_LITELLM=http://litellm:4000/v1/
```

Note: Replace `readonly_user:password` with your read-only PostgreSQL user credentials. Using a read-only user is crucial for security when running LLM-generated SQL queries.

5. If using Azure OpenAI Service (or any other providers), edit the `litellm-config.yaml` file:
   - Follow the configuration guide at <https://docs.litellm.ai/docs/providers/azure>
   - Adjust the model deployments and endpoints according to your Azure setup

6. Start the services:

```bash
docker compose up -d
```

## Troubleshooting

If you encounter `unauthorized` errors, ensure you have:

- Been granted access to the Docker repository
- Successfully logged in to Docker

## Support

For access requests or issues, please open a GitHub issue or contact the repository administrators.
