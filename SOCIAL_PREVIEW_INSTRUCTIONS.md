# 🎨 Social Preview Image Instructions

## How to Generate the Image

1. **Open the HTML file** in your browser:
   ```bash
   open social-preview.html
   ```

2. **Take a screenshot** using one of these methods:

### Option A: Browser Developer Tools
1. Open Chrome/Edge DevTools (F12)
2. Toggle device toolbar (Ctrl+Shift+M / Cmd+Shift+M)
3. Set dimensions to **1280 x 640**
4. Take screenshot (⋮ menu → Capture screenshot)

### Option B: Online Tool
1. Go to https://htmlcsstoimage.com/
2. Paste the HTML content
3. Set width: 1280px, height: 640px
4. Generate & download

### Option C: Command Line (if you have Puppeteer)
```bash
npx capture-website social-preview.html social-preview.png --width=1280 --height=640
```

## Upload to GitHub

1. Go to your repo Settings
2. Scroll to "Social preview"
3. Click "Edit" → "Upload an image"
4. Select the generated image
5. Save changes

## Alternative Designs

If you want different color schemes, edit the CSS gradient in `social-preview.html`:

### Purple/Blue (Current)
```css
background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
```

### Dark Modern
```css
background: linear-gradient(135deg, #0f0f0f 0%, #434343 100%);
```

### Teal/Green
```css
background: linear-gradient(135deg, #11998e 0%, #38ef7d 100%);
```

### Orange/Pink
```css
background: linear-gradient(135deg, #fa709a 0%, #fee140 100%);
```

The preview image is ready to be generated and uploaded!
