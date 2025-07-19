# Rupertland Government Website Development Guide

## Project Overview
This is a fictional UK Government-style website for the "Principality of Rupertland" that follows exact GOV.UK design patterns and contains comprehensive government services.

## Development Process - Iterative Link Completion

Follow this process as a feedback loop to eliminate all dead links and make the site as realistic as possible:

### 1. Scan for Dead Links
- Use grep/search tools to find all `<a href="..."` links across all HTML files
- Identify which links point to pages that don't exist
- Prioritize links that appear multiple times across the site

### 2. Create Template System
- Use existing pages as templates to avoid rewriting common HTML structure
- Copy the header, footer, and navigation from existing pages
- Follow GOV.UK design patterns consistently
- Maintain the same CSS classes and semantic structure

### 3. Generate Content
- Create realistic, comprehensive content for each new page
- Follow government website content patterns
- Include practical information citizens would actually need
- Add cross-references and related links between pages

### 4. Deploy and Test
- Push changes to GitHub
- Deploy to Netlify
- Test the live site for any new broken links

### 5. Repeat Until Complete
- Continue this cycle until there are genuinely 0% dead links
- Each iteration should add substantial content and functionality
- Focus on the most commonly referenced links first

## Key Principles

### Content Quality
- All content should be realistic and useful
- Follow actual government website content patterns
- Include forms, processes, and practical information
- Add contact details, opening hours, and service descriptions

### Technical Standards
- Maintain exact GOV.UK styling and responsive design
- Use semantic HTML and proper accessibility features
- Keep consistent navigation across all pages
- Ensure all internal links work correctly

### Site Completeness
- Every link should lead to actual content, not placeholders
- Related pages should reference each other appropriately
- Footer links should all be functional
- Service pages should include complete workflows

## Testing Commands
- Use `grep -r "href=\"/" . --include="*.html"` to find all internal links
- Check netlify.toml for any remaining coming-soon redirects
- Verify all navigation menus point to existing pages

## Current Status
The site has 16+ comprehensive pages with full content and should have minimal dead links. Continue the scan-create-deploy cycle to achieve 100% link completion.