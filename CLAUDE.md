# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

"Old Student Card" is a commemorative digital experience that generates vintage-styled printable student cards. The application is a single-page web app (HTML/CSS/JavaScript) designed to run locally/offline on a tablet or laptop, creating personalized 9×6 cm physical cards for visitors at an event booth.

**Target use case:** Event booth with 100+ cards/day capacity, <60 seconds per visitor flow.

## Project Structure

```
sitecard/
├── PRD.md                          # Complete product requirements document
├── example/                        # Design assets
│   ├── background.png              # Vintage paper background for card
│   ├── icon.png                    # App icon
│   ├── logo.png / logo2.png        # Logo variations
│   ├── cardsample.jpg              # Reference card design
│   ├── schools-name-arabic.txt     # List of historic schools in Kuwait
│   └── fonts/                      # Arabic fonts
│       ├── Almarai-Regular.ttf
│       └── Almarai-Bold.ttf
└── [To be created:]
    ├── index.html                  # Main application (single-file preferred)
    ├── css/styles.css              # Optional: separated styles
    ├── js/app.js                   # Optional: separated logic
    └── assets/                     # Production assets
```

## Tech Stack & Architecture

### Core Technologies

- **Frontend:** Plain HTML5, CSS3, Vanilla JavaScript (ES6+)
- **PDF Generation:** Choose one approach:
  - **Option A (Recommended):** CSS print styles + `window.print()` for direct printing
  - **Option B:** `html2canvas` + `jsPDF` for more control and downloadable PDFs
- **Fonts:** Local Arabic TTF files loaded via `@font-face` (Almarai fonts provided)
- **Hosting:** Local file:// or simple static server (`npx serve`)

### Key Design Constraints

- **Single-file preferred** for portability and offline reliability
- **No backend required** - pure client-side application
- **Offline-first** - must work without internet after initial setup
- **Bilingual UI** - Arabic (RTL) first, then English
- **Exact dimensions** - 9×6 cm (90×60 mm) card output

## Data Model

```javascript
visitor = {
  name: string,           // Required, max 40 chars
  schoolId: string,       // Required, from schools-name-arabic.txt
  schoolLabel: string,    // Display name of school
  year: string,          // Optional, defaults to symbolic year (e.g., 1975)
  email?: string,        // Optional for digital copy
  timestamp: string      // ISO timestamp
}
```

### Local Storage

- Optional: Store cards in `localStorage.printedCards` array for audit/reprints
- Privacy: Clear daily or avoid storing email addresses

## User Flow (3 Screens)

### Screen A - Welcome

- Logo, title, short instruction
- "Start" button → Screen B

### Screen B - Input Form

- **Fields:**
  - Name (text, required, max 40 chars) - bilingual placeholder
  - School (dropdown, required) - prepopulated from schools-name-arabic.txt
  - Year (optional) - default symbolic year or computed from birth
  - Short memory line (optional, max 30 chars)
  - Email (optional, for digital copy)
- **Validation:** Name + School required before enabling preview
- **RTL support:** Use `<div dir="rtl">` for Arabic elements
- **Buttons:** "Preview Card" (primary), "Clear" (secondary)

### Screen C - Preview

- Card preview scaled for screen
- Card layout (9×6 cm):
  - Background: vintage paper image
  - Top-left: logo
  - Center: Name (large), School, Year, ID
  - **Buttons:** "Print" (primary), "Send by Email" (optional), "Edit" (back to form)

## Print Configuration

### Critical Print Settings

```css
@page {
  size: 90mm 60mm;
  margin: 0;
}

.print-card {
  width: 90mm;
  height: 60mm;
  box-sizing: border-box;
  /* Use padding for content margins, NOT page margins */
}

@media print {
  body * { visibility: hidden; }
  .print-card, .print-card * { visibility: visible; }
  .print-card { position: fixed; left: 0; top: 0; }
}
```

### Printer Setup Notes

- Configure printer driver for 90×60 mm custom paper size
- Test scale at 100% (disable "Fit to page")
- For thermal printers: check margin/bleed compatibility
- Asset resolution: 300 DPI → background should be ~1063×709 px

## Development Commands

Since this is a static web app with no build process:

```bash
# Option 1: Ope directly in browser (file:// protocol)
# Navigate to directory and open index.html

# Option 2: Run local static server (recommended for testing)
npx serve .
# Then open http://localhost:3000

# Option 3: Python simple server
python -m http.server 8000
# Then open http://localhost:8000
```

## Internationalization (i18n) Guidelines

### Arabic Language Support

- Use `<html lang="ar" dir="rtl">` for RTL layout
- Font stack: `font-family: 'AlmaraiLocal', Arial, sans-serif;`
- Load fonts via `@font-face` from `example/fonts/`
- All labels should be bilingual: "الاسم / Name"
- Ensure Arabic text alignment with `text-align: right;` or `text-align: center;`

### Schools List

Parse `example/schools-name-arabic.txt` for dropdown options:

- Elementary (ابتدائية): Lines 4-52
- Middle School (متوسطة): Lines 56-74
- High School (ثانوية): Lines 78-112

Group schools by level or show as flat list based on UX preference.

## Asset Integration

### Required Assets (from example/ folder)

1. **background.png** - Vintage paper texture for card background
2. **logo.png** - Top-left logo on card (resize to ~28px height)
3. **icon.png** - App icon/seal for bottom-right of card
4. **Fonts** - Almarai-Regular.ttf and Almarai-Bold.ttf

### Asset Preparation Checklist

- [ ] Optimize images for web (compress background.png if >500KB)
- [ ] Ensure transparent PNGs for logo and seal
- [ ] Test font rendering on target device
- [ ] Verify background image at print resolution (300 DPI)

## Testing Checklist

Before deployment:

- [ ] Form validation works (required fields enforced)
- [ ] Preview matches printed output (test 5 prints)
- [ ] PDF dimensions exactly 90×60 mm (no clipping)
- [ ] Fonts render correctly on target device
- [ ] Printer scale = 100%, margins = 0
- [ ] Arabic text displays RTL and aligns correctly
- [ ] Email sending verified (if implemented)
- [ ] Battery/power backup tested
- [ ] Staff quick-guide validated by non-technical user

## Launch Day Checklist

- Device battery ≥80% + charger present
- Printer connected, test print 1 card
- Backup paper/ink ready
- Waste bin near station
- Printed staff instructions (1 sheet)
- Consent note for email collection

## Privacy & Security

- **No cloud storage** without explicit consent
- **Email consent:** Show checkbox with privacy note: "Email will be used only to send your card; we won't store it or use it for marketing."
- **Local data:** Rotate/clear localStorage daily if storing visitor data
- **No external dependencies** in production (bundle all libraries locally)

## Staff Workflow

1. Open `index.html` in Chrome on device
2. Click "Start"
3. Help visitor enter name, school, optional memo/email
4. Click "Preview" → verify alignment
5. Click "Print" → select printer, confirm 90×60 mm size
6. Hand card to visitor
7. If email requested: export PDF and send via local email client

**Troubleshooting:**

- Text too big → reduce `.print-card` font-size
- Image clipped → verify `@page { margin: 0 }`
- Blank print → check image path and file permissions
- Arabic text disconnected → verify font and `dir="rtl"`

## Code Style & Architecture Principles

### Keep It Simple

- Prefer vanilla JS over frameworks (no React/Vue needed)
- Single-file `index.html` is acceptable and encouraged
- Inline styles/scripts are OK for portability
- Minimize dependencies (only html2canvas/jsPDF if needed)

### Accessibility

- Use semantic HTML (`<label>`, `<select>`, `<input>`)
- Add `aria-*` attributes for screen readers
- Ensure high-contrast text on background
- Keyboard navigation support (Tab, Enter)

### Performance

- Lazy-load heavy libraries (html2canvas) only when needed
- Optimize background image (WebP fallback to PNG)
- Use CSS transforms for print preview scaling
- Debounce form validation

## Common Development Tasks

### Adding a New School

1. Add school name to `example/schools-name-arabic.txt`
2. Update dropdown in `index.html` (if hardcoded) or parse from file

### Changing Card Dimensions

1. Update `@page { size: XXmm YYmm; }`
2. Update `.print-card { width: XXmm; height: YYmm; }`
3. Recalculate background image resolution (300 DPI)
4. Test print and adjust padding

### Implementing PDF Download (Option B)

```javascript
// Load libraries (add to <head>)
<script src="https://cdnjs.cloudflare.com/ajax/libs/html2canvas/1.4.1/html2canvas.min.js"></script>
<script src="https://cdnjs.cloudflare.com/ajax/libs/jspdf/2.5.1/jspdf.umd.min.js"></script>

// Generate PDF
async function generatePDF() {
  const card = document.getElementById('card');
  const canvas = await html2canvas(card, { scale: 3 });
  const imgData = canvas.toDataURL('image/png');

  const pdf = new jsPDF({
    orientation: 'landscape',
    unit: 'mm',
    format: [60, 90]
  });

  pdf.addImage(imgData, 'PNG', 0, 0, 90, 60);
  pdf.save('student-card.pdf');
}
```

### Email Integration (Optional)

- **Manual:** Export PDF, attach to local email client
- **Automated (requires network):** Node.js + nodemailer with local SMTP
- **Not recommended:** Server-side solutions (defeats offline requirement)

## Timeline Estimate

From PRD section 21:

- Design assets & template: 4–8 hours
- Build MVP web app: 4–6 hours
- Testing & printer calibration: 2–4 hours
- Staff training: 1–2 hours
- **Total:** ~12–20 hours

## References

- **PRD:** See PRD.md for complete product requirements
- **Starter Code:** PRD.md lines 211-319 (minimal working example)
- **Schools List:** example/schools-name-arabic.txt
- **Assets:** example/ folder contains all required design files

## Implementation Strategy

1. **Start with PRD starter code** (lines 211-319) as base template
2. **Replace placeholder assets** with files from example/ folder
3. **Parse schools list** from schools-name-arabic.txt and populate dropdown
4. **Test print early** on actual printer to calibrate dimensions
5. **Iterate on card design** based on print tests
6. **Add email feature** only if time permits (optional)
7. **Create staff guide** as simple PDF or printed sheet

## Known Limitations

- **No multi-language switching** - UI is fixed bilingual Arabic/English
- **No undo/history** - visitor must re-enter if they navigate away
- **No batch printing** - one card at a time
- **Email requires manual intervention** or network connectivity
- **Browser-dependent** - tested on Chrome, may vary on Safari/Firefox
