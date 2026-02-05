# Current Context - Spirited Hive

**Last Updated:** 2026-02-04

## Active Work Streams

| Stream | Status | Theme ID | Notes |
|--------|--------|----------|-------|
| Vodka Iced Tea Launch | Phase 1 Complete | #156222554340 | March 1st launch, Feb 20 presentation |
| Holiday Campaign | On Hold | #153001951460 | Checkpointed at v6 |

## Quick Status

### Vodka Iced Tea Launch (Primary)
- **Theme:** `spirited-hive-vodka-iced-tea-launch` (#156222554340)
- **Preview:** https://spirited-hive.myshopify.com?preview_theme_id=156222554340
- **Based on:** Production theme (SH25 - Flow - Updated #146073616612)

**Phase 1 Completed:**
- [x] Announcement bar: "NEW: Vodka Iced Tea + Honey — It's Tea Time" (orange #E87A2E)
- [x] Hero headline: "IT'S TEA TIME" with "Shop Vodka Iced Tea" CTA
- [x] Navigation: Auto-highlight for items containing "Tea" or "NEW"
- [x] Product page: Using existing template (no changes needed)

**Pending (Admin tasks, not code):**
- [ ] Add Vodka Iced Tea product in Shopify Admin
- [ ] Add menu item to main-menu navigation
- [ ] Update Klaviyo popup with new flavor option
- [ ] Swap hero image when can renders arrive from Chris

### Holiday Campaign (On Hold)
- **Theme:** "Hive for the Holidays" (#153001951460)
- **Checkpoint:** v6 (lights fixed)
- **Tag:** `checkpoint-v6-lights-fixed`

## Key Files Modified This Session

| File | Change |
|------|--------|
| `sections/header-group.json` | Announcement bar text + colors |
| `templates/index.json` | Hero headline "IT'S TEA TIME" + CTA button |
| `snippets/nav--main.liquid` | Auto-highlight logic + CSS for "Tea"/"NEW" items |

## Technical Notes

### Theme Architecture
- Production theme uses different file naming than holiday branch
- `sections/header-group.json` (not `group-header.json`)
- `image-with-text-slideshow` section type (not `gs-hero`)

### Navigation Highlight
Added to `snippets/nav--main.liquid`:
- Liquid logic checks `link.title | downcase` for "tea" or "new"
- Adds `.nav-highlight` class to matching items
- CSS: orange background (#E87A2E), white text, rounded corners

### Popup/Enrollment
- Managed through Klaviyo (external platform), not theme code
- Klaviyo block enabled in `config/settings_data.json`
- Theme's built-in popup is disabled

## Pending Questions
- None currently

## Next Session Priorities
1. Add product to Shopify Admin when can renders arrive
2. Add navigation menu item
3. Consider Phase 2 features (dedicated landing page, video content)

## Important IDs & Links

| Resource | ID/URL |
|----------|--------|
| Vodka Iced Tea Theme | #156222554340 |
| Production Theme | #146073616612 |
| Holiday Theme | #153001951460 |
| Preview URL | https://spirited-hive.myshopify.com?preview_theme_id=156222554340 |
| Theme Editor | https://spirited-hive.myshopify.com/admin/themes/156222554340/editor |
