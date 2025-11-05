# Ground Truth Recovery Instructions

## Ground Source of Truth - Holiday Theme v1.0

**Commit:** `0cda0c8` - "Add holiday theme: Christmas lights, snowfall, red background"

**Date:** Friday, October 31, 2025, 1:01 PM

**Tag:** `GROUND-TRUTH-HOLIDAY-v1.0`

**Backup Branch:** `backup/ground-truth-holiday-v1.0`

---

## What This Version Contains

This is the foundational holiday theme with:
- ✓ Cherry Christmas red background (#DC143C crimson) on all pages
- ✓ 50 animated falling snowflakes (20 on mobile for performance)
- ✓ 40 twinkling Christmas light bulbs (20 on mobile)
- ✓ White text contrast styling on red background
- ✓ All effects integrated into `layout/theme.liquid`

### Files Included

```text
assets/custom.css              - Red background styling
assets/holiday-snow.css        - Snowfall animation
assets/holiday-lights.css      - Christmas lights styling
assets/holiday-lights.js       - Lights position controller
snippets/holiday-snow.liquid   - Snow snippet (50 snowflakes)
snippets/holiday-lights.liquid - Lights snippet (40 bulbs)
layout/theme.liquid            - Integration (lines 17-18, 151-152)
```

---

## How to Recover This Version

### Option 1: Using Git Tag (Recommended)
```bash
# View all tags
git tag -l

# Checkout the ground truth tag
git checkout GROUND-TRUTH-HOLIDAY-v1.0

# Create new branch from this point
git checkout -b my-new-branch
```

### Option 2: Using Backup Branch
```bash
# Checkout the backup branch
git checkout backup/ground-truth-holiday-v1.0

# Create new branch from this point
git checkout -b my-new-branch
```

### Option 3: Using Commit Hash
```bash
# Checkout by commit hash
git checkout 0cda0c8

# Create new branch from this point
git checkout -b my-new-branch
```

### Option 4: Reset Current Branch to Ground Truth
```bash
# WARNING: This will discard all uncommitted changes!
git reset --hard GROUND-TRUTH-HOLIDAY-v1.0
```

---

## Emergency Recovery (If Tag is Lost)

If tags are somehow lost, recover from GitHub:

1. Go to: https://github.com/The-Prod-Father-Pt-1/spirited-hive
2. Click "Tags" or find branch `backup/ground-truth-holiday-v1.0`
3. Download ZIP or clone fresh:
   ```bash
   git clone https://github.com/The-Prod-Father-Pt-1/spirited-hive.git
   cd spirited-hive
   git checkout GROUND-TRUTH-HOLIDAY-v1.0
   ```

---

## Verify You're on Ground Truth

After checking out, verify with:
```bash
# Check current commit
git log --oneline | head -1
# Should show: 0cda0c8 Add holiday theme: Christmas lights, snowfall, red background

# Check for holiday files
ls -la snippets/ | grep holiday
ls -la assets/ | grep holiday

# Should see:
# - holiday-lights.liquid
# - holiday-snow.liquid
# - holiday-lights.css
# - holiday-lights.js
# - holiday-snow.css

# Check custom.css has red background
head -20 assets/custom.css
# Should see: background-color: #DC143C !important;
```

---

## Push Ground Truth to Shopify

Once on ground truth version:
```bash
# Push to "Hive for the Holidays" theme
shopify theme push --theme="Hive for the Holidays"

# Or push to a new theme
shopify theme push --unpublished --store spirited-hive.myshopify.com
# Then enter theme name when prompted
```

---

## Notes

- **Tag is permanent**: `GROUND-TRUTH-HOLIDAY-v1.0` will always point to commit `0cda0c8`
- **Backup branch**: `backup/ground-truth-holiday-v1.0` is a protected branch
- **Remote backup**: Both tag and branch are pushed to GitHub
- **Triple redundancy**: Tag + Branch + Commit hash all lead to same place

---

## Created

- **When:** Sunday, November 3, 2025
- **Why:** To ensure we can always return to the working Friday 1:01 PM holiday theme
- **By:** Claude Code with user approval
