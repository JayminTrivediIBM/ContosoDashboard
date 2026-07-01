# Data Model: Document Upload and Management

## Entities

### Document
- DocumentId: int
- Title: string
- Description: string?
- Category: string
- Tags: string?
- FileName: string
- FilePath: string
- FileSizeBytes: long
- FileType: string
- UploadedByUserId: int
- ProjectId: int?
- TaskId: int?
- UploadDate: DateTime
- UpdatedDate: DateTime?
- ScanStatus: string
- ScanCompletedDate: DateTime?
- IsDeleted: bool

### DocumentShare
- DocumentShareId: int
- DocumentId: int
- UserId: int
- SharedByUserId: int
- ShareDate: DateTime
- IsActive: bool

### DocumentActivity
- DocumentActivityId: int
- DocumentId: int
- UserId: int
- ActivityType: string
- ActivityDate: DateTime
- Details: string?

## Relationships

- A User uploads many Documents.
- A Project may contain many Documents.
- A Task may contain many Documents.
- A Document may have many DocumentShares.
- A Document may have many DocumentActivities.

## Validation Rules

- Title is required.
- Category must be one of the supported values from the feature spec.
- FileName and FilePath must be non-empty.
- FileSizeBytes must be greater than zero.
- FileType must be stored as text and should be limited to a practical length for MIME types.
