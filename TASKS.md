# Old Student Card - Development Tasks

## Project Timeline: ~12-20 hours total

---

## Stage 1: Project Setup & Asset Preparation (2-3 hours)

### 1.1 Create Project Structure
- [ ] Create `index.html` in project root
- [ ] Create `assets/` folder
- [ ] Create `assets/fonts/` subfolder
- [ ] Create `assets/images/` subfolder

### 1.2 Prepare and Optimize Assets
- [ ] Copy fonts from `example/fonts/` to `assets/fonts/`
  - Almarai-Regular.ttf
  - Almarai-Bold.ttf
- [ ] Copy and optimize images to `assets/images/`:
  - background.png (compress if >500KB)
  - logo.png (resize/optimize for web)
  - icon.png (for seal/stamp)
- [ ] Test that all assets load correctly

### 1.3 Parse Schools Data
- [ ] Read `example/schools-name-arabic.txt`
- [ ] Create structured list of schools by level:
  - Elementary (ابتدائية)
  - Middle School (متوسطة)
  - High School (ثانوية)
- [ ] Decide on dropdown format (grouped or flat list)

**Deliverable:** Project folder with all assets ready to use

---

## Stage 2: HTML Structure - Welcome Screen (1-2 hours)

### 2.1 Basic HTML Setup
- [ ] Create HTML5 doctype with `lang="ar"` and `dir="rtl"`
- [ ] Add viewport meta tag for mobile/tablet
- [ ] Add title: "بطاقة الطالب القديمة - Old Student Card"
- [ ] Load fonts via `@font-face` in `<style>` block

### 2.2 Welcome Screen (Screen A)
- [ ] Add app logo/icon at top center
- [ ] Add bilingual title: "بطاقة الطالب القديمة / Old Student Card"
- [ ] Add short instruction (1-2 lines in Arabic/English)
- [ ] Add large "ابدأ / Start" button
- [ ] Add vintage styling (warm colors, subtle textures)

### 2.3 Basic JavaScript Structure
- [ ] Add `<script>` tag at bottom
- [ ] Create app state object: `const appState = { currentScreen: 'welcome', visitor: {} }`
- [ ] Create `showScreen(screenName)` function
- [ ] Add event listener for Start button

**Deliverable:** Welcome screen with vintage aesthetic, working Start button

---

## Stage 3: Input Form Screen (2-3 hours)

### 3.1 Form HTML Structure (Screen B)
- [ ] Create form container (hidden by default)
- [ ] Add form fields:
  - Name input (text, required, max 40 chars)
  - School dropdown (required)
  - Year input (optional, default to 1975)
- [ ] Add bilingual labels for all fields
- [ ] Add "معاينة البطاقة / Preview Card" button (primary)
- [ ] Add "مسح / Clear" button (secondary)

### 3.2 Populate School Dropdown
- [ ] Create JavaScript array from schools data
- [ ] Populate `<select>` with `<optgroup>` for each level
- [ ] Add Arabic school names with proper RTL display

### 3.3 Form Validation
- [ ] Create validation function:
  - Check name is not empty
  - Check school is selected
- [ ] Show error messages in Arabic/English
- [ ] Disable Preview button until validation passes
- [ ] Add real-time validation on input

### 3.4 Form Styling (Vintage)
- [ ] Style inputs with vintage paper texture background
- [ ] Use warm, sepia-toned colors
- [ ] Add subtle shadows and borders (old paper effect)
- [ ] Ensure good contrast for readability
- [ ] Make form responsive for tablet screens

**Deliverable:** Fully functional form with validation and vintage styling

---

## Stage 4: Card Preview Design (3-4 hours)

### 4.1 Card Layout HTML (Screen C)
- [ ] Create `.print-card` container (9×6 cm / 90×60 mm)
- [ ] Set background image from assets
- [ ] Add logo in top-left corner
- [ ] Create layout for:
  - Student name (large, centered)
  - School name (smaller, below name)
  - Year
  - ID number (auto-generated)
  - Seal/stamp (bottom-right, semi-transparent)

### 4.2 ID Generation Logic
- [ ] Create `generateID()` function
  - Format: `SL-YYYYMMDD-XXXX`
  - Random 4-digit number
- [ ] Test ID generation (ensure uniqueness)

### 4.3 Preview Rendering Function
- [ ] Create `renderCardPreview(visitorData)` function
- [ ] Populate card with visitor data
- [ ] Show preview container (scaled for screen)
- [ ] Add action buttons:
  - "طباعة / Print" (primary)
  - "تعديل / Edit" (back to form)

### 4.4 Vintage Card Styling
- [ ] Apply vintage paper texture background
- [ ] Use classic Arabic fonts (Almarai)
- [ ] Add subtle aging effects:
  - Slight sepia tone
  - Soft shadows
  - Faded edges (optional)
- [ ] Ensure proper RTL text alignment
- [ ] Test different name lengths for overflow

### 4.5 Responsive Preview
- [ ] Scale card preview to fit screen (transform: scale())
- [ ] Ensure preview looks good on tablet
- [ ] Add print-specific styles (hide in preview)

**Deliverable:** Beautiful vintage card preview with all visitor data displayed

---

## Stage 5: Print Functionality (2-3 hours)

### 5.1 CSS Print Styles (Option A - Recommended)
- [ ] Add `@page { size: 90mm 60mm; margin: 0; }`
- [ ] Create `.print-card` with exact dimensions (90mm × 60mm)
- [ ] Add `@media print` rules:
  - Hide everything except `.print-card`
  - Position card at top-left
  - Ensure 100% scale
- [ ] Test print preview in browser

### 5.2 Print Button Functionality
- [ ] Add event listener to Print button
- [ ] Call `window.print()`
- [ ] Test on actual printer with 9×6 cm paper
- [ ] Adjust padding/margins if needed

### 5.3 Print Calibration
- [ ] Print 5 test cards
- [ ] Check for:
  - Correct dimensions (measure with ruler)
  - No clipping or cut-off text
  - Proper image alignment
  - Readable text at all sizes
- [ ] Adjust CSS if needed:
  - Font sizes
  - Padding
  - Image positions

### 5.4 Alternative: PDF Generation (Option B - if needed)
- [ ] Add `html2canvas` and `jsPDF` libraries (CDN or local)
- [ ] Create `generatePDF()` function
- [ ] Convert card to canvas at high DPI (scale: 3)
- [ ] Create PDF with exact dimensions (90mm × 60mm)
- [ ] Add download functionality
- [ ] Test PDF quality

**Deliverable:** Working print functionality with correct card dimensions

---

## Stage 6: Polish & User Experience (1-2 hours)

### 6.1 Screen Transitions
- [ ] Add smooth transitions between screens
- [ ] Animate screen changes (fade in/out)
- [ ] Add loading state for Preview button

### 6.2 Error Handling
- [ ] Add friendly error messages (bilingual)
- [ ] Handle print dialog cancellation
- [ ] Add "Try Again" options

### 6.3 Clear/Reset Functionality
- [ ] Implement Clear button (reset form)
- [ ] Add confirmation before clearing
- [ ] Reset to welcome screen after print

### 6.4 Accessibility
- [ ] Add `aria-label` attributes to all inputs
- [ ] Ensure keyboard navigation works (Tab, Enter)
- [ ] Test with screen reader (if available)
- [ ] Ensure high contrast for text

### 6.5 Local Storage (Optional)
- [ ] Save recent cards to `localStorage.printedCards`
- [ ] Add simple counter: cards printed today
- [ ] Add option to reprint last card

**Deliverable:** Polished app with smooth UX and error handling

---

## Stage 7: Testing & Calibration (2-3 hours)

### 7.1 Functionality Testing
- [ ] Test all form validations
- [ ] Test with various name lengths (short, medium, long)
- [ ] Test with all school options
- [ ] Test optional fields (year)
- [ ] Test Clear button
- [ ] Test Edit button from preview

### 7.2 Print Testing
- [ ] Print 10 test cards with different data
- [ ] Measure dimensions with ruler (exactly 9×6 cm?)
- [ ] Check print quality:
  - Text clarity
  - Image sharpness
  - Color accuracy (warm vintage tones)
  - No bleeding or smudging
- [ ] Test on actual event printer

### 7.3 Browser Testing
- [ ] Test in Chrome (primary)
- [ ] Test in Firefox (secondary)
- [ ] Test in Safari (if available)
- [ ] Test on actual tablet device

### 7.4 RTL & Arabic Testing
- [ ] Verify all Arabic text displays correctly
- [ ] Check RTL alignment
- [ ] Test with Arabic-only names
- [ ] Test with mixed Arabic/English input

### 7.5 Edge Cases
- [ ] Very long names (40 chars)
- [ ] Very short names (2 chars)
- [ ] Names with special characters
- [ ] Empty optional fields

**Deliverable:** Fully tested app, print calibration complete

---

## Stage 8: Documentation & Deployment (1-2 hours)

### 8.1 Staff Quick Guide
- [ ] Create simple PDF or printed sheet (1 page)
- [ ] Include step-by-step instructions:
  1. Open index.html
  2. Click Start
  3. Fill visitor info
  4. Preview → Print
  5. Hand card to visitor
- [ ] Add troubleshooting section
- [ ] Add printer setup notes

### 8.2 README Documentation
- [ ] Create/update README.md with:
  - How to run the app (open index.html or use static server)
  - Browser requirements
  - Printer setup instructions
  - Asset attribution
- [ ] Add screenshots (optional)

### 8.3 Deployment Package
- [ ] Test opening `index.html` directly (file:// protocol)
- [ ] Test with `npx serve .`
- [ ] Verify all assets load offline
- [ ] Create backup on USB drive
- [ ] Verify fonts work on target device

### 8.4 Launch Checklist
- [ ] Print launch checklist from PRD
- [ ] Device battery check
- [ ] Printer connection test
- [ ] Backup paper/ink ready
- [ ] Staff trained on quick guide

**Deliverable:** Production-ready app with documentation

---

## Stage 9: Optional Enhancements (If Time Permits)

### 9.1 Email Functionality (Removed from scope)
- Email and memory line fields have been removed to keep the form simple
- Focus is on: Name, School, Year only

### 9.2 Advanced Features
- [ ] Add photo upload (visitor photo on card)
- [ ] Add QR code with card ID
- [ ] Add print queue (multiple cards)
- [ ] Add statistics dashboard (cards printed today)

### 9.3 Themes
- [ ] Create 2-3 vintage color schemes
- [ ] Add theme selector
- [ ] Different background textures

**Deliverable:** Enhanced app with extra features

---

## Stage 10: Event Day Support (Ongoing)

### 10.1 Pre-Event Setup
- [ ] Charge device to 80%+
- [ ] Load paper in printer
- [ ] Print 3 test cards
- [ ] Have backup supplies ready

### 10.2 During Event
- [ ] Monitor printer status
- [ ] Track cards printed (mental note or counter)
- [ ] Handle any technical issues
- [ ] Collect feedback from visitors

### 10.3 Post-Event
- [ ] Clear localStorage (privacy)
- [ ] Save any important data
- [ ] Document any issues encountered
- [ ] Plan improvements for next event

**Deliverable:** Successful event execution

---

## Quick Start Guide (Which Stage to Begin)

**Start Here:**
1. If assets are ready → Stage 2 (HTML Structure)
2. If starting from scratch → Stage 1 (Setup)
3. If you have basic HTML → Stage 3 (Form)
4. If form is done → Stage 4 (Card Design)

**Current Status:** Ready to start Stage 1

---

## Time Estimates Summary

| Stage | Task | Time |
|-------|------|------|
| 1 | Setup & Assets | 2-3h |
| 2 | Welcome Screen | 1-2h |
| 3 | Input Form | 2-3h |
| 4 | Card Preview | 3-4h |
| 5 | Print Functionality | 2-3h |
| 6 | Polish & UX | 1-2h |
| 7 | Testing | 2-3h |
| 8 | Documentation | 1-2h |
| **Total** | **MVP** | **14-22h** |
| 9 | Optional Features | +4-6h |

---

## Notes

- Each stage builds on the previous one
- Test frequently, especially print functionality
- Focus on vintage aesthetic throughout
- Keep it simple - single file is OK
- Prioritize Arabic/RTL support
- Print calibration is critical - don't skip!

**Ready to start? Let me know which stage you'd like to begin with!**
