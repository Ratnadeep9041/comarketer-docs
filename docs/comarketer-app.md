# CoMarketer - Literal Project Documentation

## Directory Structure and File Descriptions

### Root
- `comarketer-app/` — Main application directory (Next.js app)
- `docs/` — Project documentation (this file)

### comarketer-app/
- `package.json`, `package-lock.json` — Node.js dependencies and scripts
- `tsconfig.json` — TypeScript configuration
- `next.config.ts` — Next.js configuration
- `postcss.config.mjs` — PostCSS configuration for Tailwind CSS
- `eslint.config.mjs` — ESLint configuration
- `public/` — Static assets (SVGs, favicon, etc.)
- `README.md` — Basic project info and Next.js usage
- `src/` — Application source code

### comarketer-app/src/app/
- `page.tsx` — **Main UI page.** Implements the core React component for the app. Handles user input, displays a file tree, and integrates Sandpack for live code previews. Manages state for messages, file trees, and code generation. Handles API requests to `/api/generate` for code generation.
- `layout.tsx` — **Root layout.** Sets up global fonts (Geist), imports global CSS, and wraps all pages in the HTML structure.
- `globals.css` — Global CSS styles for the app.
- `favicon.ico` — App favicon.

#### comarketer-app/src/app/components/
- `FileTree.tsx` — **File tree component.** Renders a collapsible, recursive file/folder tree UI. Used to visualize the generated project structure. Accepts a tree prop (array of FileNode objects).

#### comarketer-app/src/app/api/
- `generate/route.ts` — **API endpoint.** Handles POST requests for code generation. Receives a prompt, calls the LLM via `unifiedSDK.ts`, parses the response, and returns generated code. Uses utility functions from `utils/prompt.ts`.

#### comarketer-app/src/app/utils/
- `prompt.ts` — **Prompt templates.** Contains various string templates and functions for constructing prompts to send to the LLM (e.g., for generating a project, components, or file trees). Defines strict response formats for LLM compatibility.
- `unifiedSDK.ts` — **LLM provider abstraction.** Exports `generateLLMResponse`, which routes requests to different LLM providers (OpenAI, Azure, Bedrock, Google Vertex, etc.) and returns generated text. Handles provider/model selection and API options.

## Detailed File and Folder Functionality (Logic-Focused)

### comarketer-app/
- **package.json / package-lock.json**: Define project dependencies and scripts for building, running, and linting the app.
- **tsconfig.json**: Configures TypeScript options for type safety and code quality.
- **next.config.ts**: Customizes Next.js build and runtime behavior.
- **postcss.config.mjs**: Sets up PostCSS for Tailwind CSS processing.
- **eslint.config.mjs**: Lints code for style and error prevention.
- **public/**: Contains static assets (SVGs, favicon) served directly by Next.js.
- **src/**: Main application logic and UI.

### comarketer-app/src/app/
- **page.tsx**: The main UI component. Handles user input (project prompts), manages state for messages, file trees, and code previews. Sends requests to the backend API for code generation and updates the UI with results.
- **layout.tsx**: Sets up the global HTML structure, imports fonts and global CSS, and wraps all pages.
- **globals.css**: Global styles for the app.

#### comarketer-app/src/app/components/
- **FileTree.tsx**: Renders a recursive, interactive file/folder tree. Visualizes the generated project structure, allowing users to expand/collapse folders and view files.

#### comarketer-app/src/app/api/
- **generate/route.ts**: API endpoint for code generation. Receives user prompts, constructs system prompts using utility templates, calls the LLM via unifiedSDK, parses the response, and returns generated code/files as JSON.

#### comarketer-app/src/app/utils/
- **prompt.ts**: Contains prompt templates and functions for constructing LLM requests. Ensures strict, parseable response formats (JSON/custom tags) for reliable code generation.
- **unifiedSDK.ts**: Abstracts LLM provider logic. Routes requests to different LLMs (OpenAI, Azure, Bedrock, Google Vertex, etc.), handles model selection, and returns generated text.

---

## Code Preview Approaches: WebContainers vs. Sandpack vs. Manual Hosting

### WebContainers
- **What**: Browser-based Node.js runtime (by StackBlitz) that runs full npm projects in-browser, including server-side code.
- **Pros**:
  - True full-stack environment (can run backend code, npm scripts).
  - High fidelity: matches local dev experience.
- **Cons**:
  - Heavy resource usage; slower startup.
  - Limited browser support.
  - More complex integration.
  - Security sandboxing limits some features.
- **Suitability**: Best for full-stack demos or when backend code must run in-browser.

### Sandpack
- **What**: React component library (by CodeSandbox) for live-editable code previews. Runs code in an iframe sandbox, supports many front-end frameworks.
- **Pros**:
  - Lightweight, fast, and easy to integrate in React apps.
  - Secure: runs code in isolated iframe.
  - Supports live editing, file trees, and custom themes.
  - Good for front-end (React, Next.js, etc.) previews.
- **Cons**:
  - Limited to front-end code (no backend/server-side execution).
  - Some advanced features (custom bundlers, etc.) may require extra setup.
- **Suitability**: Ideal for front-end code previews, interactive documentation, and educational tools.

### Manual Hosting
- **What**: Build and deploy the generated code to a server (local or remote), then embed or link to the running site.
- **Pros**:
  - Full control over environment and deployment.
  - Can support any stack or custom requirements.
- **Cons**:
  - Slow feedback loop (build, deploy, reload).
  - Not interactive or live-editable.
  - Complex to automate for every user/project.
- **Suitability**: Best for production or persistent demos, not for instant previews.

### Why We Chose Sandpack

For CoMarketer, the goal is to provide instant, interactive previews of generated front-end code (React/Next.js) directly in the browser, with a live file tree and code editor. Sandpack offers:

- Seamless React integration.
- Fast, secure, and isolated code execution.
- Live editing and previewing of user-generated code.
- Minimal setup and resource usage compared to WebContainers.
- No need for backend/server-side execution in the preview.

WebContainers were not chosen due to their heavier resource requirements, complexity, and unnecessary backend support for our use case. Manual hosting was rejected due to its lack of interactivity and slow feedback.

**In summary:** Sandpack provides the best balance of speed, security, and user experience for live front-end code previews in this project.

---

## Main Logic Flow
1. **User interacts with the UI** (`page.tsx`):
   - Enters a prompt describing the desired project/app.
   - Submits the prompt, which triggers a POST request to `/api/generate`.
2. **API Route** (`api/generate/route.ts`):
   - Receives the prompt, constructs a system prompt using templates from `utils/prompt.ts`.
   - Calls `generateLLMResponse` from `utils/unifiedSDK.ts` to get a response from the selected LLM provider.
   - Parses the LLM response to extract code/files.
   - Returns the generated code/files as JSON.
3. **UI updates** (`page.tsx`):
   - Receives the generated code/files.
   - Updates the file tree and code preview (via Sandpack and `FileTree.tsx`).
   - Allows the user to explore the generated project structure and code.

## Deployment

### Deploying to Vercel

CoMarketer is designed to be easily deployed on Vercel, which is the recommended platform for Next.js applications. Follow these steps to deploy:

1. **Push your code to a Git repository** (GitHub, GitLab, or Bitbucket).
2. **Sign up or log in to [Vercel](https://vercel.com/).**
3. **Import your repository:**
   - Click "New Project" and select your repository.
   - Vercel will auto-detect the Next.js framework and suggest default build settings.
4. **Configure environment variables** (if needed):
   - In the Vercel dashboard, go to your project settings > Environment Variables.
   - Add any required variables (e.g., API keys).
5. **Deploy:**
   - Click "Deploy". Vercel will build and deploy your app.
   - After deployment, you’ll get a live URL for your app.

#### Automatic Previews
- Every push to your repository (main or branches) triggers an automatic deployment and generates a unique preview URL for testing.

### Why Vercel and Not Netlify?

- **Vercel** is the creator and primary maintainer of Next.js, offering first-class support for all Next.js features (including API routes, ISR, SSR, and edge functions).
- **Seamless integration:** Vercel provides zero-config deployments for Next.js, automatic static optimization, and instant rollbacks.
- **Performance:** Vercel’s global edge network ensures fast delivery and optimized caching for Next.js apps.
- **Developer Experience:** The Vercel dashboard, preview deployments, and Git integration are tailored for Next.js workflows.

**Netlify** is also a powerful platform and supports Next.js, but some advanced features (like ISR, middleware, or edge functions) may require extra configuration or are not as tightly integrated as on Vercel. For the best compatibility, performance, and ease of use with Next.js, Vercel is the preferred choice for this project.

---

## Utility Details
- **`prompt.ts`**: Defines strict prompt/response formats for LLMs to ensure parseable, structured output (JSON or custom tags). Includes multiple prompt variants for different frameworks (React, Next.js, etc.).
- **`unifiedSDK.ts`**: Abstracts LLM provider logic, allowing easy switching between OpenAI, Azure, Bedrock, Google, etc. Handles model selection and API options.

## Component Details
- **`FileTree.tsx`**: Recursively renders folders/files. Supports expand/collapse for folders. Used to visualize the generated project structure in the UI.

## API Details
- **`/api/generate`**: Accepts `{ prompt: string }` in POST body. Returns `{ code: string }` (the generated code/files from the LLM).

---
This documentation provides a literal, technical breakdown of the project structure, file purposes, and main logic flow for developers and contributors. 