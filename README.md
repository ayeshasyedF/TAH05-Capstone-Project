

**File Architecture - Project**
TAH05-Capstone-Project/
├── frontend/                  # Student C's mobile app
├── backend/                   # <-- Type "backend" in Supabase's Working directory box
│   ├── supabase/              # Supabase CLI automatically looks inside backend/ for this
│   │   ├── migrations/        # Your 7 table schemas, RLS policies & functions
│   │   ├── functions/         # Edge Functions
│   │   └── config.toml
│   └── backend-architecture.md
└── README.md


**File Architecture -- Backend**
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
