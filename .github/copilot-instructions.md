# AI Coding Guidelines for Academic Portfolio Project

## Architecture Overview
This is a dynamic React portfolio website that fetches all content from Google Sheets. The app automatically hides empty sections and combines research publications into a unified display.

**Key Data Flow:**
- Google Sheets (18+ sheets) → CSV export → PapaParse → React state → Filtered sections → Component rendering
- Reference: `src/config/sheets.ts` for sheet IDs, `src/hooks/usePortfolioData.ts` for fetching, `src/utils/fetchData.ts` for CSV parsing

## Core Patterns
- **Section Filtering**: Use `rows.filter(r => Object.values(r).some(v => v))` to hide empty rows/sections
- **Link Detection**: Use `isValidUrl()` helper to convert URLs into clickable buttons with ExternalLink icons
- **Responsive Layouts**: Desktop tables, mobile cards; reference `src/components/Section.tsx` and `ResearchPublications.tsx`
- **Animation Framework**: Framer Motion for staggered entrance animations; viewport-triggered with `whileInView`

## UI Conventions
- **Glassmorphism**: Use `glass-card` class for frosted glass effects with backdrop blur
- **Gradient Themes**: Sky blue/cyan/blue palette; CSS variables in `src/index.css` for consistency
- **Component Structure**: Hero shows stats, dynamic Sections from sheets, combined ResearchPublications, Contact form
- **Publication Stats**: Count rows from journal/conference/books sheets for Hero badges

## Development Workflow
- **Local Dev**: `npm run dev` (Vite dev server)
- **Build**: `npm run build` (TypeScript compilation + Vite build)
- **Deploy**: Vercel with serverless API; set `RESEND_API_KEY` env var for email
- **Sheets Setup**: Make all Google Sheets "Anyone with the link can view"; update IDs in `sheets.ts`

## Email Integration
- Contact form posts to `/api/send-email.ts` (Vercel serverless)
- Fallback: FormSubmit API (requires domain verification after deploy)
- Reference: `EMAIL_FIX_GUIDE.md` for troubleshooting

## Key Files to Reference
- `src/App.tsx`: Main layout, section filtering, data passing
- `src/components/ResearchPublications.tsx`: Combined publications display with subsections
- `src/config/sheets.ts`: Sheet IDs and section titles mapping
- `src/index.css`: CSS variables, gradients, glassmorphism styles