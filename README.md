# AI Photo Gallery Manager

A local, AI-powered photo management tool that helps you **search, review, and safely delete photos using natural language**.

This app scans your photo folders, understands what's inside each image using an AI vision model, and lets you find images with prompts like:

- "math notes"
- "handwritten equations"
- "whiteboard"
- "documents"
- "screenshots with text"

You stay fully in control: everything runs locally except the AI calls, and deletions go to the **Windows Recycle Bin**, not permanent delete.

---

## What This App Does

### 1. Indexes Your Photos
You point the app to one or more photo folders. For each image, it:

- Loads and downsizes the image (for speed and lower API cost)
- Generates a **short descriptive caption** using an AI vision model
- Creates a **semantic embedding** of that caption
- Stores everything locally in a small SQLite database

Only metadata is stored -- your images remain exactly where they are on disk.

---

### 2. Lets You Search with Natural Language
Instead of folders and filenames, you search using meaning.

Examples:
- "math notes"
- "handwritten formulas"
- "passport photo"
- "notes on lined paper"

The app converts your query into an embedding and finds the most semantically similar images, even if the exact words never appear.

---

### 3. Shows Results Visually
Search results are displayed as:

- Image thumbnails
- AI-generated captions
- Relevance scores

You can visually inspect everything before taking any action.

---

### 4. Safely Deletes Photos (Recycle Bin)
Selected images can be removed **from within the app**.

Important:
- Files are sent to the **Windows Recycle Bin**
- Nothing is permanently deleted
- Deleted files are marked as such in the local database

This makes cleanup safe and reversible.

---

## Why This Exists

Traditional photo managers rely on:
- Folder structure
- Filenames
- Manual tagging

This app is designed for:
- Large, messy photo collections
- Scanned notes, whiteboards, screenshots
- People who want to *search by meaning*, not by memory

It is especially useful for:
- Students
- Teachers
- Researchers
- Anyone with years of screenshots or photographed notes

---

## AI Provider Design (OpenAI / Gemini)

The app is built with a **pluggable AI provider interface**.

- OpenAI is used by default
- Gemini can be swapped in later without changing the app logic
- Provider choice is controlled via environment variables

This avoids lock-in and keeps the core app stable.

---

## What Runs Locally vs Remotely

**Local**
- Folder scanning
- Image previews
- Database (SQLite)
- Search ranking
- Deletion logic

**Remote (via API)**
- Image captioning
- Text embeddings

No images or metadata are uploaded anywhere except during the AI request itself.

---

## Project Structure (Simplified)

