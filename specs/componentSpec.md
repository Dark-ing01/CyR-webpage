# COMPONENT-SPEC.md

## 1. Purpose

Define the reusable UI components for the clothing catalog.

Components should be simple, consistent, accessible, and aligned with the visual direction described in `BRAND-IDENTITY.md` and `LAYOUT-SPEC.md`.

Use Astro components by default. Add client-side JavaScript only when interaction is required.

## 2. Global Components

### Header
- Brand logo or wordmark.
- Main navigation: Home, Catalog, and available categories.
- Responsive navigation for mobile devices.
- Clear visual distinction between desktop and mobile layouts.

### Footer
- Brand identity and short description.
- Basic navigation links.
- Social media links only when real URLs are provided.
- No invented contact information or social accounts.

### PageHeading
- Page title and optional description.
- Consistent typography and spacing across pages.
- Optional breadcrumb navigation where appropriate.

## 3. Catalog Components

### ProductCard
Displays a product preview in the catalog.

Must include:
- Product image.
- Product name.
- Price.
- Optional category or relevant label.
- Link to the product detail page.

Requirements:
- Entire card should provide an intuitive navigation experience.
- Images must preserve their aspect ratio and avoid layout shifts.
- Consistent image presentation across the catalog.
- No cart, wishlist, or purchase controls.

### ProductGrid
- Displays products using a responsive grid.
- Four columns on large desktop screens, adapting to available space.
- Two columns on mobile.
- Consistent gaps and card dimensions.

### CatalogFilters
Provides catalog filtering controls.

Must support:
- Category selection.
- Minimum and maximum price.
- Clearing all active filters.

Requirements:
- Show active filter state.
- Adapt to a sidebar on desktop and a drawer or bottom sheet on mobile.
- Keep filtering behavior consistent across screen sizes.

### CatalogToolbar
- Displays the number of matching products.
- Provides sorting options: price ascending and descending.
- May include a search input if product search is implemented.

### EmptyState
Displayed when no products match the current filters.

Must include:
- A concise explanatory message.
- An action to clear filters and restore the catalog.

## 4. Product Detail Components

### ProductGallery
- Displays the main product image and additional images.
- Supports image navigation when multiple images exist.
- Responsive presentation, including horizontal/swipe navigation on mobile.
- Avoid unnecessary controls when only one image exists.

### ProductInformation
Displays the product's main information:
- Product name.
- Price.
- Description.
- Available attributes, such as colors, sizes, or materials, when provided.

Do not display attributes that are not available in the product data.

## 5. Shared UI Elements

### Button
Support a small set of consistent variants:
- Primary: main actions.
- Secondary: alternative actions.
- Text/Ghost: low-emphasis actions.

### Link
- Consistent typography and hover/focus states.
- Clear distinction between navigation links and actions.

### Badge
Used for optional product labels, such as "New" or "Featured", only when explicitly defined in the product data.

## 6. Design and Implementation Rules

- Follow the colors, typography, and visual direction in `BRAND-IDENTITY.md`.
- Follow page composition and responsive behavior in `LAYOUT-SPEC.md`.
- Use Tailwind CSS for styling.
- Prefer composition and small components over large components with many conditional branches.
- Avoid unnecessary abstractions and dependencies.
- All interactive elements must support keyboard navigation and visible focus states.
- Use semantic HTML and accessible labels.
- Do not invent product information or functionality.
- Do not introduce e-commerce features outside the project's defined scope.

## 7. Acceptance Criteria

- Components are reusable across the pages where appropriate.
- Components behave consistently on desktop, tablet, and mobile.
- Visual styling follows the brand identity.
- Interactive components work without requiring a backend.
- Components remain simple and easy to maintain.