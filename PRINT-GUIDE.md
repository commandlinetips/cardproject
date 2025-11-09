# Print Calibration Guide - Old Student Card

## Quick Print Setup

### Step 1: Printer Configuration

**Paper Size:**
- Width: 90mm (9cm)
- Height: 60mm (6cm)
- Orientation: Landscape

**Print Settings:**
- Margins: 0mm (No margins)
- Scale: 100% (Do NOT use "Fit to page")
- Quality: Best/High quality
- Color: Full color

### Step 2: Browser Print Settings

When clicking "طباعة / Print":

1. **Destination:** Select your printer
2. **Layout:** Landscape
3. **Paper size:** Custom 90 × 60 mm (or 9 × 6 cm)
4. **Margins:** None
5. **Scale:** 100%
6. **Options:**
   - Disable "Headers and footers"
   - Disable "Background graphics" (optional)

### Step 3: Test Print

1. Print one test card
2. Measure with ruler:
   - Should be exactly 9cm wide × 6cm tall
   - Check all corners are visible
   - Verify no text is cut off

### Step 4: Troubleshooting

#### Problem: Card is too small/large
**Solution:**
- Ensure scale is set to 100%
- Disable "Fit to page" option
- Check custom paper size matches 90×60mm

#### Problem: Text is cut off at edges
**Solution:**
- Set margins to 0mm
- Verify paper size is correct
- Check printer driver settings

#### Problem: Logo or seal is missing
**Solution:**
- Enable "Background graphics" in print options
- Ensure images are loading (check internet connection for first load)
- Try PDF download option instead

#### Problem: Card is blank when printed
**Solution:**
- Ensure you're printing from the Preview screen
- Check printer has paper and ink
- Try downloading PDF and printing that instead

#### Problem: Colors look wrong
**Solution:**
- Check color printer settings (not grayscale)
- Adjust printer color calibration
- The vintage sepia effect is intentional

## Printer-Specific Settings

### For Photo Printers:
- Use photo paper (glossy or matte)
- Set to "Borderless" mode if available
- Custom size: 90 × 60 mm

### For Thermal Printers:
- Configure custom label size in driver
- Disable auto-cut between cards (if continuous)
- Test media thickness setting

### For Regular Printers:
- Use heavy cardstock (200-300gsm recommended)
- Custom paper size in driver settings
- May need to manually cut to size

## PDF Download Option

If direct printing doesn't work well:

1. Click "تحميل PDF / Download PDF" button
2. Wait for PDF generation (takes 2-3 seconds)
3. PDF will download as: `student-card-[name]-[ID].pdf`
4. Open PDF and print from PDF viewer
5. Advantages:
   - More reliable across different printers
   - Can email to visitors
   - Keeps digital backup

## Card Dimensions Reference

```
┌─────────────────────────────┐
│                             │  60mm (height)
│    Student Card Layout      │
│                             │
└─────────────────────────────┘
        90mm (width)

Actual size card = Credit card size
```

## Testing Checklist

Before event day:

- [ ] Printer driver installed and updated
- [ ] Custom paper size 90×60mm configured
- [ ] Test print completed and measured
- [ ] 5 test cards printed successfully
- [ ] Colors look correct (vintage brown tones)
- [ ] All text is readable
- [ ] Logo and seal are visible
- [ ] No clipping at edges
- [ ] Paper/card stock loaded
- [ ] Backup paper available
- [ ] PDF download tested (as backup option)

## localStorage Data

The app automatically tracks printed cards:

**View history in browser console:**
```javascript
localStorage.getItem('printedCards')
```

**Clear history:**
```javascript
localStorage.removeItem('printedCards')
```

**Get today's count:**
```javascript
// Already logged in console on app start
// Check: "📊 Cards printed today: X"
```

## Performance Tips

1. **Pre-load images:** Open app once before event to cache assets
2. **Keep browser tab open:** Don't close between prints
3. **Disable browser extensions:** Ad blockers can interfere
4. **Use Chrome:** Best print support (recommended browser)

## Emergency Backup Plan

If printing fails during event:

1. **Use PDF Download** - Generate PDFs and print later
2. **Export data** - Save localStorage to backup file
3. **Mobile hotspot** - If offline, use phone for internet
4. **Second device** - Have backup laptop/tablet ready

## Card Quality Standards

**Acceptable:**
- ✅ All text clearly visible
- ✅ Logo recognizable
- ✅ Seal/stamp visible
- ✅ Colors warm/brown vintage tones
- ✅ Dimensions within ±2mm tolerance

**Not Acceptable:**
- ❌ Text cut off at edges
- ❌ Name unreadable
- ❌ ID number missing
- ❌ Severely faded/too dark
- ❌ Paper jam damage

## Support

For technical issues:
1. Check browser console (F12) for errors
2. Test PDF download as alternative
3. Verify all assets loaded (check Network tab)
4. Try different browser (Chrome recommended)

---

**Last Updated:** 2025-11-09
**Card Dimensions:** 90mm × 60mm (exact)
**Recommended Browser:** Chrome/Chromium
**Tested Printers:** Photo printers, Thermal label printers
