# Technical Specification

## 1. Purpose

This document defines the technical implementation of the clothing catalog application.

It establishes the technology stack, architectural principles, project structure, development conventions, and implementation constraints.

This specification must be interpreted together with:

- `specs/IdentitySpec.md`
- `specs/requirementsSpec.md`

The brand identity defines the visual direction.

The product requirements define the expected application behavior.

This document defines how the application will be implemented.

## 2. Technology Stack

### Framework

Astro

Astro must be used as the primary application framework.

The application must use Astro's static site generation capabilities.

### Language

TypeScript

Always use strong typing.

TypeScript must be used for application logic, product data, utilities, and interactive modules.

Use strict type checking.

Avoid the use of `any` unless there is a documented and justified reason.

### Styling

Tailwind CSS v4

Tailwind CSS must be used as the primary styling solution.

The application must use the official Tailwind CSS Vite integration supported by Astro.

The project must not use the legacy Tailwind v3 integration.

### Package Manager

pnpm

pnpm must be the exclusive package manager for the project.

The project must include a `pnpm-lock.yaml` file.

Do not use npm or Yarn to install or manage dependencies.

### Rendering Strategy

Static Site Generation (SSG)

The application must generate static HTML pages during the build process.

The production application must not require server-side rendering or a server adapter.

## 3. Architectural Principles

### 3.1 Astro-First Architecture

Astro components must be the default choice for application structure and presentation.

Use `.astro` components for:

- Layouts.
- Pages.
- Navigation.
- Product cards.
- Product information.
- Static sections.
- Reusable presentation components.

Do not introduce a UI framework by default.

### 3.2 Progressive Interactivity

The application must prioritize static HTML and CSS.

Client-side JavaScript must only be introduced for functionality that requires interaction.

Examples include:

- Catalog filtering.
- Product sorting.
- Product search.
- Mobile navigation.
- Product image galleries.

Interactive functionality must remain isolated and must not require the entire application to run as a client-side SPA.

### 3.3 No Backend Architecture

The application must not introduce:

- API clients.
- Backend services.
- Database repositories.
- Authentication services.
- Server-side business logic.
- Environment-dependent backend configuration.

The initial application is a static frontend.

### 3.4 Simplicity

Prefer straightforward implementations over unnecessary abstractions.

Do not introduce architectural layers, dependency injection, state management libraries, or complex design patterns without a concrete requirement.

The project should remain easy to understand and maintain.

## 4. Project Structure

Use the following initial project structure:

```text
src/
├── assets/
│   ├── images/
│   │   ├── products/
│   │   └── editorial/
│   └── fonts/
├── components/
│   ├── layout/
│   ├── catalog/
│   └── product/
├── data/
│   ├── products.ts
│   └── categories.ts
├── layouts/
│   └── BaseLayout.astro
├── pages/
│   ├── index.astro
│   ├── catalog/
│   │   ├── index.astro
│   │   └── [slug].astro
│   └── products/
│       └── [slug].astro
├── scripts/
│   └── catalog/
├── styles/
│   └── global.css
└── types/
    └── product.ts

public/
├── favicon.svg
└── brand/

docs/
├── brand/
│   └── BRAND-IDENTITY.md
├── product/
│   └── PRODUCT-REQUIREMENTS.md
└── technical/
    └── TECHNICAL-SPEC.md
```

This structure is an initial organizational guideline.

Do not create empty directories or files without a concrete implementation need.

The structure may evolve as the project develops, provided the architectural principles remain intact.

## 5. Product Data

### 5.1 Local Data Source

Product information must be stored in a local, typed dataset.

The initial source of truth must be:

`src/data/products.ts`

Product data must not be duplicated across pages or presentation components.

### 5.2 Product Types

Define a shared TypeScript product model.

The model must support:

- Unique identifier.
- Slug.
- Name.
- Description.
- Category identifier.
- Price.
- Main image.
- Additional images.
- Optional attributes.
- Optional featured status.

Use appropriate types for prices, image paths, categories, and optional attributes.

### 5.3 Data Access

Catalog operations must be implemented as simple reusable functions.

Examples:

- Retrieve all products.
- Retrieve a product by slug.
- Retrieve products by category.
- Filter products by price.
- Sort products by price.
- Search products by name.

These functions must operate on the local dataset.

They must not depend on Astro components or browser APIs.

Pure catalog operations should be independently testable.

## 6. Asset Management

### Product Images

Product images must be stored locally.

Prefer Astro's asset handling for images that require build-time processing or optimization.

Images must be referenced through the appropriate local asset imports.

Use the `public/` directory for assets that must retain a stable public path or be copied directly without processing.

### Image Optimization

Use Astro's image capabilities when appropriate.

Product images must:

- Preserve their intended aspect ratio.
- Avoid unnecessary distortion.
- Use appropriate dimensions.
- Include meaningful alternative text.
- Be optimized for their display context.

Do not rely on remote image URLs for product content.

## 7. Routing

Astro's file-based routing must be used.

The initial routes must include:

- `/` — Homepage.
- `/catalog/` — Complete catalog.
- `/catalog/[slug]/` — Category catalog.
- `/products/[slug]/` — Product details.

Product and category pages must be generated statically from the local dataset.

Use descriptive, stable slugs.

Unknown product or category slugs must resolve to an appropriate not-found page.

## 8. Client-Side Interactivity

### Implementation

Use native browser JavaScript and TypeScript for initial interactive functionality.

Interactive modules must be separated from static presentation components.

Avoid introducing a global client-side application state unless it becomes necessary.

### Catalog

Catalog interactions must operate on the local product dataset.

Filtering, sorting, and search must update the displayed products without requiring a full page reload.

The catalog must remain usable when JavaScript is unavailable, with static content and navigation still accessible.

### Browser State

Do not persist catalog filters, search terms, or user preferences across sessions unless explicitly required.

The initial implementation does not require local storage or session storage.

## 9. Styling and Design System

Tailwind CSS must be the primary styling system.

The application must implement the visual direction defined in `BRAND-IDENTITY.md`.

### Design Tokens

Define the brand's colors, typography, spacing conventions, and other reusable visual values centrally.

The initial color tokens must include:

- Charcoal Black: `#171615`
- Warm Ivory: `#F3EFE8`
- Espresso Brown: `#4A3429`
- Taupe: `#A18A78`
- White: `#FFFFFF`

Avoid duplicating brand values throughout the application.

### Styling Conventions

- Prefer Tailwind utility classes.
- Use component-scoped CSS only when it provides a clear benefit.
- Avoid unnecessary global CSS.
- Avoid inline styles for ordinary visual properties.
- Do not introduce a second styling framework.

## 10. Dependencies

Keep dependencies minimal.

Only introduce a dependency when it provides meaningful value that cannot be reasonably achieved with the existing stack.

Do not install React, Vue, Svelte, a state management library, or a component library by default.

Any additional dependency must have a clear purpose and must be compatible with Astro and the static deployment model.

## 11. Development Scripts

The project must provide standard development scripts:

- `dev` — Start the local development server.
- `build` — Generate the production static site.
- `preview` — Preview the production build locally.
- `check` — Run Astro and TypeScript diagnostics.
- `test` — Run automated tests.

Use pnpm to execute all project scripts.

## 12. Testing

### Unit Testing

Pure catalog functions must be covered by unit tests.

Tests should cover:

- Category filtering.
- Price filtering.
- Combined filters.
- Sorting.
- Search.
- Product lookup.
- Empty results.

### Build Validation

The production build must complete successfully before deployment.

The application must not contain unresolved imports, invalid routes, or TypeScript errors.

## 13. Build and Deployment

The application must produce a static production build.

The generated output must be deployable to a static hosting provider.

The production deployment must not require:

- Node.js runtime services.
- Database connections.
- Backend environment variables.
- Server adapters.

The deployment process must use the project's lockfile to ensure reproducible dependency installation.

## 14. Implementation Constraints

The coding agent must:

1. Read all project specifications before implementation.
2. Follow the defined stack.
3. Use Astro as the primary framework.
4. Use Tailwind CSS as the primary styling solution.
5. Use pnpm exclusively.
6. Keep the application static and frontend-only.
7. Avoid unnecessary dependencies and abstractions.
8. Keep product data separate from presentation.
9. Avoid introducing out-of-scope functionality.
10. Ask for clarification before making significant architectural changes.

## 15. Technical Acceptance Criteria

The initial implementation is technically complete when:

- The application is built with Astro.
- TypeScript strict checking is enabled.
- Tailwind CSS is correctly integrated.
- pnpm is used for dependency management.
- The application generates static pages.
- Product and category routes are generated from local data.
- Catalog interactions work without a backend.
- Product images are stored locally.
- Catalog operations are independently testable.
- The production build succeeds.
- The generated site can be deployed to static hosting.
- No unnecessary UI framework or backend architecture has been introduced.