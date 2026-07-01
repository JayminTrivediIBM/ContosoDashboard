# Tasks: Document Upload and Management

**Input**: Design documents from `/specs/001-document-management/`
**Prerequisites**: plan.md (required), spec.md (required for user stories), research.md, data-model.md, contracts/

**Organization**: Tasks are grouped by user story to enable independent implementation and testing of each story.

## Format: `[ID] [P?] [Story] Description`

- **[P]**: Can run in parallel (different files, no dependencies)
- **[Story]**: Which user story this task belongs to (e.g., US1, US2, US3)
- Include exact file paths in descriptions

## Phase 1: Setup (Shared Infrastructure)

**Purpose**: Add the shared document infrastructure needed by all user stories.

- [ ] T001 Create document-related directories and supporting configuration files under ContosoDashboard/Services and ContosoDashboard/Models
- [ ] T002 Add document entity, scan status, and related model classes in ContosoDashboard/Models
- [ ] T003 [P] Register document services and storage abstractions in ContosoDashboard/Program.cs

---

## Phase 2: Foundational (Blocking Prerequisites)

**Purpose**: Create the core persistence and access primitives required before any user story can be implemented.

- [ ] T004 Extend ContosoDashboard/Data/ApplicationDbContext.cs with document, share, and activity DbSets and relationships
- [ ] T005 Implement IFileStorageService and LocalFileStorageService in ContosoDashboard/Services
- [ ] T006 Implement IDocumentService and DocumentService with upload, list, search, preview/download, metadata update, and delete workflows
- [ ] T007 Add authorization and activity logging hooks for document access and management actions

**Checkpoint**: Foundation ready - user story implementation can now begin.

---

## Phase 3: User Story 1 - Upload and organize work documents (Priority: P1) 🎯 MVP

**Goal**: Allow users to upload supported documents and see them in their document list with required metadata.

**Independent Test**: A user can upload a supported file, provide required metadata, and see the document appear in the list.

### Implementation for User Story 1

- [ ] T008 [P] [US1] Create the document upload UI and form components in ContosoDashboard/Pages
- [ ] T009 [P] [US1] Add document list and category/project filtering UI in ContosoDashboard/Pages
- [ ] T010 [US1] Wire the upload form to DocumentService and file storage in ContosoDashboard/Services
- [ ] T011 [US1] Persist document metadata and queue scan requests after upload in ContosoDashboard/Services
- [ ] T012 [US1] Show upload success/error feedback and progress handling in the UI

**Checkpoint**: User Story 1 should be fully functional and independently testable.

---

## Phase 4: User Story 2 - Find and access documents securely (Priority: P2)

**Goal**: Allow authorized users to search, preview, and download documents safely.

**Independent Test**: A user can search for a document and access it only when authorized.

### Implementation for User Story 2

- [ ] T013 [P] [US2] Add search and filtering controls to the document browsing experience in ContosoDashboard/Pages
- [ ] T014 [US2] Implement authorization-aware query and access methods in ContosoDashboard/Services
- [ ] T015 [US2] Add preview/download actions and secure file retrieval in ContosoDashboard/Pages and ContosoDashboard/Services
- [ ] T016 [US2] Add document activity logging for downloads and access checks in ContosoDashboard/Services

**Checkpoint**: User Stories 1 and 2 should both work independently.

---

## Phase 5: User Story 3 - Manage and audit documents (Priority: P3)

**Goal**: Support metadata updates, replacement, deletion, and scan status awareness for documents.

**Independent Test**: An authorized user can update or delete a document and see the scan status reflected.

### Implementation for User Story 3

- [ ] T017 [P] [US3] Add document detail/edit UI and scan status display in ContosoDashboard/Pages
- [ ] T018 [US3] Implement metadata update, file replacement, and delete actions in ContosoDashboard/Services
- [ ] T019 [US3] Add Azure Functions queue-triggered scan worker support and status update handling in ContosoDashboard/Services
- [ ] T020 [US3] Expose scan failure/success feedback and audit activity where appropriate in the UI

**Checkpoint**: All user stories should now be independently functional.

---

## Phase 6: Polish & Cross-Cutting Concerns

**Purpose**: Improve the end-to-end experience and ensure the feature is ready for validation.

- [ ] T021 [P] Update documentation and quickstart guidance in specs/001-document-management/quickstart.md
- [ ] T022 Validate upload, search, access, and scan status flows through manual testing
- [ ] T023 [P] Refine error handling, validation feedback, and security checks across document pages and services

---

## Dependencies & Execution Order

- Setup must complete before foundational work.
- Foundational work must complete before any user story implementation.
- User stories can proceed in priority order with the P1 story as the MVP.
- The Azure Functions scan workflow is part of the later management story and should not block the initial MVP upload path.

## Parallel Opportunities

- The upload form and document list UI can be built in parallel.
- The document service and storage abstraction can be implemented in parallel with the UI scaffolding once the foundation is in place.
