# Trevia Projects

## Current State
- Homepage ProjectsSection shows all 6 projects (3 completed + 3 ongoing)
- Clicking a project card does nothing (no detail view)
- Services grid uses two separate rows: 3 in first row (lg:grid-cols-3), 2 in second row via flex — on medium (md) screens the second row items don't fill nicely or are misaligned
- Footer logo uses `filter: brightness(0) invert(1) opacity(0.95)` (white inversion) — looks different from header logo which shows the natural color

## Requested Changes (Diff)

### Add
- Project detail modal/overlay: clicking any project card opens a full-detail panel showing image, title, type, location, status badge, year, area, description, and a "View All Projects" CTA button
- The detail modal works on both the homepage ProjectsSection and the /projects page

### Modify
- Homepage ProjectsSection: filter to show ONLY ongoing projects (status === "Ongoing"), update subtitle to "Ongoing Developments"
- Services grid: replace the split first-row/second-row approach with a single responsive grid that shows 3 cols on lg, 2 cols on md (not 1), and 1 col on mobile. This ensures all 5 cards display properly at medium screen sizes.
- Footer logo: remove the `filter: brightness(0) invert(1)` — use the same natural logo as the header (just use a white/light background or add a subtle white background box behind it if needed for visibility on the dark footer). Match header logo style: same `height: 56px`, `width: auto`, `objectFit: contain`, but without color inversion.

### Remove
- Completed projects from homepage section (show only ongoing)

## Implementation Plan
1. In `OurServicesSection`: replace the two-row layout (firstRow/secondRow) with a single unified grid: `grid-cols-1 md:grid-cols-2 lg:grid-cols-3`. The last odd card on lg can be centered via CSS.
2. In `ProjectsSection` (homepage): filter `PROJECTS` to only `status === "Ongoing"` before rendering. Update subtitle text.
3. Add a `selectedProject` state variable and a `ProjectDetailModal` component (dialog overlay). Both homepage cards and /projects page cards set the selected project and open the modal on click.
4. `ProjectDetailModal`: full-width overlay with image, title, type/location, status badge, year, area, and description. Close button (X) top-right. "View All Projects" button navigates to /projects.
5. Footer logo: remove the `filter` CSS property so the logo renders in its natural color. The dark background provides enough contrast.
