# Deployment

### How Deployment Works
- Deployments are handled by the `/api/deploy` endpoint (see `src/app/api/deploy/route.ts`).
- **No GitHub account is required**: Projects are deployed directly to a shared Vercel account via the Vercel API, not through GitHub integration.
- **All generated projects are initially deployed to the same Vercel account** (the app’s own account). This makes deployment instant and seamless for users.
- **Migration**: If a user wants, they can later migrate the project to their own Vercel account for full control and customization.
- **Custom domains** are supported at deploy time.

#### Why this approach?
- **Faster onboarding**: No need for users to connect GitHub or set up their own Vercel account to see a live deployment.
- **Simplicity**: All deployment logic is managed in the backend (`deploy/route.ts`), not via GitHub Actions or external CI.
- **User flexibility**: Users can migrate to their own account at any time for production use.

#### Redis Usage
- **Redis** is used to store and retrieve generated files, so large code outputs do not overwhelm the server or client. This enables efficient caching and retrieval, especially for big projects or repeated requests.



## Why Vercel and Not Netlify?
- Vercel is the creator and primary maintainer of Next.js, offering first-class support for all Next.js features.
- Seamless integration, zero-config deployments, automatic static optimization, and instant rollbacks.
- Performance: Vercel’s global edge network ensures fast delivery and optimized caching.
- Developer Experience: The Vercel dashboard, preview deployments, and Git integration are tailored for Next.js workflows.

Netlify is also a powerful platform and supports Next.js, but some advanced features may require extra configuration or are not as tightly integrated as on Vercel. For the best compatibility, performance, and ease of use with Next.js, Vercel is the preferred choice for this project. 