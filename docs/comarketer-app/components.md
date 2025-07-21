# Component & Utility Reference

## UI Components
- **FileTree.tsx**: Recursive, collapsible file/folder tree. Visualizes project structure.
- **deployButton.tsx**: Dialog/modal for deploying to Vercel (supports custom domain input).
- **ChatWebsiteLoader.tsx**: Animated loader for code generation progress.
- **UI primitives** (`src/components/ui/`): Button, Dialog, Label, Textarea (Radix UI-based, Tailwind styled).

## Utilities
- **prompt.ts**: Prompt templates and formatting for LLMs.
- **unifiedSDK.ts**: LLM provider abstraction and routing.
- **gemini.ts**: Gemini API integration and response parsing.
- **redis.ts**: Redis connection utility (stores generated files to avoid server/client overload).
- **lib/utils.ts**: Utility for merging Tailwind/className values. 