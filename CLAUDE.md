# Rupertland Government Website Development Guide

## Project Overview
This is a fictional UK Government-style website for the "Principality of Rupertland" that follows exact GOV.UK design patterns and contains comprehensive government services.

**Architecture:** Single-Page Application (SPA) using JavaScript navigation for maximum efficiency and maintainability.

## Current Architecture - Single-Page Application (SPA)

### Overview
The site has been completely refactored from 50+ static HTML files to a single-page application (`index-spa.html`) for improved efficiency and maintainability. This approach eliminates code duplication and provides instant navigation.

### Key Files
- **`index-spa.html`** - Main SPA file containing all pages as sections
- **`netlify.toml`** - Configuration with catch-all redirect to SPA
- **`styles.css`** - External CSS file for GOV.UK styling
- **No legacy files** - All content migrated to SPA architecture

### Complete SPA Structure
```
index-spa.html
├── Single <head> with CSS and metadata
├── Shared <header> with navigation
├── Page sections with id="page-name" class="page"
│   ├── Home page (active by default)
│   ├── About Rupertland (government overview)
│   ├── Government Services (service directory)
│   ├── Digital ID & Citizen Portal (authentication hub)
│   ├── Identity Card Application (form workflow)
│   ├── Tax Calculator (interactive calculator)
│   ├── News & Announcements (government updates)
│   ├── Contact Government (contact directory)
│   ├── Immigration Services (comprehensive immigration info)
│   ├── Legal Aid (legal assistance information)
│   ├── Royal Family (constitutional monarchy details)
│   ├── Parliament (legislative process, MPs, proceedings)
│   ├── Government Transparency (open data, FOI, accountability)
│   ├── Ministers & Officials (cabinet, senior officials)
│   ├── Laws & Regulations (legal framework, legislation)
│   ├── Government Departments (ministries, agencies, structure)
│   ├── Constitution (fundamental law, rights, amendments)
│   └── Data Protection (privacy rights, data laws)
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

### 1. Adding New Pages (Recursive System Approach)
```bash
# Step 1: Identify missing pages using recursive analysis
grep -o "showPage('[^']*')" index-spa.html | sort | uniq > referenced_pages.txt
grep -o 'id="[^"]*" class="page"' index-spa.html | grep -o 'id="[^"]*"' | sed 's/id="//;s/"//' > existing_pages.txt
diff referenced_pages.txt existing_pages.txt  # Shows missing pages

# Step 2: Prioritize by reference frequency
grep -o "showPage('[^']*')" index-spa.html | sort | uniq -c | sort -nr  # Most referenced first
```

```javascript
// Step 3: Add new page section in HTML
<div id="new-page" class="page">
    <div class="govuk-breadcrumbs"><!-- Breadcrumbs --></div>
    <main class="govuk-main-wrapper">
        <!-- Page content with proper GOV.UK styling -->
    </main>
</div>

// Step 4: Update page titles in JavaScript
const titles = {
    'new-page': 'New Page Title - GOV.RP',
    // ... existing titles
};

// Step 5: Add navigation links throughout SPA
<a onclick="showPage('new-page')" class="govuk-link nav-link">New Page</a>
```

### 2. Content Migration Process
```bash
# Extract content from legacy HTML files
# 1. Read legacy file to understand structure and content
# 2. Extract main content (excluding header/footer/navigation)
# 3. Convert to SPA format with proper breadcrumbs
# 4. Update all internal links to use showPage() navigation
# 5. Add page to titles object
# 6. Test navigation thoroughly
# 7. Delete legacy file only after successful migration
```

### 3. Testing Navigation Completeness
```bash
# Check all showPage references (what's being called)
grep -o "showPage('[^']*')" index-spa.html | sort | uniq

# Check existing page definitions (what exists)
grep -o "id=\"[^\"]*\" class=\"page\"" index-spa.html | sed 's/id="//;s/" class="page"//'

# Find missing pages - any references without definitions
comm -23 <(grep -o "showPage('[^']*')" index-spa.html | sed "s/showPage('//;s/')//" | sort | uniq) <(grep -o 'id="[^"]*" class="page"' index-spa.html | sed 's/id="//;s/" class="page"//' | sort)

# Check for dead links (should return empty if all good)
# Above command shows pages that are referenced but don't exist
```

### 4. Form Development Standards
- Use standardized form classes matching ofcat patterns
- Include proper validation and accessibility attributes  
- Add JavaScript handlers for client-side processing
- Display success/error messages with proper styling
- Ensure forms work without page reloads (SPA-compatible)

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

## Content Migration History

### Phase 1: Initial SPA Architecture (July 2025)
- Converted 16 core pages from static HTML to SPA format
- Implemented JavaScript navigation with browser history support
- Added working forms (tax calculator, ID application, contact)
- Established GOV.UK design compliance

### Phase 2: Government Content Migration (July 2025)
- **Systematic content extraction** from 6 legacy HTML files based on reference frequency
- **Priority-based migration:** parliament (5 refs) → transparency (2 refs) → ministers (2 refs) → laws-regulations (3 refs) → departments (3 refs) → constitution (1 ref)
- **Content preservation:** All legislative, governmental, and constitutional information migrated
- **Cross-reference optimization:** Updated all internal links to use SPA navigation
- **Code reduction:** Eliminated 2,852 lines of duplicate HTML code

### Migration Achievements
- ✅ **Zero legacy files** - All content successfully migrated to SPA
- ✅ **Complete government coverage** - Parliament, ministries, laws, constitution all included
- ✅ **Systematic approach** - Used recursive link analysis to prioritize content migration
- ✅ **Content quality** - Maintained full detail and accuracy during migration

## Current Status - Production Ready

### ✅ **Complete SPA Architecture**
- **17 comprehensive pages** with full government content
- **JavaScript navigation system** with browser history support  
- **Zero code duplication** - shared header, footer, navigation
- **Instant navigation** - no page reloads required
- **Form workflows** comply with ofcat standards
- **GOV.UK design compliance** maintained throughout

### 📋 **Core Government Pages Included:**
**Citizen Services:**
- Home, About Rupertland, Government Services
- Digital ID & Citizen Portal, Identity Card Application  
- Tax Calculator, Immigration Services, Legal Aid

**Government Structure:**
- Parliament (MPs, legislative process, parliamentary proceedings)
- Ministers & Officials (cabinet members, senior officials, contact info)
- Government Departments (all ministries, agencies, organizational structure)
- Royal Family (constitutional monarchy, Prince Rupert biography)

**Legal Framework:**
- Constitution (fundamental law, rights, amendment process)
- Laws & Regulations (complete legal framework, legislation categories)
- Data Protection (privacy rights, data protection laws)
- Government Transparency (open data, FOI, accountability measures)

**Communication:**
- News & Announcements, Contact Government

### 🔗 **Navigation Status:**
- **Core government pages:** ✅ Complete with full content
- **Legislative content:** ✅ Complete (parliament, laws, constitution)
- **Administrative content:** ✅ Complete (ministers, departments, transparency)
- **Citizen services:** ✅ Complete (digital ID, immigration, legal aid)
- **Remaining:** Some service detail pages and footer pages (privacy, terms, cookies)

### 🎯 **Next Development Priorities:**
1. **Service detail pages** - citizenship, business registration, property registry
2. **Footer pages** - privacy policy, terms of service, cookies, accessibility
3. **Communication pages** - newsletter signup, social media, RSS feeds
4. **Additional services** - based on recursive analysis of remaining broken links

### 📊 **Technical Metrics:**
- **File count reduction:** 50+ HTML files → 1 SPA file
- **Code reduction:** ~20,000 lines → ~3,200 lines (84% reduction)
- **Load time improvement:** Multiple HTTP requests → Single page load
- **Maintenance improvement:** Multiple files to update → Single source of truth