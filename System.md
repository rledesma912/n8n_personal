# Contexto del Sistema: Automatización Narrativa con n8n

Este documento proporciona una visión consolidada del entorno técnico y operativo para asistir en la creación de flujos de trabajo en n8n, integrando capacidades de IA local y bases de datos vectoriales.

## 1. Perfil del Host (Infraestructura Local)
*   **Sistema Operativo:** Ubuntu 24.04.4 LTS (Noble Numbat), kernel 6.17.0.
*   **Hardware Crítico:**
    *   **CPU:** AMD Ryzen 5 5600G (12 hilos, 6 núcleos).
    *   **RAM:** 64GB DDR4 (Suficiente para múltiples instancias de LLM).
    *   **GPU:** NVIDIA GeForce RTX 3060 (12GB VRAM), CUDA 13.0, Driver 580.126.09.
*   **Almacenamiento:** Disco dedicado `/mnt/LLM` para modelos y aplicaciones de IA.
*   **Servicios de IA Disponibles:**
    *   **Ollama:** v0.15.2 (Modelos: `mistral:latest`, `llama3.1:8b`).
    *   **ComfyUI:** Instalado y funcional para generación de imágenes.

## 2. Arquitectura del Proyecto (Docker Compose)
El ecosistema n8n está orquestado mediante contenedores para garantizar persistencia y escalabilidad:

*   **n8n (Versión: Open Source / Self-hosted):** 
    *   **Nota Crítica:** Se utiliza la edición de comunidad/open-source. La IA cloud **NO** debe sugerir funcionalidades exclusivas de las versiones *Enterprise* o *Cloud* (ej. variables de entorno en la UI, gestión avanzada de usuarios, nodos de IA nativos premium, o ejecuciones en cola avanzadas).
    *   Accesible en `http://localhost:5678`.
    *   Configurado con **PostgreSQL** como base de datos persistente.
    *   Capacidad para interactuar con el host mediante `host.docker.internal`.
*   **PostgreSQL (v.15-alpine):** 
    *   Gestiona los metadatos de los flujos de n8n.
    *   Puerto: `5432`.
*   **ChromaDB (v.latest):** 
    *   Base de datos vectorial para RAG (Retrieval-Augmented Generation).
    *   Accesible en `http://localhost:8000`.
    *   API habilitada para reseteo y persistencia de colecciones.

## 3. Proceso Literario y Flujo
El proyecto se centra en la creación colaborativa de historias de terror siguiendo un flujo estructurado:

### A) Flujo de Trabajo (Estructura n8n)
1.  **Entrada:** Manual o automatizada.
2.  **Embeddings:** Generados localmente con Ollama (`nomic-embed-text`).
3.  **Búsqueda:** Consulta semántica a la colección `story` en ChromaDB.
4.  **Generación:** Prompt contextual enviado a Ollama (`mistral:latest`).
5.  **Cierre:** El resultado se almacena capítulos en PostgreSQL para mantener la memoria a largo plazo del relato.
POr ahora seguimos mejorando el Flujo A.

### B) Etapas de Calidad Literaria:
Al diseñar flujos, se deben incluir nodos de verificación para:
*   **Corrección Lingüística:** Ortografía, gramática y puntuación.
*   **Revisión Narrativa:** Eliminar clichés de terror y lugares comunes.
*   **Consistencia Interna:** Control de personajes, tiempos narrativos y POV.
*   **Ritmo (TTS):** Párrafos optimizados para síntesis de voz (pausas dramáticas, longitud de frases).

## 4. Guía para el LLM Cloud (Instrucciones de Ayuda)
Cuando asistas en la creación de flujos de n8n para este sistema:
*   **Networking:** Usa siempre `http://host.docker.internal:[puerto]` para acceder a Ollama (puerto 11434) o ChromaDB (puerto 8000) desde n8n.
*   **Rutas de Archivos:** Los archivos locales de n8n están en `/home/node/.n8n` dentro del contenedor.
*   **Variables:** Prioriza el uso de variables de entorno `${N8N_BASIC_AUTH_USER}`, etc.
*   **Idioma:** Todas las interacciones, prompts y flujos deben mantenerse en **Español**.
