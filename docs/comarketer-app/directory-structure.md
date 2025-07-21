# Directory Structure

```
comarketer-app/
├── package.json           # Project dependencies and scripts
├── tsconfig.json          # TypeScript configuration
├── next.config.ts         # Next.js configuration
├── postcss.config.mjs     # Tailwind/PostCSS config
├── eslint.config.mjs      # ESLint config
├── public/                # Static assets (SVGs, favicon, etc.)
├── src/
│   ├── app/
│   │   ├── page.tsx               # Main UI page (core logic, state, Sandpack, file tree)
│   │   ├── layout.tsx             # Root layout, global CSS/fonts
│   │   ├── globals.css            # Global styles
│   │   ├── favicon.ico            # App favicon
│   │   ├── components/
│   │   │   ├── FileTree.tsx           # Recursive file/folder tree UI
│   │   │   ├── deployButton.tsx       # Vercel deploy dialog/button
│   │   │   └── ChatWebsiteLoader.tsx  # Animated loader for code generation
│   │   ├── api/
│   │   │   ├── generate/route.ts      # POST /api/generate (code generation)
│   │   │   └── deploy/route.ts        # POST /api/deploy (Vercel deployment logic)
│   │   └── utils/
│   │       ├── prompt.ts              # Prompt templates/formatting for LLMs
│   │       ├── unifiedSDK.ts          # LLM provider abstraction
│   │       ├── gemini.ts              # Gemini API integration
│   │       └── redis.ts               # Redis connection utility (stores generated files)
│   ├── components/
│   │   └── ui/
│   │       ├── button.tsx             # Button primitive
│   │       ├── dialog.tsx             # Dialog/modal primitive
│   │       ├── label.tsx              # Label primitive
│   │       └── textarea.tsx           # Textarea primitive
│   └── lib/
│       └── utils.ts                   # Utility: className merging
└── README.md                  # Project documentation (this file)
```

See each file for details on its purpose and usage. 