# API Endpoints

- **POST `/api/generate`**: Accepts `{ prompt: string }`. Uses LLMs to generate code/files, returns `{ returns:stream }`.
- **POST `/api/deploy`**: Accepts `{ files, customDomain? }`. Deploys generated code to Vercel, returns deployment URL. 