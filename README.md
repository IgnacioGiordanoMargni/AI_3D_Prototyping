AI-Driven 3D Asset Prototyping
Text-to-3D Generation using Shap-E and Retrieval-Augmented Generation (RAG)
Overview

This repository presents a technical proof of concept for accelerating early-stage 3D asset prototyping through the integration of generative AI and Retrieval-Augmented Generation (RAG).

The system transforms natural language descriptions into approximate 3D models by enhancing user prompts with contextual knowledge before generating geometry using Shap-E.
The resulting assets are intended for rapid testing, validation and experimentation, not for final production use.

Problem Context

In early phases of game development and real-time 3D applications, teams often require:

Placeholder or proxy assets

Fast visual validation of scale and proportions

Rapid iteration without blocking development on manual modeling

Traditional asset pipelines are costly at this stage. This project explores how AI-assisted generation can reduce iteration time by enabling on-demand 3D asset creation directly from text input.

Solution Description

The solution introduces a RAG-based prompt refinement layer in front of a text-to-3D generative model.

Instead of directly passing raw user prompts to Shap-E, the system:

Retrieves relevant contextual information from a curated 3D-related knowledge base

Refines and expands the original query

Produces a more structured and semantically rich prompt for 3D generation

This approach improves consistency, relevance and usability of the generated assets during prototyping.

Technical Architecture

The pipeline is composed of the following stages:

1. Document Ingestion

Text documents related to 3D objects and concepts are loaded from a local directory

Documents are split into overlapping chunks to preserve semantic continuity

2. Vectorization and Retrieval

Text chunks are embedded using sentence-transformer embeddings

Embeddings are stored in a ChromaDB vector database

A retriever fetches the most relevant context for a given query

3. RAG Prompt Generation

A local LLM (via Ollama) combines the retrieved context with the user query

The output is an enriched prompt tailored for 3D generation

4. 3D Asset Generation

The refined prompt is passed to Shap-E

Latent sampling and diffusion are executed on GPU when available

The generated mesh is decoded and exported as a standard 3D file

User Query
   ↓
Vector Retrieval (ChromaDB)
   ↓
RAG Prompt Refinement (LLM)
   ↓
Shap-E Text-to-3D Generation
   ↓
OBJ Mesh Export

Technologies Used

Python

Shap-E – text-to-3D generative model

LangChain – RAG pipeline orchestration

ChromaDB – vector database for semantic retrieval

Sentence-Transformers – text embeddings

Ollama (local LLM inference)

Trimesh – mesh conversion and export

PyTorch – model execution (CPU / GPU)

Output

Generated 3D meshes exported in OBJ format

Assets are compatible with standard DCC tools and game engines

Geometry is intended for visual testing and prototyping

Use Cases

Rapid asset prototyping in game development

Gameplay and mechanics validation with placeholder models

Technical experimentation with generative 3D pipelines

Early art direction and scale validation

Research and exploration of AI-assisted 3D workflows

Limitations

Generated meshes are approximate and non-production ready

Topology and UVs may require manual cleanup

No automatic rigging or animation support

The system is optimized for speed and experimentation, not final assets

Professional Relevance

This project demonstrates:

Practical application of RAG beyond text-only use cases

Integration of generative AI into 3D asset pipelines

Experience with vector databases and local LLM inference

Focus on real production constraints in interactive applications


## 🔬 Comparative Results

The following table compares the output of Shap-E (baseline) and Shap-E with RAG-enhanced prompts using identical input queries.



| Prompt | Shap-E (Baseline) | Shap-E + RAG |
|------|------------------|--------------|
| *"un cubo biselado (a beveled cube)"* | ![](Assets/shap-egifs/cubo_biselado.gif) | ![](Assets/rag_gifs/cubo_biselado_RAG.gif) |
| *"una caja de pc (a pc box)"* | ![](Assets/shap-egifs/caja_pc.gif) | ![](Assets/rag_gifs/caja_pc_RAG.gif) |
| *"una caja eléctrica (an electric box)"* | ![](Assets/shap-egifs/caja_electrica.gif) | ![](Assets/rag_gifs/electric_box_rag.gif) |
| *"un servidor rack 1u (a 1u server rack)"* | ![](Assets/shap-egifs/servidor_rack.gif) | ![](Assets/rag_gifs/servidor_rack.gif) |
| *"una mesa (a table)"* | ![](Assets/shap-egifs/mesa.gif) | ![](Assets/rag_gifs/mesa_rag.gif) |
| *"un switch de ocho puertos (an eight-port switch)"* | ![](Assets/shap-egifs/switch.gif) | ![](Assets/rag_gifs/switch_rag.gif) |
| *"un router de red (a network router)"* | ![](Assets/shap-egifs/router.gif) | ![](Assets/rag_gifs/router_red_rag.gif) |



All comparisons were rendered using identical camera, lighting and animation settings to ensure consistency.

License

This repository is intended for educational, experimental and portfolio purposes.
