# Research: Document Upload and Management

## Decision: Use a service-based document workflow with a file storage abstraction and queued background scanning

The feature will follow the existing repository pattern of service classes and EF Core data access. A new document service will orchestrate validation, persistence, authorization, and activity logging. File storage will be handled by an abstraction so the training implementation can use the local file system while remaining compatible with a future Azure-backed implementation. After a file is uploaded, the application will publish a scan request to Azure Queue Storage and an Azure Functions worker will process it asynchronously through a Queue trigger, updating the document status once scanning completes.

### Rationale

- The app already uses service classes for business logic and uses dependency injection consistently.
- This approach keeps the implementation aligned with the repository’s architecture and the constitution’s offline-first guidance.
- A storage abstraction supports the stated migration path without forcing a rewrite of the UI or business logic.
- Queue-triggered Azure Functions provide a natural fit for asynchronous malware scanning and keep the upload workflow responsive while still supporting a future cloud-based deployment.

### Alternatives considered

- Direct page-level file handling: rejected because it would duplicate validation and authorization logic and would not fit the current architecture.
- Using a database-only approach for file storage: rejected because the stakeholder requirement explicitly calls for local filesystem storage and secure file handling outside web-root.
- A full new subsystem or separate microservice: rejected because it would be too heavy for the current training project and would violate the simplicity principle.
