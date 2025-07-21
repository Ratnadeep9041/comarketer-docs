# Core Architecture & Main Logic Flow

## Main UI (`src/app/page.tsx`)
- Handles user input, manages state for messages, file tree, and code preview.
- Integrates Sandpack for live code editing and preview.
- Renders the file tree (`FileTree.tsx`) and deploy button (`deployButton.tsx`).
- Handles API requests to `/api/generate` and `/api/deploy`.

## Usage
1. **Enter a prompt** describing the app/project you want to generate.
2. **Submit** to trigger code generation (calls `/api/generate`).
3. **Explore** the generated file tree and code preview (live-editable via Sandpack).
4. **Deploy** instantly to Vercel (with or without a custom domain).

## LLM Integration
- **`unifiedSDK.ts`**: Abstracts provider logic (OpenAI, Bedrock, Gemini, Azure, Vertex, etc.). Handles prompt routing, model selection, and API options.
- **`prompt.ts`**: Defines strict prompt/response formats for LLMs (JSON/custom tags) to ensure parseable, structured output.
- **`gemini.ts`**: Handles Gemini API requests and response parsing.
- **`redis.ts`**: (Optional) Caches generated files for performance and to avoid overwhelming the server/client.

## Sandpack Integration
- Used for live, in-browser code preview and editing (React/Next.js/Tailwind projects).
- Secure, fast, and isolated (runs in iframe sandbox). 