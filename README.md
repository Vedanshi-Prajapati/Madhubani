<div align="center">

  <img src="artform/Assets.xcassets/AppIcon.appiconset/logo.png" alt="Madhubani Icon" width="112" height="112" style="border-radius: 24px;" />

  # Madhubani
  ### Traditional Mithila Folk Art for iOS

  <p align="center">
    A guided drawing app for learning and creating traditional Madhubani folk art on iPhone and iPad.
  </p>

  [![WWDC 2026 Winner](https://img.shields.io/badge/WWDC%202026-Swift%20Student%20Challenge%20Winner-FFD700?style=flat-square&logo=apple&logoColor=black)](https://developer.apple.com/wwdc/)
  [![App Store](https://img.shields.io/badge/App_Store-Download-blue?style=flat-square&logo=apple&logoColor=white)](https://apps.apple.com/in/app/madhubani/id6792649215)
  [![Platform](https://img.shields.io/badge/Platform-iOS%2017%2B%20%7C%20iPadOS-lightgrey?style=flat-square)](https://developer.apple.com/ios/)
  [![Swift](https://img.shields.io/badge/Swift-5.9+-orange?style=flat-square&logo=swift&logoColor=white)](https://swift.org)
  [![SwiftUI](https://img.shields.io/badge/UI-SwiftUI-informational?style=flat-square)](https://developer.apple.com/xcode/swiftui/)
  [![License](https://img.shields.io/badge/License-MIT-green?style=flat-square)](LICENSE)

  <br/>

  <a href="#overview">Overview</a> •
  <a href="#features">Features</a> •
  <a href="#tools--mechanics">Tools & Mechanics</a> •
  <a href="#architecture">Architecture</a> •
  <a href="#getting-started">Getting Started</a> •
  <a href="#app-store">App Store</a> •
  <a href="#support--privacy">Support & Privacy</a>
</div>

---

> **Apple WWDC 2026 Swift Student Challenge Winner**  
> Recognized by Apple for preserving cultural art through native iOS engineering, combining on-device computer vision with a custom drawing canvas.

---

## Overview

**Madhubani** is an iOS application designed to teach and preserve the traditional art form of Mithila (Madhubani) painting from Bihar, India. Known for its distinct double-line borders, intricate hatching (*Kachni*), vibrant natural pigments (*Bharni*), and geometric symmetry, the art form has been practiced for generations on mud walls and handmade paper.

The app translates these traditional techniques into an interactive digital medium. Using Apple's **Vision framework**, the app detects contours in traditional templates to guide learners with real-time stroke snapping and coverage tracking, while also providing a sandbox mode for original artwork.

---

## Features

### Guided Learning Journey
- **15 Progressive Levels**: Covers essential folk motifs, ranging from basic floral elements and birds to complex deity compositions and multi-layered mandalas.
- **Interactive Roadmap**: Visual level progression with persistent unlock tracking.
- **Contour Extraction**: Uses `VNDetectContoursRequest` to extract template line geometry directly from image assets at runtime.
- **Assisted Snapping**: Real-time distance calculation snaps drawing paths to underlying template contours with adjustable strength.
- **Coverage Feedback**: Tracks stroke overlap against template paths to calculate drawing progress.

### Drawing Engine
- **Stroke Styles**:
  - `Single Line`: Standard line for fine details.
  - `Double Line`: Parallel double strokes characteristic of traditional Madhubani linework.
  - `Single & Double Wavy`: Curved patterns for borders, water, and garments.
- **Hatching & Fill Patterns**: Traditional *Kachni* textures including dots, crosshatch, stripes, waves, and checks.
- **Scanline Flood Fill**: Custom boundary-fill algorithm for coloring enclosed areas with high edge accuracy.
- **Symmetry Engine**: Real-time bilateral and radial mirroring for drawing balanced mandalas and border motifs.
- **Canvas Interaction**: Smooth pan and pinch-to-zoom (up to 4x) with floating zoom HUD and reset controls.
- **History**: Full undo/redo stack.

### Curated Color Palettes
Four palettes modeled after natural dyes and mineral pigments historically used in Mithila art:
- **Classic**: Crimson, turmeric, forest green, deep indigo, charcoal black, ochre.
- **Earthy**: Terracotta, raw umber, dried straw, soft clay.
- **Indigo Night**: Midnight blue, royal indigo, temple gold, slate grey.
- **Festive**: Vermilion, marigold orange, rani pink, leaf green.

### Free Draw & Gallery
- **Sandbox Studio**: Unconstrained blank canvas with full access to all brushes, fill patterns, symmetry tools, and palettes.
- **Local Persistence**: Completed works are saved to the app sandbox as high-resolution PNGs and indexed with Core Data.
- **In-App Gallery**: View, inspect, and manage saved artworks with creation timestamps.

---

## Tools & Mechanics

| Tool | Mode | Implementation |
| :--- | :--- | :--- |
| **Double Brush** | Draw | Calculates perpendicular offsets along touch points to render parallel double strokes. |
| **Wavy Brush** | Draw | Applies sine-wave phase modulation to the stroke path based on cumulative arc-length. |
| **Hatching Pattern** | Pattern | Fills target regions using procedural clip paths (dots, diagonal stripes, crosshatching). |
| **Flood Fill** | Bucket | Scanline flood fill on a raw pixel buffer with color-distance thresholding. |
| **Symmetry Guide** | Assist | Mirrors touch points across canvas center axes in real time. |
| **Contour Assist** | Assist | Finds nearest contour vertex and pulls points within snap radius via weighted falloff. |

---

## Architecture

The project is built entirely in Swift using SwiftUI and UIKit:

```
artform/
├── AppState.swift               # Global observable app state and progress coordinator
├── MadhubaniApp.swift           # @main application entry point
├── RootFlow.swift               # Flow coordinator: loader, onboarding, main tabs
│
├── Canvas & Engine/
│   ├── CanvasEngine.swift       # Touch input pipeline, stroke smoothing, and render passes
│   ├── CanvasStore.swift        # Stroke/fill data model and undo/redo stacks
│   ├── CanvasTransform.swift    # Pan/zoom matrix transformation
│   ├── CanvasView.swift         # UIKit/SwiftUI bridging surface for low-latency drawing
│   ├── FloodFill.swift          # Scanline flood fill implementation
│   └── AssistEngine.swift       # Nearest-neighbor contour snapping and coverage calculation
│
├── Vision/
│   └── VisionTemplateProcessor  # Actor performing VNDetectContoursRequest and path flattening
│
├── UI & Screens/
│   ├── RoadmapView.swift        # 15-level curved progression view
│   ├── DrawScreen.swift         # Guided level drawing interface
│   ├── FreeDrawView.swift       # Open canvas sandbox view
│   ├── GalleryViews.swift       # Saved artwork gallery and detail inspection
│   ├── ToolBar.swift            # Expandable floating tool selector
│   └── LoaderScreen.swift       # Launch transitions and state loading
│
├── Data & Persistence/
│   ├── Models.swift             # Artwork, Level, and Palette data structs
│   ├── LevelData.swift          # Level metadata and template image associations
│   ├── PersistenceController.swift # Core Data stack configuration
│   ├── ArtworkStore.swift       # Disk I/O for saving and loading artwork PNG files
│   └── ProgressStore.swift      # Level unlock persistence
│
└── Theme/
    └── MTheme.swift             # Palettes, typography definitions, and styling constants
```

---

## App Store

Madhubani is available for download on iPhone and iPad:

<div align="center">
  <a href="https://apps.apple.com/in/app/madhubani/id6792649215">
    <img src="https://tools.applemediaservices.com/api/badges/download-on-the-app-store/black/en-us?size=250x83&releaseDate=1600000000" alt="Download on the App Store" width="160">
  </a>
  <p><a href="https://apps.apple.com/in/app/madhubani/id6792649215">Download Madhubani on the App Store</a></p>
</div>

---

## Getting Started

### Requirements
- macOS Sonoma 14.0 or later
- Xcode 15.0 or later
- iOS 17.0+ deployment target

### Build & Run
1. Clone the repository:
   ```bash
   git clone https://github.com/Vedanshi-Prajapati/Madhubani.git
   cd Madhubani
   ```
2. Open the project in Xcode:
   ```bash
   open artform.xcodeproj
   ```
3. Select your development team under **Signing & Capabilities**.
4. Choose a simulator or connected iOS device and press `Cmd + R` to build and run.

---

## Support & Privacy

- **Support**: For technical support or inquiries, visit the [Support Page](https://vedanshi-prajapati.github.io/madhubani-support/support.html) or open an [Issue on GitHub](https://github.com/Vedanshi-Prajapati/Madhubani/issues).
- **Privacy Policy**: All drawing data and completed artworks are stored strictly on-device. No analytics, tracking, or user data are collected or transmitted. Read the full [Privacy Policy](https://vedanshi-prajapati.github.io/madhubani-support/privacyPolicy.html).

---

## Author

**Vedanshi Prajapati**  
GitHub: [@Vedanshi-Prajapati](https://github.com/Vedanshi-Prajapati)

---

## License

This project is licensed under the [MIT License](LICENSE).
