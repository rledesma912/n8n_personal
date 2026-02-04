# Pasos iterativos de trabajo con IA:

## A) Corrección lingüística (obligatorio)

### Verificar y corregir:
- Ortografía
- Gramática
- Puntuación
- Concordancia verbal
> No cambiar estilo ni vocabulario, salvo error.


bla bla bla

## B) Revisión narrativa (anti-cliché)
- Detectar clichés típicos de terror
- Señalar frases gastadas
- Marcar lugares comunes
- Sugerir reemplazos sin reescribir la historia
> No cambia, solo marca y propone.

## C) Consistencia interna
- Personajes que cambian de nombre
- Tiempos incoherentes (día/noche)
- Acciones imposibles
- Objetos que aparecen sin introducción
- Cambios bruscos de POV
> Identifica y señala.

## D) Ritmo narrativo (muy importante para TTS)
- Detectar párrafos demasiado largos
- Sugerir cortes para respiración
- Marcar dónde conviene una pausa dramática

# Diagrama de trabajo con el LLM
::: mermaid
flowchart LR
    subgraph "Workflow 1: Construcción Colaborativa con RAG"
        A[Trigger Manual<br>Tu nueva orden] --> B[1. Embedding de la Consulta<br>Nodo Embeddings Ollama<br>Model: nomic-embed-text];
        B --> C[2. Búsqueda Semántica<br>Nodo HTTP Request<br>POST /api/v1/collections/story/chromadb:8000];
        C --> D[3. Construir Prompt Contextual<br>Nodo Code/Function];
        D --> E[4. Generar Continuación<br>Nodo HTTP Request a Ollama<br>Model: mistral:latest];
        E --> F[5. Almacenar Nuevo Fragmento<br>Nodo HTTP Request a ChromaDB];
        F --> G[6. Mostrar Resultado<br>y Esperar Siguiente Orden];
    end

    G --> A
:::