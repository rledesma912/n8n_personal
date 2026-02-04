# Project Overview

This project serves as a self-contained environment for a creative writing project that leverages AI for narrative generation. It uses Docker to deploy and manage two key services:

*   **n8n:** An open-source workflow automation tool. In this project, n8n is used to orchestrate a sophisticated literary creation process, as detailed in `proceso_literario.md`. The workflows likely involve interacting with Large Language Models (LLMs) to generate and refine story content.

*   **ChromaDB:** A vector database used for storing and retrieving embeddings. This is a core component of the RAG (Retrieval-Augmented Generation) workflow, allowing the AI to access and build upon existing story fragments.

The project is designed for a Spanish-speaking user, with all documentation and prompts written in Spanish.

## Key Files

*   `docker-compose.yml`: Defines the `n8n` and `chromadb` services, their configurations, and data volumes.
*   `proceso_literario.md`: A crucial document outlining the iterative creative process. It defines steps for linguistic correction, narrative review, consistency checks, and pacing. It also contains a Mermaid diagram illustrating the n8n RAG workflow.
*   `prompts/`: This directory contains detailed instructions for the AI model, defining the persona, style, structure, and constraints for generating horror stories.
    *   `context_tunning.md`: A prompt for generating a horror story with very specific constraints on length and structure.
    *   `story_create.txt`: A similar, but slightly different, prompt for generating a horror story.
*   `.env.example`: A template for the environment variables required to run the services, including credentials for n8n.
*   `README.md`: Provides instructions on how to set up and run the Docker environment.

## Building and Running

1.  **Set up environment variables:**
    ```bash
    cp .env.example .env
    ```
    Edit the `.env` file to set your `N8N_BASIC_AUTH_USER` and `N8N_BASIC_AUTH_PASSWORD`.

2.  **Start the services:**
    ```bash
    docker-compose up -d
    ```

3.  **Access n8n:**
    Open your browser and navigate to `http://localhost:5678`.

4.  **Access ChromaDB:**
    The ChromaDB API is available at `http://localhost:8000`.

## Development Conventions

*   **Creative Focus:** The primary goal of this project is creative writing, specifically horror stories. The n8n workflows and AI prompts are tailored for this purpose.
*   **RAG-based Workflow:** The project uses a Retrieval-Augmented Generation (RAG) architecture. New story fragments are generated based on the existing context stored in ChromaDB.
*   **Iterative Process:** The `proceso_literario.md` emphasizes an iterative approach to writing, with distinct phases for correction, review, and refinement.
*   **Spanish Language:** All prompts, documentation, and generated content are in Spanish.
