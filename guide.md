# OnSet Gallery User Guide

[English](guide.md) | [Русский](guide.ru.md) | [README](README.md)

This guide walks you through the setup and core workflow of OnSet Gallery on macOS and Windows, from installation to exporting standardized metadata into Adobe Lightroom Classic and Capture One Pro.

OnSet Gallery operates strictly locally. All session indexes and ratings are stored on your machine in `~/.onset-gallery/` (or `%USERPROFILE%\.onset-gallery` on Windows). Deleting a session within the application removes only the local cached index; your original camera files remain untouched.

---

## 1. Installation & First Launch

Download the latest version from the **[GitHub Releases](https://github.com/konubrikov/onset-gallery/releases)** page.

### macOS (macOS 12 Monterey or newer)
1. Download the `.dmg` package and double-click to mount it.
2. Drag the **OnSet Gallery** icon into your **Applications** folder.
3. **Handling macOS Gatekeeper on First Launch:**
   - Because preview releases do not currently include an Apple Developer ID notarization seal, macOS Gatekeeper may show a warning: *"OnSet Gallery cannot be opened because the developer cannot be verified"*.
   - **Method A (GUI):** In Finder, navigate to **Applications**, right-click (or `Control`-click) **OnSet Gallery**, and select **Open**. In the pop-up security prompt, click **Open**. (Required only once; subsequent launches open directly).
   - **Method B (Terminal):** Clear the quarantine flag via:
     ```bash
     xattr -cr /Applications/OnSetGallery.app
     ```

### Windows (Windows 10 / 11 64-bit)
1. Download the `.msi` or standalone `.exe` installer.
2. Run the installer and proceed through the setup dialogs.
3. **Handling Windows Defender SmartScreen:**
   - For preview builds without an expensive EV code-signing certificate, Windows SmartScreen may display: *"Windows protected your PC"*.
   - Click the **More info** link.
   - Click **Run anyway**.
   - The application starts normally.

---

## 2. Opening a Shoot Folder

Upon launching OnSet Gallery without active sessions, the welcome screen prompts you to designate a shoot directory. The target folder may contain standard JPEGs or camera RAW files (such as `.ARW`, `.CR2`, `.CR3`, `.NEF`). RAW images are rendered using their embedded high-resolution previews for maximum speed.

![Session Selection Screen](guide/01-sessions.png)

You can open a session through multiple methods:

- **Open Folder:** Standard system directory picker. Also accessible via menu **File → Open Folder** or `Ctrl+O` (`⌘O` on macOS).
- **Enter Path:** Direct entry for absolute paths, ideal when navigating network volumes or mounted external drives.
- **Drag & Drop:** Simply drag a folder from Finder or Windows Explorer directly onto the application window.

*Note: Opening a previously scanned folder instantly restores its existing session and cached ratings.*

---

## 3. Image Review and Fast Keyboard Navigation

Opening a session displays the main gallery interface: the current image in high resolution, the bottom filmstrip showing the full sequence, and frame metadata (counter, filename, dimensions) in the status overlay.

![Gallery Review View](guide/03-gallery.png)

OnSet Gallery is designed around single-key keyboard operations:

| Shortcut | Action |
| --- | --- |
| `←` / `→` | Previous / Next image |
| `↑` | **Like** (Green color label) |
| `↓` | **Reject** (Red color label + Rejected flag) |
| `F` | **Favorite** (Yellow color label) |
| `1` – `5` | Assign Star Rating (1 to 5 stars) |
| `Z` | Undo last rating action |
| `G` | Toggle between Filmstrip and Overview Grid |
| `+` / `−` | Zoom in / Zoom out |
| `0` | Fit image to window |
| `Space` | Toggle **Follow Mode** (auto-scroll to newest incoming photos) |
| `Esc` | Return to Session List |

Ratings are reflected immediately on both the active frame and the filmstrip thumbnails:

![Rating a Frame](guide/04-like.png)

### Quick Filters & Reject Management
At the top of the filmstrip, filter chips let you isolate subsets:
- **All Frames**
- **Unmarked Only** (useful for clearing pending queues)
- **Likes** / **Favorites** / **Rejects**

Next to the filters, reject handling modes allow you to streamline your review:
- **Skip Rejects:** Keeps rejected frames in the filmstrip but skips past them during arrow key navigation.
- **Hide Rejects:** Completely hides rejected frames from the filmstrip to prevent redundant reviews.

When shooting tethered or receiving frames via FTP, toggle **Follow Mode** (`Space`) so the gallery automatically jumps to newly incoming frames as the camera writes them to disk.

---

## 4. Overview Grid & Smart Pre-Culling

Press `G` or click the grid icon in the bottom toolbar to switch into the Overview Grid. This view allows you to inspect entire burst sequences and spot subtle variations in pose or expression.

![Overview Grid View](guide/05-grid.png)

### Automated Pre-Cull
When shooting rapid bursts, repetitive frames accumulate quickly. The **Pre-cull** feature executes a local, hardware-accelerated analysis of the active session:

- **Technical Analysis:** Evaluates sharpness, motion blur, and exposure consistency across consecutive frames.
- **Facial Evaluation (macOS):** On macOS, the analyzer detects closed eyes and unfavorable facial expressions within similar takes. On Windows, pre-cull focuses on optical and exposure metrics.
- **Safe Evaluation:** Pre-cull never overrides ratings you have manually set, and always ensures top candidate frames within any burst series remain unflagged.
- **100% Local:** All calculations execute directly on your processor without cloud transmission.

---

## 5. Exporting to Adobe Lightroom Classic & Capture One Pro

Click the **Export** button in the upper toolbar to transfer your on-set selections to your editing catalog.

![Metadata Export Dialog](guide/06-export.png)

### Export Modes

1. **Write XMP Alongside Files:**
   - For RAW files, OnSet Gallery generates standardized `.xmp` sidecar files in the source directory.
   - For standalone JPEGs (without a corresponding RAW), metadata tags are written into the file headers.
   - If an existing `.xmp` sidecar is present (for example, containing prior camera profiles or crop data), OnSet Gallery updates only ratings and color labels, preserving existing development settings.
2. **Save XMP ZIP Archive:**
   - Bundles all generated `.xmp` sidecars into a single compressed `.zip` archive. Ideal for transferring curation data to an offsite retoucher or secondary workstation.
3. **Copy Filename List:**
   - Copies the filenames of selected frames (All, Likes, Favorites, or Likes + Favorites) directly to the system clipboard for immediate catalog filtering.

### Reading Metadata in Catalogs

#### Adobe Lightroom Classic
1. Select the target folder in the Library module.
2. In the top menu, choose **Metadata → Read Metadata from Files**.
3. Lightroom applies the ratings and color labels to your catalog items.
4. *Alternative:* Choose **Library → Find by Filename → Contains** and paste the copied filename list.

#### Capture One Pro
1. Under **Preferences → Image → Metadata**, verify that Sidecar XMP sync is enabled (prefer **Sync** or **Auto Sync**).
2. To load by filename: Go to **Select → Select By → Filename List** and paste the copied list from OnSet Gallery.

### Metadata Translation Table

| OnSet Gallery | XMP Metadata Tag | Lightroom Classic | Capture One Pro |
| --- | --- | --- | --- |
| **Like** (`↑`) | `xmp:Label="Green"` | Green Label | Green Label |
| **Favorite** (`F`) | `xmp:Label="Yellow"` | Yellow Label | Yellow Label |
| **Reject** (`↓`) | `xmp:Label="Red"` + Reject Flag | Red Label / Rejected | Red Label / Rejected |
| **Stars** (`1`–`5`) | `xmp:Rating="1..5"` | 1 to 5 Stars | 1 to 5 Stars |

---

## 6. Direct Camera Ingest via Wi-Fi FTP

Modern mirrorless cameras (Sony Alpha, Canon EOS, Nikon Z) feature built-in Wi-Fi FTP background transfer. OnSet Gallery includes an embedded FTP receiver, allowing direct ingest to your workstation without third-party FTP utilities.

1. In the session manager, click the **FTP** button to launch the server configuration dialog.
2. The dialog displays your local workstation IP address, listening port (default `2121`), and local credentials.
3. Configure your camera's FTP transfer settings with these matching parameters.
4. Set the camera destination directory to your active shoot session folder.
5. In OnSet Gallery, open the session and enable **Follow Mode** (`Space`). New frames will appear instantly on screen as they complete transfer.

*Security Note: The FTP server listens on your local network interface only. Credentials and network communications remain strictly confined to your local Wi-Fi / Ethernet connection.*

---

## 7. Technical Specifications & Limits

- **Folder Depth:** Folder scanning traverses directories up to 6 levels deep.
- **Batch Capacity:** Optimized for up to 4,000 frames per session pass.
- **RAW Handling:** Fast rendering utilizes embedded JPEG previews stored within RAW files (no demosaicing delay).
- **Supported Formats:** Standard JPEG (`.jpg`, `.jpeg`) and major camera RAW formats (`.arw`, `.cr2`, `.cr3`, `.nef`, `.dng`, `.orf`, `.rw2`).
- **Data Protection:** Original media files are never moved, renamed, or deleted by the application.
