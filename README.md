[README.md](https://github.com/user-attachments/files/27093396/README.md)
# 3D Model Workspace

**A web-based 3D workspace for cosmetic product design — with AI-powered material suggestions, label mapping, and real-time visualization.**

![Next.js](https://img.shields.io/badge/Next.js-16-black) ![TypeScript](https://img.shields.io/badge/TypeScript-5-blue) ![Three.js](https://img.shields.io/badge/Three.js-green) ![License](https://img.shields.io/badge/License-Private-red)

---

## Table of Contents

- [What You Can Do](#what-you-can-do)
- [Live Demo](#live-demo)
- [Quick Start (3 Steps)](#quick-start-3-steps)
- [Getting a 3D Model](#getting-a-3d-model)
- [Feature Guide](#feature-guide)
- [Tech Stack](#tech-stack)
- [Environment Variables](#environment-variables)
- [Project Structure](#project-structure)
- [Deployment](#deployment)

---

## What You Can Do

| Feature | Description |
|---------|-------------|
| **Upload & View 3D Models** | Drag & drop `.glb`, `.fbx`, or `.gltf` files — they render in an interactive 3D viewport |
| **Material Editor** | 18 cosmetic material presets (Matte, Shiny, Glassy, Metallic, Glitter...) with real-time preview |
| **AI Material Suggestions** | Click "AI Suggest" to get smart material recommendations based on your product name |
| **Label / Decal System** | Upload label images and map them onto 3D model surfaces |
| **Lighting Studio** | Add ambient, directional, point, and spot lights — full control over color, intensity, position |
| **Transform Controls** | Move, rotate, scale any object in the scene with precise numeric input |
| **Layer Hierarchy** | Scene tree showing all objects — click to select, expand to inspect |
| **Sketch Mode** | Draw concepts on canvas and convert to 3D (requires AI API key) |
| **AI Concept Generator** | Generate 3D models from text prompts or images (requires Meshy/Tripo API key) |

> **Everything works without API keys except AI 3D generation.** See [Demo Mode](#demo-mode) below.

---

## Live Demo

Deployed at: **[Click here to open the live app](https://2jcw24f395.coze.site)**

---

## Quick Start (3 Steps)

### Prerequisites

- **Node.js 18+** (recommended: 20+)
- **pnpm** package manager (`npm i -g pnpm`)

### Step 1: Install

```bash
# Extract the ZIP you downloaded
unzip 3d-model-workspace-github.zip
cd 3d-model-workspace-github

# Install dependencies (~2 minutes on first run)
pnpm install
```

### Step 2: Configure (Optional)

```bash
# Copy the environment template
cp .env.example .env.local
```

**You can skip this step entirely.** The app works in Demo Mode without any configuration.
Only add API keys if you want AI-powered 3D generation (see [Environment Variables](#environment-variables)).

### Step 3: Run

```bash
# Start development server
pnpm dev
```

Open **http://localhost:5000** in your browser.

---

## Getting a 3D Model

The app needs a 3D model file to get started. Here are free sources:

### Free GLB/FBX Model Sources

| Source | URL | Notes | Format |
|--------|-----|-------|--------|
| **Sketchfab** | https://skify.com/sketchfab | Largest free 3D model library | GLB/GLTF |
| **Poly Pizza** | https://poly.pizza | Low-poly, optimized for web | GLB/GLTF |
| **TurboSquid (Free)** | https://www.turbosquid.com/free-3d-models | Filter by "free" | FBX/GLB/OBJ |
| **Smithsonian 3D** | https://3d.si.edu/api/v1/artwork?api_key=yourkey | Museum-quality scans | GLTF |
| **ReadyPlayerMe** | https://readyplayer.me | Avatar/character models | GLB |

### Recommended Test Models for This App

Since this is a **cosmetic product workspace**, try searching for:

- `lipstick glb`
- `perfume bottle fbx`
- `cosmetics container gltf`
- `makeup palette 3d`
- `cream jar glb`

### How to Download from Sketchfab (Most Popular)

1. Go to https://skify.com/sketchfab
2. Search for a model (e.g., "lipstick")
3. Click **Download** → Choose **GLB** format
4. Save the `.glb` file to your computer
5. In this app, click **"Upload 3D Model"** and select the file

### File Size Guidelines

| Size | Recommendation |
|------|---------------|
| < 5 MB | ✅ Ideal — loads instantly |
| 5–20 MB | ✅ Good — short loading time |
| 20–50 MB | ⚠️ Acceptable — may take a few seconds |
| > 50 MB | ⚠️ Large — consider optimizing first |

---

## Feature Guide

### 1. Home Page

```
┌─────────────────────────────────────────────┐
│   🎨 3D Model Workspace                      │
│   Create Stunning Beauty Visualizations      │
│                                             │
│   ┌──────────┐  ┌──────────┐               │
│   │ Upload   │  │ Create   │               │
│   │ 3D Model │  │ Sketch   │               │
│   │          │  │          │               │
│   │ .glb/.fbx│  │ AI→3D    │               │
│   └──────────┘  └──────────┘               │
│                                             │
│   Your Projects                             │
│   ┌──────────────────────────────────┐     │
│   │ No projects yet                   │     │
│   │ Quick Start guide here...         │     │
│   └──────────────────────────────────┘     │
└─────────────────────────────────────────────┘
```

### 2. Workspace Page (After Uploading a Model)

The workspace has three main areas:

```
┌──────────────────────────────────────────────────────┐
│ Toolbar: [Select] [Move] [Rotate] [Scale] [Label]    │
├──────────────────────┬───────────────────────────────┤
│                      │  Right Panel                  │
│                      │  ┌─────────────────────────┐  │
│   3D VIEWPORT        │  │ [Model] [Gen] [Labels]  │  │
│   (Interactive)       │  ├─────────────────────────┤  │
│                      │  │                         │  │
│   • Drag to orbit     │  │  Content changes based  │  │
│   • Scroll to zoom    │  │  on selected tab:       │  │
│   • Click to select   │  │                         │  │
│                      │  │  - Material Presets     │  │
│                      │  │  - Color/Roughness/etc  │  │
│                      │  │  - Lighting controls    │  │
│                      │  │  - Transform values     │  │
│                      │  │  - Layer tree           │  │
│                      │  └─────────────────────────┘  │
│                      │                               │
│   Layer Panel         │                               │
│   (Scene hierarchy)   │                               │
└──────────────────────┴───────────────────────────────┘
```

### 3. Material Editor (18 Presets)

Each preset applies a unique combination of color, roughness, metalness, and transparency:

| Category | Presets |
|----------|---------|
| **Matte** | Matte, Soft, Creamy, Velvet, Frosted, Ceramic, Rubber |
| **Glossy** | Shiny, Glossy, Satin, Pearl, Champagne |
| **Special** | Metallic, Glassy, Neon, Holo, Glitter, Rose Gold |

Click any preset card to apply it instantly to the selected 3D object. The colored preview shows the actual texture pattern (not just solid color).

### 4. AI Material Suggestions

1. Select a 3D model in the viewport
2. Open the **Material** panel
3. Click the **AI Suggest** button
4. Wait 2–3 seconds for AI analysis
5. Click any suggestion card to apply it

The AI reads your project name and recommends the best cosmetic materials (e.g., suggests "Shiny + Metallic" for a lipstick, "Soft + Creamy" for a foundation).

### 5. Label / Decal Workflow

1. Switch to the **Labels** tab in the right panel
2. **Upload** a label image (PNG/JPG with transparency works best)
3. **Map** the label to a mesh surface:
   - Select coverage mode: **Full** (covers entire surface) or **Single** (click to place)
   - Click **Apply Label**
4. The label texture appears on the 3D model in real-time

### 6. Lighting Controls

| Light Type | Use Case |
|-----------|----------|
| **Ambient** | Base illumination — prevents pure black shadows |
| **Directional** | Sun-like light — creates defined shadows |
| **Point** | Bulb-like — emits light in all directions from a point |
| **Spot** | Flashlight — cone-shaped focused light |

Adjust color, intensity, and position for each light. Changes reflect in real-time.

---

## Tech Stack

| Component | Technology |
|-----------|-----------|
| Framework | Next.js 16 (App Router) |
| Language | TypeScript 5 (strict mode) |
| UI Library | shadcn/ui + Radix UI Primitives |
| Styling | Tailwind CSS 4 |
| 3D Engine | Three.js + React Three Fiber + Drei |
| State | Zustand (global store) |
| Database | PostgreSQL (custom storage layer) |
| Storage | S3-compatible (coze-coding-dev-sdk) |
| AI (Materials) | LLM (built-in, no key needed) |
| AI (3D Gen) | Meshy AI / Tripo AI (optional) |

---

## Environment Variables

Create a `.env.local` file in the project root (copy from `.env.example`):

### For Full Functionality (Optional)

| Variable | What It Does | Get It From |
|----------|-------------|-------------|
| `MESHY_API_KEY` | Enables AI text/image → 3D generation | [meshy.ai](https://www.meshy.ai/) |
| `TRIPO_API_KEY` | Backup 3D generation provider | [tripo.ai](https://tripo.ai/) |
| `HUNYUAN_3D_API_KEY` | Third backup provider | Tencent Cloud |

### Demo Mode (No Keys Needed)

Leave all variables empty. These features still work:

- ✅ Upload and view GLB/FBX/GLTF models
- ✅ All 18 material presets with texture previews
- ✅ AI material suggestions (uses built-in LLM)
- ✅ Label upload, mapping, and application
- ✅ Full lighting studio
- ✅ Transform controls (position/rotation/scale)
- ✅ Layer hierarchy panel
- ✅ Sketch drawing canvas

**Only disabled without keys:** AI 3D generation (Make3D button shows demo fallback).

---

## Project Structure

```
3d-model-workspace/
├── src/
│   ├── app/
│   │   ├── page.tsx              # Home page (upload/create projects)
│   │   ├── layout.tsx            # Root layout
│   │   ├── api/
│   │   │   ├── make3d/route.ts          # POST: Start 3D generation task
│   │   │   ├── make3d/[taskId]/route.ts # GET: Poll task status
│   │   │   ├── ai/material-suggest/     # POST: AI material recommendations
│   │   │   ├── projects/route.ts        # GET: List projects
│   │   │   ├── projects/[id]/route.ts   # GET/PUT/DELETE: CRUD
│   │   │   ├── projects/[id]/model/     # GET: Serve model file (GLB/FBX/GLTF)
│   │   │   └── labels/route.ts          # POST/DELETE: Label management
│   │   └── workspace/[id]/page.ts # Main 3D workspace
│   ├── components/
│   │   ├── ModelViewer.tsx        # Three.js 3D viewport (core)
│   │   ├── MaterialPanel.tsx      # Material editor + 18 presets + AI suggest
│   │   ├── GeneratePanel.tsx      # AI concept generator UI
│   │   ├── LabelsPanel.tsx        # Label upload/mapping/apply
│   │   ├── LightingPanel.tsx      # Light type/color/intensity/position
│   │   ├── TransformPanel.tsx     # Position/rotation/scale inputs
│   │   ├── LayerPanel.tsx         # Scene hierarchy tree
│   │   ├── RightPanel.tsx         # Tab container (Model/Gen/Labels)
│   │   └── DrawingCanvas.tsx      # Sketch mode canvas
│   ├── storage/database/          # PostgreSQL data layer
│   └── utils/                    # Shared utilities
├── public/                       # Static assets (models uploaded here)
├── scripts/                      # Build/start scripts
├── package.json
├── pnpm-lock.yaml
├── tsconfig.json
├── next.config.ts
├── tailwind.config.ts
├── postcss.config.mjs
├── .coze                         # Coze deployment config
├── .env.example                  # Environment variable template
├── .gitignore
└── README.md                     # This file
```

---

## Deployment

### Option A: Local Development

```bash
pnpm install
cp .env.example .env.local   # optional
pnpm dev                     # http://localhost:5000
```

### Option B: Production Build

```bash
pnpm build                   # Builds to .next/
pnpm start                   # Starts production server on port 5000
```

### Option C: Docker (Example)

```dockerfile
FROM node:20-alpine
WORKDIR /app
COPY package.json pnpm-lock.yaml ./
RUN corepack enable && pnpm install --frozen-lockfile
COPY . .
RUN pnpm build
EXPOSE 5000
CMD ["pnpm", "start"]
```

### Option D: Vercel / Netlify

This is a standard Next.js app. Connect your GitHub repo to:
- [Vercel](https://vercel.com) (zero-config for Next.js)
- [Netlify](https://netlify.com) (with `pnpm build` build command)

Set environment variables in the platform dashboard.

---

## Troubleshooting

| Problem | Solution |
|---------|-----------|
| `pnpm install` fails | Ensure Node.js 18+ is installed. Try `node -v` to check. |
| Port 5000 already in use | Kill the process: `lsof -ti:5000 \| xargs kill -9`, or change port in `.coze`. |
| Model doesn't load (404) | Make sure the file is `.glb`, `.fbx`, or `.gltf`. Check browser console for errors. |
| Material panel empty | Click on a 3D object in the viewport first to select it. |
| AI Suggest button not working | Requires internet connection (calls built-in LLM). No API key needed. |
| Make3D returns error | Requires `MESHY_API_KEY` or `TRIPO_API_KEY` in `.env.local`. Without keys, it runs in demo mode. |
| Labels don't appear on model | Ensure the label image is PNG/JPG format. Try "Full Coverage" mode first. |

---

## License

Private project — All rights reserved.
