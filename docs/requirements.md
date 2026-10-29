# KT Copilot — Software Requirements Specification

**Project:** KT Copilot  
**Version:** 1.0  
**Status:** Initial requirements  
**Frontend:** Angular  
**Backend:** Java and Spring Boot  
**AI:** Gemini API with Spring AI  
**Database:** PostgreSQL with pgvector

## 1. Project Overview

KT Copilot is an AI-powered knowledge transfer platform designed to help software development teams capture, organize, search, and share technical project knowledge.

The platform uses Generative AI and Retrieval-Augmented Generation (RAG) to answer questions from project documentation, assist new team members, and generate structured knowledge transfer materials.

## 2. Problem Statement

Technical knowledge is frequently scattered across documents, API specifications, setup guides, and troubleshooting notes.

This makes onboarding time-consuming and makes it difficult for developers to find accurate answers about an existing software project.

KT Copilot aims to centralize project knowledge and provide a context-aware assistant that answers questions using available documentation.

## 3. Target Users

- **Project Developers:** Find technical information and troubleshoot issues.
- **New Team Members:** Understand project architecture, setup, APIs, and workflows.
- **Technical Leads:** Organize knowledge and prepare handover documentation.
- **Project Administrators:** Manage project workspaces and user access.

## 4. Functional Requirements

### FR-01: Project Management
- Users can create and access authorized project workspaces.
- Each project maintains its own knowledge base.
- Project data must remain isolated from unauthorized users.

### FR-02: Document Management
- Authorized users can upload supported PDF and text-based documents.
- The system extracts text and stores document metadata.
- The system tracks document processing status.
- Unsupported, empty, or invalid files are rejected with meaningful errors.

### FR-03: AI Knowledge Assistant
- Users can ask natural-language questions about project documents.
- The system retrieves relevant document passages before generating an answer.
- Responses should be grounded in retrieved content.
- The assistant should acknowledge when the available information is insufficient.

### FR-04: Source Citations
- Answers should include references to the documents used.
- Users can inspect the relevant source passages.
- Citations should correspond to actual retrieved content.

### FR-05: Onboarding Assistant
- Generate onboarding checklists from available project knowledge.
- Explain project setup instructions and technical concepts.
- Suggest a structured learning sequence for new developers.

### FR-06: KT Document Generation
- Generate structured knowledge transfer documents from approved sources.
- Include system overview, setup instructions, APIs, dependencies, and troubleshooting information when available.
- Allow users to review and edit generated content before saving or exporting it.

### FR-07: Troubleshooting Assistant
- Accept error messages and problem descriptions.
- Retrieve relevant documentation and troubleshooting steps.
- Explain possible causes using supporting evidence.
- Require human review before executing any suggested operational action.

### FR-08: Conversation History
- Maintain question-and-answer history for authorized users.
- Allow users to revisit previous conversations.
- Keep conversations associated with the appropriate project and user.

## 5. Non-Functional Requirements

### Security
- Protect APIs using authentication and authorization.
- Enforce project-level access controls.
- Store API keys securely on the backend.
- Validate uploaded files and restrict file sizes.
- Never expose confidential project data to unauthorized users.

### Performance
- Provide clear processing status for long-running document ingestion.
- Measure API response times and AI processing latency.
- Handle AI provider timeouts and rate limits gracefully.

### Reliability
- Validate AI-generated structured outputs.
- Handle malformed documents and failed processing jobs.
- Avoid presenting unsupported AI-generated claims as established facts.

### Maintainability
- Separate Angular, backend, document-processing, and AI responsibilities.
- Use clear package structure and configuration management.
- Include automated tests and developer documentation.

## 6. Proposed Technology Stack

| Component | Technology |
|---|---|
| Frontend | Angular |
| Backend | Java, Spring Boot |
| AI integration | Spring AI, Gemini API |
| Relational database | PostgreSQL |
| Vector search | pgvector |
| API documentation | Springdoc OpenAPI |
| Backend testing | JUnit, Mockito |
| Version control | Git, GitHub |
| Containerization | Docker |

## 7. High-Level Architecture

1. Angular provides the user interface.
2. Spring Boot exposes secured REST APIs.
3. The document-processing pipeline extracts and chunks document text.
4. The embedding service generates vector representations.
5. PostgreSQL and pgvector store project metadata and embeddings.
6. The retrieval pipeline finds relevant passages for user questions.
7. The LLM generates answers grounded in the retrieved passages.
8. The frontend displays answers, citations, and processing status.

## 8. MVP Scope

The first working version will include:

1. A basic Angular application.
2. A Spring Boot backend with a health-check endpoint.
3. PostgreSQL database connectivity.
4. Document upload and text extraction.
5. Document chunking and embedding generation.
6. RAG-based question answering.
7. Answers with source citations.
8. Basic automated tests.

Authentication, onboarding workflows, KT document generation, and advanced evaluation will be introduced in subsequent phases.

## 9. Acceptance Criteria

The MVP will be considered complete when:

- The Angular frontend communicates with the Spring Boot backend.
- A supported document can be uploaded and processed successfully.
- Extracted content is stored and indexed.
- A user can ask a question related to the uploaded document.
- The system retrieves relevant passages and generates an answer.
- The answer includes verifiable source references.
- Unsupported questions receive an appropriate limitation message.
- Invalid files and AI provider failures are handled gracefully.
- Core backend and frontend workflows have automated tests.

## 10. Future Enhancements

- GitHub repository and source-code analysis.
- Architecture and dependency visualization.
- Knowledge-gap detection.
- Hybrid search and reranking.
- AI response evaluation dashboard.
- Role-specific onboarding plans and quizzes.
- Docker-based deployment and CI/CD automation.

## 11. Development Principles

- Implement features incrementally.
- Prefer evidence-based AI answers over unsupported speculation.
- Keep user data and project workspaces isolated.
- Measure AI quality using a repeatable evaluation dataset.
- Document implementation decisions and known limitations.
