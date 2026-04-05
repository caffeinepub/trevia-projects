# Trevia Projects

## Current State
Project cards on both the Home page (ongoing projects section) and the /projects page currently open a modal popup (ProjectDetailModal) when clicked. The service detail pages use a dedicated full page route (/service-detail) with a global `selectedService` variable pattern.

## Requested Changes (Diff)

### Add
- `let selectedProject` global variable (like `selectedService`) to hold the clicked project
- `ProjectDetailPage` component — a full dedicated page (like ServiceDetailPage) showing project details: hero image, title, type, location, status, year, area, description, and a WhatsApp contact button
- `/project-detail` route pointing to `ProjectDetailPage`
- Route registered in `routeTree`

### Modify
- Card click handlers in `ProjectsSection` (Home page) — instead of `setSelectedProject(project)`, set `selectedProject = project` and `navigate({ to: '/project-detail' })`
- Card click handlers in `ProjectsPageComponent` (/projects page) — same change
- Remove the `ProjectDetailModal` component entirely (no longer needed)
- Remove `selectedProject` useState and modal rendering from both sections

### Remove
- `ProjectDetailModal` component
- All modal-related state (`selectedProject` useState in both ProjectsSection and ProjectsPageComponent)
- Modal render JSX in both sections

## Implementation Plan
1. Add `let selectedProject: (typeof PROJECTS)[number] | null = null;` near the other global state vars (~line 102)
2. Replace `ProjectDetailModal` with a `ProjectDetailPage` function component
   - Full page layout matching ServiceDetailPage style
   - Header at top, back button (→ Back to Projects)
   - Hero image with status badge overlay
   - Project title, type, location, year, area
   - Full description section
   - Key highlights section (area, type, location, year)
   - WhatsApp contact button (number: 9000564939, pre-filled message with project name)
   - Footer at bottom
   - `useEffect` scroll to top on mount
3. Update both card click handlers to: `selectedProject = project; navigate({ to: '/project-detail' });`
4. Remove selectedProject useState and modal JSX from both components
5. Add `projectDetailRoute` and register in routeTree
