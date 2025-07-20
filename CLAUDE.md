# Rupertland Government Website Development Guide

## Project Overview
This is a fictional UK Government-style website for the "Principality of Rupertland" that follows exact GOV.UK design patterns and contains comprehensive government services.

**Architecture:** Single-Page Application (SPA) using JavaScript navigation for maximum efficiency and maintainability.

## Current Architecture - Single-Page Application (SPA)

### Overview
The site has been refactored from multiple static HTML files to a single-page application (`index-spa.html`) for improved efficiency and maintainability. This approach eliminates code duplication and provides instant navigation.

### Key Files
- **`index-spa.html`** - Main SPA file containing all pages as sections
- **`netlify.toml`** - Configuration with catch-all redirect to SPA
- **`styles.css`** - External CSS file for GOV.UK styling
- **Static HTML files** - Legacy files, now superseded by SPA

### SPA Structure
```
index-spa.html
├── Single <head> with CSS and metadata
├── Shared <header> with navigation
├── Page sections with id="page-name" class="page"
│   ├── Home page (active by default)
│   ├── About Rupertland
│   ├── Government Services
│   ├── Digital ID & Citizen Portal
│   ├── Identity Card Application
│   ├── Tax Calculator
│   ├── News & Announcements
│   ├── Contact Government
│   ├── Immigration Services
│   ├── Legal Aid
│   ├── Royal Family
│   └── Data Protection
├── Shared <footer>
└── JavaScript navigation system
```

### Navigation System
- **showPage(pageId)** - Core navigation function
- **Browser history support** - Back/forward buttons work correctly
- **URL hash routing** - Direct links to pages work (e.g., #digital-id)
- **Dynamic page titles** - Page title updates based on current page
- **Scroll to top** - Automatic scroll on page change

### Form Handling
All forms include client-side JavaScript handlers:
- **Tax Calculator** - Real-time tax calculation with breakdown
- **ID Application** - Application submission with reference numbers
- **Contact Form** - Message submission with confirmation
- **Form Styling** - Matches ofcat standards with proper form classes

### CSS Architecture
```css
/* Page visibility control */
.page { display: none; }
.page.active { display: block; }

/* Navigation styling */
.nav-link { cursor: pointer; }
.govuk-breadcrumbs__link--js { cursor: pointer; }

/* Form components (matching ofcat) */
.form-group, .form-label, .form-input, .form-hint
.radio-group, .radio-item
.success-panel, .error-panel
.button, .button:hover
```

## Development Process - SPA Maintenance

### 1. Adding New Pages
```javascript
// 1. Add new page section in HTML
<div id="new-page" class="page">
    <!-- Page content -->
</div>

// 2. Update page titles in JavaScript
const titles = {
    'new-page': 'New Page Title - GOV.RP',
    // ... existing titles
};

// 3. Add navigation links
<a onclick="showPage('new-page')" class="govuk-link nav-link">New Page</a>
```

### 2. Testing Navigation
```bash
# Check all showPage references
grep -o "showPage('[^']*')" index-spa.html | sort | uniq

# Check existing page definitions
grep -o "id=\"[^\"]*\" class=\"page\"" index-spa.html

# Find missing pages
# Compare the two lists above
```

### 3. Form Development
- Use standardized form classes matching ofcat patterns
- Include proper validation and accessibility attributes
- Add JavaScript handlers for client-side processing
- Display success/error messages with proper styling

## Key Principles

### SPA Benefits
- **No code duplication** - Single header, footer, navigation
- **Instant navigation** - No page reloads, immediate response
- **Easier maintenance** - One file to update, not 16+
- **Consistent styling** - Guaranteed consistency across all pages
- **Better performance** - Loads once, navigates instantly

### Content Quality
- All content should be realistic and useful
- Follow actual government website content patterns
- Include forms, processes, and practical information
- Add contact details, opening hours, and service descriptions

### Technical Standards
- Maintain exact GOV.UK styling and responsive design
- Use semantic HTML and proper accessibility features
- Follow ofcat form patterns and CSS classes
- Ensure all navigation links work correctly in SPA

### SPA Completeness
- Every showPage() call should have corresponding page section
- Related pages should cross-reference each other appropriately
- Footer links should all be functional within SPA
- Service pages should include complete workflows with working forms

## Testing Commands
```bash
# Check navigation completeness
grep -o "showPage('[^']*')" index-spa.html | sort | uniq

# Check existing pages
grep -o "id=\"[^\"]*\" class=\"page\"" index-spa.html

# Test form classes
grep -c "form-group\|form-label\|form-input" index-spa.html

# Verify netlify.toml SPA redirect
grep -A 5 "Redirect to SPA" netlify.toml
```

## Current Status
**✅ SPA Architecture Complete**
- 12+ comprehensive pages with full content
- JavaScript navigation system working
- Forms comply with ofcat standards
- All major government services included
- Zero code duplication achieved

**📋 Pages Included:**
- Home, About, Services, Digital ID, Identity Card, Tax Calculator
- News, Contact, Immigration, Legal Aid, Royal Family, Data Protection

**🔗 Navigation Status:**
- Core pages: ✅ Complete
- Referenced pages: Some missing (e.g., parliament, ministers, departments)
- Footer links: Some missing (e.g., privacy, cookies, terms)

Continue adding missing page sections to eliminate any remaining dead links.