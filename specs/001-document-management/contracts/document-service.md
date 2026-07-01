# Document Service Contract

## Overview

The document service will expose the core operations needed by the UI and future controllers or pages.

## Operations

### UploadAsync
- Input: document metadata, file stream, authenticated user context
- Output: created document record or validation error
- Notes: validates file size and type, generates a safe storage path, persists metadata, queues a scan request, and records an activity entry

### GetAccessibleDocumentsAsync
- Input: authenticated user context and optional filters
- Output: list of documents the user may access
- Notes: enforces role and project-based authorization rules

### DownloadAsync
- Input: document identifier and authenticated user context
- Output: file stream or access error
- Notes: verifies the user can access the document before streaming the file

### UpdateMetadataAsync
- Input: document identifier, metadata updates, authenticated user context
- Output: success or authorization error

### DeleteAsync
- Input: document identifier and authenticated user context
- Output: success or authorization error
- Notes: removes file from storage and the metadata record

### UpdateScanStatusAsync
- Input: document identifier, scan result, and optional failure details
- Output: success or not-found error
- Notes: called by the Azure Functions worker after a scan completes or fails
