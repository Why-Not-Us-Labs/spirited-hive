# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

This is a Shopify theme called **Flow** (version 39.8.0) developed by Eight Themes. It's a production e-commerce theme built using Shopify's Liquid templating language.

## Architecture

### Core Directory Structure

- **layout/** - Main theme layout templates
  - `theme.liquid` - Primary layout file that includes header, footer, and page content
  - `password.liquid` - Password-protected store layout
  - GemPages integration layouts (`theme.gempages.*`)

- **sections/** - Shopify sections (modular, reusable content blocks)
  - Homepage sections: `slideshow.liquid`, `featured-product.liquid`, `featured-collection.liquid`, etc.
  - Template sections: `collection-header.liquid`, `blog-posts.liquid`
  - Customer account sections: `customer-*.liquid`
  - Specialized sections: `countdown.liquid`, `events-calendar.liquid`, `collage.liquid`

- **snippets/** - Reusable code components
  - Product components: `card-color-swatch.liquid`, `badge.liquid`
  - UI components: `breadcrumb.liquid`, `back-to-top-button.liquid`, `cart-drawer.liquid`
  - Form inputs: `form-input.liquid`, `form-input--dropdown.liquid`, etc.
  - Utility snippets: `css-variables.liquid`, `button-color-overrides.liquid`

- **templates/** - Page templates
  - JSON-based templates for products, collections, pages, blog, etc.
  - Multiple template variations using suffixes (e.g., `product.basic.json`, `product.merch.json`)
  - GemPages builder templates (`*.gem-*-template.*`)

- **assets/** - Static assets (CSS, JavaScript, images)
  - Theme scripts use ES6 modules with `.js` extension
  - Minified CSS files with `.min.css` pattern
  - Component-based architecture: `component-*.js` files

- **config/** - Theme settings and configuration
  - `settings_schema.json` - Defines all theme customization options in the Shopify admin

- **locales/** - Internationalization files
  - Translation JSON files for multiple languages (bg, cs, da, de, etc.)

### Key Patterns

**Liquid Architecture:**
- Uses Liquid `{% render %}` for including snippets
- `{% sections %}` for section groups (header-group, footer-group, overlay-group)
- Extensive use of `{% liquid %}` blocks for multi-line logic
- Settings accessed via `settings.*` (e.g., `settings.cart_type`, `settings.color_primary`)

**JavaScript Architecture:**
- Web Components pattern using `<safe-load-scripts>` for lazy loading
- Custom element registry at `window.wetheme.webcomponentRegistry`
- Event-driven architecture using `eventBus.js`
- Module-based loading with `data-flow-load-key` attributes

**Color Schemes:**
- Four color schemes: Default (white), First (light), Second (accent), Third (dark)
- Applied via `color-scheme--{{ section.settings.color_scheme }}` classes
- CSS variables defined in `css-variables.liquid` snippet

**Product Variants:**
- Supports three variant display styles: dropdowns, buttons, swatches
- Combined listings support (products linking to other products via variant options)
- Color swatches can use images, metafield values, or file-based swatches
- Variant images driven by `settings.show_variant_image_for_options`

**Cart System:**
- Two cart types: drawer (slide-out) and page
- AJAX-based cart updates using `routes.cart_add_url`, `routes.cart_change_url`
- Cart recommendations powered by Shopify's product recommendations API

**GemPages Integration:**
- Third-party page builder integration
- Templates with `gem-*-template` pattern
- Special handling in layout files for GemPages scripts

## Development Commands

This is a Shopify theme, so development requires the Shopify CLI:

```bash
# Start local development server (requires Shopify CLI)
shopify theme dev

# Deploy to a Shopify store
shopify theme push

# Pull theme files from store
shopify theme pull
```

Note: This repository does not include package.json or build tools. Theme assets are pre-compiled.

**Important:** See `LOCAL-FIRST-WORKFLOW.md` for the complete local-first development workflow, including:
- Template JSON structure for hiding/showing sections
- Asset management patterns
- Git workflow with Shopify push/pull
- Rollback strategies

## Settings Schema

The `config/settings_schema.json` defines extensive theme settings:
- Colors and typography
- Cart and product card configurations
- Animations and spacing
- Popup modals (newsletter, age verification)
- Social media links
- Search and navigation settings

When modifying theme settings, update this schema to expose controls in Shopify admin.

## Working with Sections

Sections are JSON files (in templates) or Liquid files (in sections/) that define:
- Schema for customization options
- Blocks for nested content
- Presets for quick insertion

Example section structure:
```liquid
{% schema %}
{
  "name": "Section Name",
  "settings": [...],
  "blocks": [...],
  "presets": [...]
}
{% endschema %}
```

## Translation System

All user-facing strings use the `{{ 't' }}` filter:
```liquid
{{ 'products.product.add_to_cart' | t }}
```

Translations stored in `locales/*.json` files with nested key structure.

## Important Metafields

- `shop.metafields.gempages` - GemPages configuration
- `value.swatch.image` and `value.swatch.color` - Variant swatch metafields
- Product metafields for custom badges and variants

## Theme Features

- Predictive search with AJAX results
- Quick shop modal for products
- Gift wrapping product integration
- Product comparison
- Store locator
- Events calendar
- Countdown timers
- Age verification popup
- Newsletter popup with customizable triggers
- Back-to-top button
- Breadcrumbs (optional)
- Animations (optional, with Ken Burns effect)
- Product recommendations in cart

---

## Project Workflow & Standards

### Time Tracking (REQUIRED)

**Client:** Spirited Hive requires accurate time tracking for all work.

**Location:** `time-spent/time-log.md`

**Process:**
1. **Clock in** when starting work - add new entry with start time
2. **Clock out** when stopping work - add end time and calculate minutes
3. **Be honest** - no fudging numbers, no overshooting
4. Track actual work time, not time away from keyboard
5. Include brief description of work done

**Format:**
```
YYYY-MM-DD | HH:MM - HH:MM | XXX min | Brief description
```

**Important:** This file is tracked in git and syncs across computers for consistent logging.

### Meeting Documentation

**Location:** `docs/YYYY-MM-DD-meeting-name/`

**Required Files:**
- `meeting-notes.md` - Structured notes from meeting
- `transcript.md` - Full transcript (if available)
- `video.mp4` - Recording of meeting
- `action-items.md` - Extracted action items with assignments

**Process:**
1. After each client meeting, create dated folder
2. Add video, transcript, and initial notes
3. Process materials to identify requirements
4. Extract clear action items with team assignments
5. Review action items align with project standards

**Templates:** Use templates in `docs/_templates/` for consistency

### Team Structure

This project uses a specialized Shopify development team:

- **Product Manager** - Requirements gathering, prioritization, client communication
- **Designer** - UI/UX design, maintaining brand consistency
- **Frontend Engineer** - Implementation, component development
- **Shopify Architect** - Theme architecture, Shopify best practices, admin configuration

### Subagents (Multi-Agent Collaboration)

The `subagents/` folder contains detailed role definitions for specialized agents. See `subagents/README.md` for the complete team workflow.

**Available Agents:**
| Agent | Primary Role | When to Use |
|-------|--------------|-------------|
| Product Manager | Requirements & PRDs | Processing client meetings, writing user stories |
| Designer | Visual design | Creating mockups, ensuring brand consistency |
| Frontend Expert | Liquid/JS/CSS implementation | Building sections, implementing designs |
| Shopify Architect | Technical decisions | Architecture, performance, code review |
| QA Engineer | Testing & validation | Test plans, cross-device testing, sign-off |
| DevOps Specialist | Deployment | Git workflow, theme push, rollback |

**Typical Flow:** PM → Designer → Frontend Expert → Architect (review) → QA → DevOps

### Quality Standards (NON-NEGOTIABLE)

1. **Never cut corners** - Quality over speed, but build efficiently
2. **Dual configurability** - Everything must be adjustable from:
   - Claude Code / codebase
   - Shopify admin (for non-technical users)
3. **Brand consistency** - Always maintain:
   - Existing fonts
   - Color schemes
   - Design patterns
   - Never go off-rails with styling
4. **Complete features** - Don't mark as done until:
   - Fully functional
   - Tested thoroughly
   - Documented in code
   - Configurable from admin
5. **Shopify best practices** - Follow official guidelines for:
   - Performance
   - Accessibility
   - Mobile responsiveness
   - SEO

### Section Development Standards

When creating or modifying sections:

1. **Schema settings** - Always expose relevant controls in section schema
2. **Block flexibility** - Use blocks for repeatable content
3. **Color scheme support** - Support all four theme color schemes
4. **Responsive design** - Test mobile, tablet, desktop
5. **Admin preview** - Ensure section editor shows accurate preview
6. **Default values** - Provide sensible defaults in schema
7. **Documentation** - Comment complex logic in Liquid

### Before Pushing Code

Checklist for every commit:
- [ ] Code is fully functional
- [ ] Settings exposed in Shopify admin where appropriate
- [ ] Tested on mobile and desktop
- [ ] Follows existing code patterns
- [ ] Maintains brand consistency (fonts, colors)
- [ ] No console errors
- [ ] Git commit message is descriptive
- [ ] Time log updated with work done

### Shopify CLI Integration

The project is connected to the Spirited Hive Shopify store.

**Development workflow:**
```bash
# Start local development with live preview
shopify theme dev

# Push changes to theme
shopify theme push

# Pull latest from store
shopify theme pull
```

**Important:** Always test in development theme before pushing to live store.

---

## Holiday Campaign Checkpoints

The holiday campaign has multiple checkpoints for safe restoration. Full documentation in `docs/CHECKPOINT-GROUND-TRUTH-v*.md`.

### Current Checkpoint: v6 (Christmas Lights Fixed)
- **Tag:** `checkpoint-v6-lights-fixed`
- **Commit:** `67d2fe6`
- **Status:** ✅ PERFECT
- **Restore:** `git checkout checkpoint-v6-lights-fixed && shopify theme push --theme="Hive for the Holidays"`

### Checkpoint History
| Version | Tag | Key Features |
|---------|-----|--------------|
| v6 | `checkpoint-v6-lights-fixed` | Christmas lights positioned correctly (inside header.liquid) |
| v5 | `checkpoint-v5-auto-scroll-complete` | Auto-scrolling reviews complete |
| v4 | `checkpoint-v4-navigation-complete` | All navigation visible, SVG icons working |
| v3 | `checkpoint-v3-product-reviews-complete` | Video carousel & character reviews |

### Critical: Christmas Lights Implementation
Lights MUST be rendered in `sections/header.liquid` (line 886) after `</nav>` with `position: relative`. NEVER use `position: fixed` or render in `layout/theme.liquid`. See `docs/CHECKPOINT-GROUND-TRUTH-v6.md` for details.

---

## Commands That Require Manual Terminal Execution

**⚠️ IMPORTANT:** Some Shopify CLI commands require interactive prompts that cannot be automated through Claude Code. These MUST be run directly in your terminal by the user.

### Creating a New Theme in Shopify Theme Library

**Command:**
```bash
shopify theme push --unpublished --store spirited-hive.myshopify.com
```

**What happens:**
1. CLI will prompt: "Name of the new theme:"
2. Enter your theme name (e.g., "Why Not Us Labs - Spirits for The Holidays")
3. Press Enter
4. Theme uploads to Shopify (takes 1-2 minutes)
5. Returns preview URL and theme editor link

**Why this is needed:**
- To create a brand new theme variation in the Shopify theme library
- To test major changes without affecting current live/development themes
- To create campaign-specific themes (like holiday campaigns)

**After completion:**
- New theme appears in Shopify Admin → Online Store → Themes
- Theme is unpublished (safe to customize before going live)
- You get a preview URL to share with team/clients

### Authentication Commands

**Command:**
```bash
shopify auth login
```

**What happens:**
1. Generates a device code (e.g., VJVR-SVSK)
2. Opens browser to https://accounts.shopify.com/activate-with-code
3. User enters code and logs in
4. CLI confirms authentication

**When needed:**
- First time setting up Shopify CLI on new computer
- After authentication expires
- When switching between Shopify stores

### Other Interactive Commands

These may also require manual execution:
- `shopify theme list` - Interactive selection of themes
- `shopify theme pull` - May prompt for theme selection
- `shopify theme delete` - Confirmation prompts

**Best Practice:**
When Claude indicates a command needs to be run manually, copy the exact command provided and run it in your terminal. Claude will provide clear instructions on what inputs to provide at each prompt.

---

## Creating New Checkpoints

When major features are completed and tested:

1. Create checkpoint document: `docs/CHECKPOINT-GROUND-TRUTH-v[X].md`
2. Create git tag: `git tag checkpoint-v[X]-brief-description`
3. Include in documentation:
   - Commit hash and branch
   - Complete feature list
   - Restoration instructions
   - Verification checklist
   - What changed since previous checkpoint
4. Update the "Holiday Campaign Checkpoints" section above
5. Commit documentation to git

---

## Holiday Campaign Architecture

### Holiday Effects Files

**Snippets (HTML/Liquid):**
- `snippets/holiday-lights.liquid` - Christmas lights HTML structure
- `snippets/holiday-snow.liquid` - Snowfall effect particles

**Assets (CSS/JS):**
- `assets/holiday-lights.css` - Lights positioning and styling
- `assets/holiday-lights.js` - Lights animation/blinking logic
- `assets/holiday-snow.css` - Snowfall animation styles

### Holiday Sections

Located in `sections/`:
- `holiday-hero.liquid` - Holiday-themed hero banner
- `holiday-video-carousel.liquid` - Character video carousel (Santa, Rudolph, etc.)
- `holiday-reviews.liquid` - Fake reviews from holiday characters (auto-scrolling)

### Holiday Theme Configuration

**Active Theme:** "Hive for the Holidays" (Theme ID: 153001951460)

**Preview URL:**
```
https://spirited-hive.myshopify.com?preview_theme_id=153001951460
```

**Holiday Colors:**
- Primary background: Cherry red `#DC143C`
- Card backgrounds: Christmas green (on mobile: white for readability)
- Text: White on dark backgrounds, black on light backgrounds

### Template Overrides

Holiday sections are configured in:
- `templates/index.json` - Homepage with holiday hero, effects
- `templates/product.json` - Product pages with video carousel, reviews
- `templates/page.holiday-landing.json` - Dedicated holiday landing page
