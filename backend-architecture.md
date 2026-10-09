# Backend architecture

Proposed architecture for the AI-Animated Children's Story Frame. Student D owns the backend API, data and media storage design, job orchestration, and frame delivery. Stack choices remain subject to team approval.

```mermaid
flowchart TD
    APP["Parent mobile app — Student C"]
    FRAME["Story frame — Student A"]

    subgraph BACKEND["Backend subsystem — Student D"]
        API["REST API"]
        DB[("Relational database")]
        QUEUE["Generation queue"]
        WORKER["Background worker"]
        STORAGE[("Media object storage")]
    end

    AI["AI and moderation — Student B"]

    APP -->|"Upload drawing and settings · Request generation · Check status"| API
    FRAME -->|"Authenticate · Request assigned content · Acknowledge completed download"| API
    API <-->|"Metadata and ownership checks"| DB
    API -->|"Save validated drawing"| STORAGE
    API -->|"Enqueue job and return job ID"| QUEUE
    QUEUE -->|"Dispatch job"| WORKER
    WORKER <-->|"Generation request and result"| AI
    WORKER <-->|"Read drawing · Save validated result"| STORAGE
    WORKER -->|"Update job state and result metadata"| DB
    API -->|"Authorized media download link"| FRAME
    STORAGE -->|"Download assigned media"| FRAME
```

## Proposed stack

| Component | Proposed choice |
| --- | --- |
| REST API | FastAPI |
| Database | PostgreSQL |
| Media storage | S3-compatible object storage |
| Queue | Redis with a task queue |
| Worker | Python background worker |

## Architecture notes

- The API returns a job ID immediately after queueing; slow AI generation runs in the worker.
- The database stores metadata and relationships; object storage holds image, video, and audio files.
- Parents and frames authenticate separately. The API checks ownership and frame assignments before issuing time-limited media download links.
- Generated media is available only after required validation and moderation succeed.
- Job lifecycle: `UPLOADED → QUEUED → GENERATING → MODERATING → READY → DELIVERED`. Failures enter `FAILED` with a recorded reason.
- `DELIVERED` means the assigned frame has acknowledged a successful download. It does not imply playback.
- Story text and narration generation remain an interface decision to confirm with Student B.

