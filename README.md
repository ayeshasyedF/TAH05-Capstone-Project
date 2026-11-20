File Architecture -- Backend

PARENT MOBILE APPLICATION
    │
    ▼
BACKEND / API LAYER
    │
    ├── SUPABASE DATABASE (PostgreSQL) ✅
    │     ├── profiles
    │     ├── frames
    │     ├── drawings
    │     ├── generation_jobs
    │     ├── stories
    │     ├── story_assets
    │     └── frame_content_assignments
    │
    ├── SUPABASE AUTHENTICATION ✅
    │
    └── SUPABASE STORAGE ✅
          ├── drawings
          └── story-assets
    │
    ▼
AI GENERATION PIPELINE
    │
    ▼
GENERATED CONTENT STORED IN SUPABASE
    │
    ▼
PHYSICAL SMART FRAME
