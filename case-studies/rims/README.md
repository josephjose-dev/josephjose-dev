# RIMS — Multimodal AI & Workflow Orchestration

**Project:** Road Incident Management System  
**Author:** Joseph S Jose · BITS Pilani, Dubai Campus  
**Status:** Prototype  
**Repository:** :PRIVATE


## Overview

RIMS is a full-stack prototype that turns text, images, and selected video frames into structured records and proposed response plans. Road incident management is its application context; the engineering centres on multimodal processing, agent orchestration, retrieval, backend validation, and real-time interfaces.

The system connects specialised AI stages through an asynchronous FastAPI backend, stores results locally, and publishes updates to a dashboard over WebSockets.

## Engineering Capabilities

| Capability | Implementation |
| :--- | :--- |
| Structured extraction | Uses LLaMA 3.3 through Groq to extract fields from free-form text. |
| Multimodal processing | Combines text analysis with Gemini vision analysis of photos and selected video frames. |
| Agent orchestration | Separates extraction, media screening, visual analysis, report generation, and response planning into five specialised stages. |
| Cross-modal reconciliation | Compares text and visual findings, applies confidence thresholds, and records detected contradictions. |
| Iterative planning | Uses a planner–critic–reviser loop, with a revision call only when the critic requests changes. |
| Similarity retrieval | Generates local sentence-transformer embeddings and searches past records with sqlite-vec. |
| Async APIs and live updates | Uses FastAPI for request handling and native WebSockets for dashboard updates. |
| Geospatial interfaces | Resolves location strings, supports map-pin selection, and compares coordinates for nearby-facility matching. |
| Input and output handling | Includes upload type and size checks, parameterized SQL, HTML escaping, and temporary-file cleanup. |

## Processing Flow

1. Accept text and optional photo or video input through the backend.
2. Extract structured fields from the text and screen submitted media.
3. Use OpenCV to select video keyframes where applicable, then analyse visual evidence with Gemini.
4. Reconcile text and visual findings using programmatic rules and confidence thresholds.
5. Generate a structured report and apply explicit priority rules.
6. Draft a response plan, critique it, and revise it when needed.
7. Store the result in SQLite and broadcast it to the dashboard.

Similarity retrieval supports comparison with past cases. The prototype also includes location-based facility matching and domain-specific rules.

## Technology Stack

| Layer | Technology |
| :--- | :--- |
| Backend | Async Python, FastAPI |
| Text models | LLaMA 3.3 70B through Groq |
| Multimodal models | Gemini 2.5 Flash through the Google API |
| Vision and video preparation | OpenCV, motion and optical-flow analysis, keyframe extraction |
| Embeddings | sentence-transformers, all-MiniLM-L6-v2, 384-dimensional vectors |
| Storage and retrieval | SQLite in WAL mode, sqlite-vec |
| Frontend | HTML5, Tailwind CSS, ES6 JavaScript |
| Live communication | FastAPI WebSockets |
| Maps and geocoding | Leaflet.js, OpenStreetMap/Nominatim |

## Engineering Decisions

### Specialised stages with explicit coordination

Separate model calls handle text extraction, vision, report generation, and planning. Programmatic coordination reconciles outputs and applies rules between stages. This keeps responsibilities inspectable and lets different tasks use different model providers.

### Selected frames for video analysis

OpenCV prepares targeted frames before multimodal inference. This reduces the input sent to the model and avoids depending on raw video uploads. The tradeoff is partial coverage: selected frames can miss events elsewhere in the clip.

### Conditional revision

The planner produces a draft and the critic reviews it. A reviser runs only when a change is requested, reducing unnecessary model calls. Agreement between these stages is a workflow check, not proof that an output is correct.

### Local embeddings and storage

Embeddings are generated locally and queried within SQLite using sqlite-vec. This keeps the prototype's storage and retrieval components on one machine. WAL mode allows readers and a writer to overlap, while SQLite still permits only one writer at a time.

### Programmatic checks around model output

The application applies explicit priority rules, validates uploads, escapes rendered content, and separates submitted text from model instructions. These measures reduce specific failure modes; they do not guarantee media authenticity, immunity to prompt injection, or correct model reasoning.

### Location-aware presentation

Leaflet and geocoding connect extracted locations to an interactive map. Haversine distance supports nearest-facility matching from a static coordinate catalog. It measures geographic proximity rather than travel time, capacity, or suitability.

## Prototype Scope

The system produces proposed plans and reports. It does not establish integration with a live emergency dispatch service.

The current design uses SQLite and local files on a single machine. Distributed workers, object storage, and a production database are possible future upgrades, rather than components implemented in this prototype. Congestion and violation calculations use configured data and rules. Media screening and visual reasoning remain heuristic and model-based assessments.

## Transferable Experience

This project demonstrates combining AI services with conventional backend engineering: structured data extraction, multimodal inputs, explicit orchestration, vector retrieval, validation, persistence, and event-driven interfaces. Those patterns apply to document processing, operational dashboards, review workflows, and other applications beyond road incidents.

