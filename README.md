<div align="center">

  <img src="artform/Assets.xcassets/AppIcon.appiconset/logo.png" alt="Madhubani App Icon" width="128" height="128" style="border-radius: 28px; box-shadow: 0 10px 25px rgba(0,0,0,0.15);" />

  # Madhubani (मधुबनी)
  ### Traditional Mithila Folk Art Studio for iOS

  <p align="center">
    <i>"Enter a world where every line is a ritual and every color is nature."</i>
  </p>

  [![Download on the App Store](https://img.shields.io/badge/App_Store-Download-0D96F6?style=for-the-badge&logo=apple&logoColor=white)](https://apps.apple.com/in/app/madhubani/id6792649215)
  [![Platform](https://img.shields.io/badge/Platform-iOS%20%7C%20iPadOS-lightgrey?style=for-the-badge&logo=apple)](https://developer.apple.com/ios/)
  [![Swift](https://img.shields.io/badge/Swift-5.9+-FA7343?style=for-the-badge&logo=swift&logoColor=white)](https://swift.org)
  [![SwiftUI](https://img.shields.io/badge/UI-SwiftUI-007ACC?style=for-the-badge&logo=swift)](https://developer.apple.com/xcode/swiftui/)
  [![Vision Framework](https://img.shields.io/badge/Core-Vision%20AI-blueviolet?style=for-the-badge)](https://developer.apple.com/documentation/vision)

  <br/>

  <a href="#-about-the-app">About</a> •
  <a href="#-key-features">Key Features</a> •
  <a href="#-traditional-art-tools">Art Tools</a> •
  <a href="#-technical-architecture">Architecture</a> •
  <a href="#-getting-started">Getting Started</a> •
  <a href="#-download-on-app-store">App Store</a>
</div>

---

## 🌺 About the App

**Madhubani** is an immersive digital art studio dedicated to preserving, celebrating, and teaching the ancient Indian folk art form of **Mithila / Madhubani painting**.

Originating from the Mithila region of Bihar, Madhubani art is renowned for its intricate geometric patterns, dual-line contouring (*Kachni*), vibrant natural pigments (*Bharni*), and sacred cultural symbolism. This app brings this centuries-old tradition into the digital age—pairing traditional Indian folk aesthetics with cutting-edge iOS technologies like **Apple's Vision Framework** and modern **SwiftUI** gestures.

Whether you are a beginner exploring cultural art or an experienced artist creating complex mandalas, **Madhubani** offers guided learning and freeform creative expression.

---

## ✨ Key Features

### 🗺️ The Guided Journey (15 Progressive Levels)
- **Interactive Folk Roadmap**: Follow a progressive learning path across 15 handcrafted folk motifs—from sacred peacocks and fish to lotus mandalas and divine figures.
- **Level Progression**: Complete artworks to unlock subsequent stages and build your mastery step by step.
- **Visual Completion Tracking**: Track your completion percentage across your creative journey.

### 👁️ AI-Powered Contour Assist Engine
- **Vision-Driven Line Snapping**: Integrates Apple's `Vision` framework (`VNDetectContoursRequest`) to detect the contours of traditional folk templates.
- **Smart Snap & Line Stabilization**: Gently snaps your brush strokes to intricate contour paths, helping you capture traditional linework with confidence.
- **Real-Time Coverage Detection**: Measures stroke accuracy and coverage against sacred outlines.

### 🖌️ Authentic Traditional Drawing Tools
- **Traditional Stroke Engine**:
  - `Single Line`: Fine-line detailing for delicate features.
  - `Double Line`: The quintessential hallmark of authentic Madhubani art.
  - `Single & Double Wavy`: Classic river, cloud, and border flourishes.
- **Folk Fill Patterns**:
  - `Dots (Kachni)`: Fine pointillism texture.
  - `Stripes & Crosshatch`: Rhythmic geometric hatching.
  - `Waves & Checks`: Traditional decorative filling.
- **Scanline Flood Fill**: Fill closed boundary regions instantly with rich natural pigment shades.
- **Radial & Bilateral Symmetry**: Craft balanced mandalas, flowers, and folk borders with real-time mirroring.

### 🎨 Hand-Curated Natural Palettes
Traditional Madhubani art uses pigments derived from lampblack, turmeric, indigo, and clay. The app includes four authentic themes:
- **Classic**: Crimson (*Sindoor*), Turmeric Gold, Deep Indigo, Forest Green, Mineral Black.
- **Earthy**: Terracotta, Raw Umber, Dried Clay, Mud Straw, River Ochre.
- **Indigo Night**: Midnight Navy, Royal Indigo, Temple Gold, Soft Ash.
- **Festive**: Radiant Vermilion, Marigold Orange, Rani Pink, Parrot Green.

### 🎨 Free Draw Creative Studio
- Create completely original Madhubani masterpieces without templates.
- Full access to all custom brushes, hatching patterns, symmetry axes, and natural dye palettes.

### 🖼️ Personal Gallery & Export
- **Automated Archiving**: Completed artworks are automatically preserved in high-resolution PNG format and indexed with CoreData.
- **Artwork Showcase**: Revisit, inspect, or delete your finished pieces anytime.

---

## 🛠 Traditional Art Tools

| Tool | Mode | Description |
| :--- | :--- | :--- |
| **Double Brush** | `Draw` | Automatically draws parallel double outlines characteristic of Mithila painting. |
| **Wavy Brush** | `Draw` | Rhythmic sinuous curves for traditional water, foliage, and garment folds. |
| **Hatching Pattern** | `Pattern` | Fills selected areas with traditional *Kachni* crosshatch, dots, and diagonal strokes. |
| **Flood Fill** | `Bucket` | High-precision color fill engine with boundary color isolation. |
| **Symmetry Guide** | `Assist` | Mirrored drawing across axes for sacred geometrical mandalas (*Aripana*). |
| **Contour Assist** | `Assist` | Real-time path snapping powered by on-device computer vision. |

---

## 🏛 Technical Architecture

The application is engineered strictly with Swift, SwiftUI, and native Apple frameworks:

```
artform/
├── AppState.swift               # Global application state, progression, & artwork catalog
├── MadhubaniApp.swift           # Application entry point (@main)
├── RootFlow.swift               # Onboarding, loading coordinator, and tab navigation
│
├── Canvas & Engine/
│   ├── CanvasEngine.swift       # Touch ingestion, stroke rendering, & bezier calculations
│   ├── CanvasStore.swift        # State storage for current drawing session & undo/redo
│   ├── CanvasTransform.swift    # Pan, pinch-to-zoom matrix & coordinate transformations
│   ├── CanvasView.swift         # Interactive drawing surface
│   ├── FloodFill.swift          # Bitmap-level scanline flood fill implementation
│   └── AssistEngine.swift       # Nearest-point contour snapping & accuracy coverage
│
├── Vision & AI/
│   └── VisionTemplateProcessor  # Apple Vision contour extraction (VNDetectContoursRequest)
│
├── UI & Screens/
│   ├── RoadmapView.swift        # 15-level curved journey roadmap with level nodes
│   ├── DrawScreen.swift         # Guided level drawing interface
│   ├── FreeDrawView.swift       # Open canvas sandbox drawing mode
│   ├── GalleryViews.swift       # CoreData-backed gallery & artwork detail view
│   ├── ToolBar.swift            # Custom floating toolbar, brushes, and color selectors
│   └── LoaderScreen.swift       # Traditional opening splash and level transitions
│
├── Data & Persistence/
│   ├── Models.swift             # Artwork, Level, and Palette data definitions
│   ├── LevelData.swift          # Level configuration and asset mappings
│   ├── PersistenceController.swift # CoreData stack for persistent storage
│   ├── ArtworkStore.swift       # Local file storage for exported PNG artworks
│   └── ProgressStore.swift      # Level unlock and completion persistence
│
└── Theme & Design System/
    └── MTheme.swift             # Color palettes, custom typography, & parchment styling
```

### Key Technologies
- **UI Framework**: SwiftUI + Combine
- **Vision & Graphics**: Apple `Vision` (`VNDetectContoursRequest`), `CoreGraphics`, `UIKit`
- **Data Persistence**: `CoreData` + `FileManager` (high-res PNG assets) + `UserDefaults`
- **Deployment Target**: iOS 17.0+ / iPadOS 17.0+

---

## 📲 Download on the App Store

Madhubani is officially available for iPhone and iPad on the Apple App Store:

<div align="center">
  <a href="https://apps.apple.com/in/app/madhubani/id6792649215" target="_blank">
    <img src="https://tools.applemediaservices.com/api/badges/download-on-the-app-store/black/en-us?size=250x83&releaseDate=1600000000" alt="Download on the App Store" width="190">
  </a>
  <p><a href="https://apps.apple.com/in/app/madhubani/id6792649215"><b>View Madhubani on the App Store ↗</b></a></p>
</div>

---

## 🚀 Getting Started (Developers)

To explore or build the source code locally:

### Prerequisites
- macOS Sonoma (14.0+) or macOS Sequoia (15.0+)
- Xcode 15.0 or later
- iOS 17.0+ physical device or simulator

### Installation

1. **Clone the repository**:
   ```bash
   git clone https://github.com/Vedanshi-Prajapati/Madhubani.git
   cd Madhubani
   ```

2. **Open the project in Xcode**:
   ```bash
   open artform.xcodeproj
   ```

3. **Configure Signing**:
   - In Xcode, select the `artform` project in the Project Navigator.
   - Go to the **Signing & Capabilities** tab.
   - Select your Apple Developer Team.

4. **Build and Run**:
   - Select an iOS Simulator (e.g., iPhone 15 Pro or iPad Air) or a connected physical device.
   - Press `Cmd + R` to build and launch the app.

---

## 👤 Author

**Vedanshi Prajapati**
- GitHub: [@Vedanshi-Prajapati](https://github.com/Vedanshi-Prajapati)

---

## 📄 License

This project is licensed under the [MIT License](LICENSE) — see the LICENSE file for details.
