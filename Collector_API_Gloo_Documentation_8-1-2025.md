
# Collector API – Gloo Studio Architecture Documentation

## Overview
The Collector API project has shifted from a manually managed FastAPI + Minikube stack to a fully integrated solution powered by **Gloo Studio**. With access to Gloo Studio’s Gateway, Data Engine, API Designer, and AI tools, the architecture now uses Gloo-native components for data ingestion, routing, and future AI analysis.

This document outlines the current state, design decisions, and roadmap for the project.

## Project State
- ✅ Minikube is running as the base Kubernetes environment.
- ✅ Gloo Gateway is deployed and serving traffic via the `gateway-proxy` service.
- ✅ Gloo Studio access is fully enabled (API Keys, Data Engine, API Designer, AI).
- ✅ Initial FastAPI container remains as a proof-of-concept but will transition to Gloo-native routes.
- ✅ We have a clear vision for how Gloo Studio pipelines will replace manual ETL.

## Current Architecture
1. **Gloo Gateway**
   - Provides entry point to all APIs in the system.
   - Handles routing to pipelines and services.

2. **Gloo Data Engine**
   - Will manage data ingestion from public APIs (e.g., Twitter, Reddit, JSONPlaceholder).
   - Supports pipelines to fetch, transform, and store data.

3. **Collector API (Phase-out Path)**
   - Original FastAPI container is running in Minikube.
   - Being used for testing, but will eventually be deprecated as Gloo API Designer takes over.

4. **Storage**
   - Future phases will use Postgres (in-cluster) or Gloo’s built-in data storage for persistence.

5. **AI/ML (Planned)**
   - Gloo AI workflows will later classify ingested data for bot/spam detection.

## Immediate Next Steps
1️⃣ **Create a Gloo Data Source**
- Define a source (e.g., JSONPlaceholder for demo or Twitter for real data).
- Store credentials securely in Gloo Studio.

2️⃣ **Build a Pipeline**
- Ingest → (Optionally transform) → Store.
- Test manually by triggering the pipeline.

3️⃣ **Expose API via Gloo Gateway**
- Define `/collect` (trigger pipeline) and `/data` (read stored data) using API Designer.
- Map these endpoints to the pipeline for end-to-end testing.

4️⃣ **Test Routing**
- Use Minikube IP + Gloo Gateway NodePort to confirm pipeline triggers via API call.

## Future Roadmap
- Phase 2: Deploy Postgres into Minikube or use Gloo-managed storage.
- Phase 3: Build live ingestion pipelines for Twitter/Reddit.
- Phase 4: Integrate Gloo AI for bot/spam detection and alerting.
- Phase 5: Create dashboards & reporting for real-time monitoring.

## Key Benefits of Gloo Studio Migration
- 🚀 **No manual microservice maintenance:** API Designer handles endpoint creation.
- 📊 **Visual data pipelines:** Ingest, clean, and store without extra code.
- 🔒 **Secure API key management:** Tokens for Twitter/X or Reddit are stored in Gloo Studio.
- 🤖 **Seamless AI integration:** Future spam/bot detection via Gloo AI models.
- ☁️ **Scalability:** Easily scale pipelines and storage without refactoring the app.

## Summary
The project is evolving from a containerized FastAPI experiment to a Gloo-native data ingestion and analysis system. With Gloo Studio’s features, we will quickly move from simple API testing to automated pipelines, database-backed data storage, and AI-driven insights — all routed through a single Gloo Gateway endpoint.
