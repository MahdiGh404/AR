# Web AR - Image Tracking Application

A marker-based augmented reality web application that uses MindAR to detect a target image and overlay a video when the marker is recognized.

## 🎯 Features

- **Marker-based AR tracking** using MindAR image tracking
- **Video overlay** that plays when target is detected
- **Smart video playback**: Pauses when target is lost, resumes (not restarts) when found
- **Audio support** from video file
- **Mobile-first design** optimized for smartphones
- **Desktop compatible** works with webcams
- **Comprehensive error handling** with user-friendly messages
- **No backend required** - runs entirely in the browser

## 📁 Project Structure

```
webAR/
├── index.html          # Main AR application (complete with CSS & JS)
├── target.jpg          # AR marker image (your target)
├── tracker.mp4         # Video to overlay on marker
├── targets.mind        # Compiled target (you must generate this)
└── README.md           # This file
```

## 🚀 Quick Start

### Step 1: Compile Target Image

Before you can use the AR application, you must compile `target.jpg` into a `.mind` file:

1. **Visit the MindAR Compiler**: https://hiukim.github.io/mind-ar-js-doc/tools/compile

2. **Upload your target image**:
   - Click or drag `target.jpg` into the upload area

3. **Compile**:
   - Click the "Start" button
   - Wait for compilation to complete (usually 10-30 seconds)
   - You'll see red dots appear on your image (these are feature points)

4. **Download**:
   - Click the "Download" button
   - Save the file as `targets.mind`

5. **Place in project**:
   - Move `targets.mind` to the same directory as `index.html`

> **💡 Tip**: Good target images have:
> - High contrast and unique patterns
> - Clear edges and details
> - No repetitive patterns
> - Good lighting (not too dark or washed out)

### Step 2: Set Up Local Server

AR applications require HTTPS or localhost. Choose one method:

#### Option A: Using npx (recommended - no installation needed)
```bash
npx http-server -p 8080
```

#### Option B: Using Python 3
```bash
python -m http.server 8080
```

#### Option C: Using VS Code Live Server
1. Install "Live Server" extension in VS Code
2. Right-click `index.html`
3. Select "Open with Live Server"

### Step 3: Prepare Target Image

You need a physical copy of `target.jpg` to scan:

- **Option 1 (Recommended)**: Print `target.jpg` on paper (A4 or Letter size)
- **Option 2**: Display `target.jpg` on another device screen (tablet, another phone, etc.)

> **⚠️ Important**: The target should be clear, well-lit, and flat for best tracking results.

### Step 4: Test on Mobile Device

1. **Find your local IP address**:
   - Windows: Run `ipconfig` in terminal, look for IPv4 Address
   - Mac/Linux: Run `ifconfig`, look for inet address

2. **Access the application**:
   - On your mobile device, open a browser
   - Navigate to: `http://YOUR_IP_ADDRESS:8080`
   - Example: `http://192.168.1.100:8080`

3. **Grant permissions**:
   - Allow camera access when prompted

4. **Scan the target**:
   - Point your phone camera at the printed/displayed `target.jpg`
   - The video should appear overlaid on the target

## 🎮 How It Works

1. **Camera opens** automatically when page loads
2. **System scans** for the target image in real-time
3. **Target detected** → Video starts playing (with audio)
4. **Target visible** → Video continues to loop
5. **Target lost** → Video pauses (preserves position)
6. **Target found again** → Video resumes from where it paused
7. **Move device** → Video stays aligned with target boundaries

## 🌐 Browser Requirements

### Supported Browsers

| Browser | Mobile | Desktop | Notes |
|---------|--------|---------|-------|
| Chrome | ✅ 90+ | ✅ 90+ | Recommended |
| Safari | ✅ 14.5+ | ✅ 14.5+ | iOS requires iOS 14.5+ |
| Firefox | ✅ 88+ | ✅ 88+ | Good performance |
| Edge | ✅ 90+ | ✅ 90+ | Chromium-based |

### Requirements

- **HTTPS or localhost** - Required for camera access
- **Camera permission** - User must grant access
- **WebGL support** - For Three.js rendering
- **Modern JavaScript** - ES6+ features used

## 🔧 Troubleshooting

### Camera Access Issues

**Problem**: "Camera Access Denied" error

**Solutions**:
- Check browser permissions settings
- Ensure you're accessing via HTTPS or localhost
- On iOS, check Settings → Safari → Camera access
- On Android, check Settings → Apps → Browser → Permissions
- Try reloading the page
- Try a different browser

---

### Target Not Detected

**Problem**: Camera works but target isn't detected

**Solutions**:
- **Lighting**: Ensure good, even lighting (not too bright or dark)
- **Distance**: Hold device 20-50cm from target
- **Angle**: Keep target flat and perpendicular to camera
- **Target quality**: Ensure printed/displayed target is clear
- **Movement**: Keep device and target relatively still initially
- **Compilation**: Verify `targets.mind` was generated correctly
- **Target image**: Try a different image with more distinctive features

---

### Video Not Playing

**Problem**: Target detected but video doesn't play

**Solutions**:
- Check that `tracker.mp4` exists in the project directory
- Verify video file format (MP4 with H.264 codec recommended)
- Check browser console for specific error messages
- Try with audio muted (some browsers block autoplay with audio)
- Ensure video file isn't corrupted
- Try a smaller/different video file

---

### "Target File Missing" Error

**Problem**: Error about `targets.mind` not found

**Solutions**:
- Ensure you've compiled `target.jpg` using the MindAR compiler
- Verify `targets.mind` is in the same directory as `index.html`
- Check filename is exactly `targets.mind` (case-sensitive)
- Clear browser cache and reload

---

### HTTPS Required Error

**Problem**: "Insecure Connection" or HTTPS requirement message

**Solutions**:
- Access via `localhost` instead of IP address
- Set up HTTPS on your local server
- Use ngrok for HTTPS tunneling: `npx ngrok http 8080`
- On mobile, ensure you're using the correct protocol

---

### Performance Issues

**Problem**: Laggy or slow performance

**Solutions**:
- Use a more powerful device
- Close other apps/browser tabs
- Reduce video file size/resolution
- Ensure good lighting (reduces CPU load)
- Try disabling browser extensions
- Use Chrome (generally best performance)

---

### Desktop Testing

**Problem**: Want to test on desktop with webcam

**Solutions**:
- Print `target.jpg` or display on phone/tablet
- Hold target in front of webcam
- Ensure good lighting
- Keep target clearly visible and flat
- Note: Mobile testing is recommended as primary platform

## 📱 Mobile Optimization

The application is optimized for mobile devices:

- Touch-friendly UI
- Automatic orientation handling
- Optimized rendering performance
- Mobile-first responsive design
- Proper viewport configuration
- iOS Safari compatibility

## 🛠️ Technical Details

### Technology Stack

- **MindAR 1.2.5** - Image tracking library
- **Three.js 0.160.0** - 3D rendering engine
- **Vanilla JavaScript** - No framework dependencies
- **HTML5 Video** - Native video playback

### Video Specifications

- **Format**: MP4 (H.264 codec recommended)
- **Rendering**: 2D plane overlay (not 3D object)
- **Positioning**: Scaled to match target image boundaries
- **Audio**: Enabled by default
- **Looping**: Continuous loop when target visible

### AR Tracking

- **Type**: Marker-based (image tracking)
- **Max targets**: 1 simultaneous target
- **Target file**: `.mind` compiled format
- **Camera**: Rear-facing (default on mobile)

## 🔒 Privacy & Security

- Camera feed is processed **locally in the browser**
- **No data is uploaded** to any server
- No tracking or analytics
- All processing happens on your device
- Camera access can be revoked at any time in browser settings

## 📝 Customization

### Change Target Image

1. Replace `target.jpg` with your image
2. Re-compile using MindAR compiler
3. Replace `targets.mind` with new compiled file

### Change Video

1. Replace `tracker.mp4` with your video
2. Recommended: MP4 format, H.264 codec
3. Keep file size reasonable for mobile performance

### Adjust Video Size

Edit the geometry in `index.html` (around line 330):

```javascript
// Current: video matches target aspect ratio
const geometry = new THREE.PlaneGeometry(1, 1 / videoAspect);

// Make video larger: multiply dimensions
const geometry = new THREE.PlaneGeometry(1.5, 1.5 / videoAspect);

// Make video smaller: reduce dimensions
const geometry = new THREE.PlaneGeometry(0.5, 0.5 / videoAspect);
```

## ❓ FAQ

**Q: Can I use multiple target images?**  
A: Yes, modify `maxTrack` in the code and compile multiple images into one `.mind` file.

**Q: Does this work offline?**  
A: Once loaded, yes if files are cached. Initial load requires internet for CDN libraries.

**Q: Can I use animated/video markers?**  
A: No, MindAR requires static image markers.

**Q: What image formats are supported for targets?**  
A: JPG and PNG work best. High contrast images track better.

**Q: Why does my video restart instead of resume?**  
A: Check the code - ensure `video.pause()` and `video.play()` are used correctly without resetting `currentTime`.

**Q: Can I deploy this to a website?**  
A: Yes! Just upload all files to any web hosting with HTTPS enabled.

## 🐛 Still Having Issues?

1. **Check browser console** (F12) for error messages
2. **Verify file structure** - all files in correct locations
3. **Test with sample images** - use MindAR's example targets first
4. **Try different devices** - test on multiple phones/browsers
5. **Check internet connection** - required for loading libraries

## 📚 Additional Resources

- **MindAR Documentation**: https://hiukim.github.io/mind-ar-js-doc/
- **MindAR GitHub**: https://github.com/hiukim/mind-ar-js
- **Three.js Documentation**: https://threejs.org/docs/
- **Image Target Compiler**: https://hiukim.github.io/mind-ar-js-doc/tools/compile

## 📄 License

This project uses open-source libraries:
- MindAR: Apache License 2.0
- Three.js: MIT License

---

**Made with ❤️ using MindAR and Three.js**
