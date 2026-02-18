---
name: frontend-task
description: "Frontend task guidelines for component creation, forms, cache management, i18n, and Playwright tests"
user-invocable: false
---

# Frontend Task Guidelines

## Component Creation and Styling
- **NEVER use ambiguous hex color values in components unless absolutely necessary**
  - Prefer updating your global CSS file to add custom colors that align with your component library conventions
  - Use CSS custom properties (CSS variables) for consistent theming
  - If a custom color cannot be added, default to Tailwind's built-in color names
  - Avoid inline hex values like `#FF5733` or `rgb(255, 87, 51)`
  - When adding colors, follow semantic CSS variable naming conventions (`--primary`, `--secondary`, `--muted`)
- **ALWAYS use the `cn()` utility for conditional class names**
  - Import `cn` from `@/lib/utils`
  - Use it to merge Tailwind classes conditionally: `className={cn("base-class", condition && "active-class")}`
  - This handles Tailwind class conflicts correctly using `tailwind-merge`

## Form Creation
- **ALWAYS use ShadCN and React Hook Form when creating forms**
  - Use your project's Form component from the UI component library
  - Use React Hook Form (`useForm` hook) for form state management and validation
  - Use Zod for schema validation in combination with React Hook Form
  - Follow the pattern established in existing forms
  - Never create forms without these libraries

## Frontend Cache Management (React Query / tRPC)
- ALWAYS ensure that mutations invalidate relevant queries or update the cache directly
- Use `utils.invalidate()` to refetch data after mutations:
```typescript
const utils = api.useUtils();
const mutation = api.router.mutation.useMutation({
  onSuccess: () => {
    utils.router.listQuery.invalidate();
  }
});
```
- For high-frequency interactions, consider optimistic updates or direct cache updates
- If the mutation returns the created/updated item, you can manually update the query cache:
```typescript
const mutation = api.router.create.useMutation({
  onSuccess: (newItem) => {
    utils.router.list.setData({ someId }, (old) => {
      return old ? [...old, newItem] : [newItem];
    });
  }
});
```
- Checklist for new features:
  - Identify all queries that display the data being modified
  - Add invalidation or cache updates for ALL of them in `onSuccess`
  - Verify UI updates without page refresh

## Internationalization (i18n)
- **ALWAYS use `useTranslation()` for user-facing strings** (when i18n is set up in the project)
  - Import from `react-i18next`
  - Never hardcode English strings in JSX
- **Add translation keys to the project's locale files**
  - Use semantic dot-notation: `section.key_name`
  - Choose the correct namespace for the feature area
- **Export route-level i18n configuration** as required by your framework
- **API errors should return translation keys** when the error message will be displayed to users

## Writing Playwright Tests for Frontend Features
- **ALWAYS write Playwright tests to verify functionality when implementing frontend features**
  - Create test files in `e2e/` directory following `*.spec.ts` pattern
  - Use `@playwright/test` for test framework
  - **ALWAYS prefer locating elements by id or data-testid attributes**
    - Use `getByTestId()` for `data-testid` attributes
    - Use `locator('#element-id')` for `id` attributes
    - Avoid `getByLabel()` and `getByText()` as they can be duplicated
  - Run tests with `npx playwright test` (or your project's test runner)
