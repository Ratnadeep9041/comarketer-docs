# CoMarketer

A Next.js-based AI-powered code/project generator with live code preview, file tree visualization, and instant deployment to Vercel.

---

## Overview
CoMarketer is a developer tool that lets users generate, preview, and deploy full-stack (primarily front-end) projects using LLMs (OpenAI, Bedrock, Gemini, etc.). It features a live file tree, code editor, and instant deployment to Vercel, all within a modern Next.js app.

## Features
- **AI-powered code generation**: Generate complete project structures and code from natural language prompts.
- **Live file tree**: Visualize and explore generated project files/folders interactively.
- **Sandpack integration**: Live-edit and preview code in-browser (React/Next.js/Tailwind supported).
- **Instant Vercel deployment**: Deploy generated projects to Vercel with one click (supports custom domains).
- **Modern UI**: Built with Radix UI, Tailwind CSS, and custom components.
- **Multi-provider LLM support**: Easily switch between OpenAI, Bedrock, Gemini, Azure, and more.
- **Redis caching**: (Optional) for storing generated files and improving performance, so large outputs do not overwhelm the server or client. 