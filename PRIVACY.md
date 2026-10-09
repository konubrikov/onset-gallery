# Privacy Policy

**OnSet Gallery**  
Effective Date: October 2026

OnSet Gallery is built with a strict **local-first, privacy-by-design** architecture. We believe that your creative work, photographs, client assets, and shoot metadata should remain entirely under your control.

---

### 1. Zero Cloud Dependency & Local Processing

- **Offline by Design:** OnSet Gallery functions entirely offline without requiring an active internet connection, account registration, or login credentials.
- **Local Execution:** All image ingestion, embedded RAW preview extraction, filmstrip generation, metadata scoring, and duplicate pre-culling occur exclusively on your local computer hardware.
- **No Cloud Uploads:** The application does not upload, sync, mirror, or backup your photographs, raw camera files, session names, or metadata sidecars to any external server or cloud service.

---

### 2. No Telemetry, Tracking, or Analytics

- **No Usage Analytics:** We do not track how you use the application, which buttons you click, how long your sessions last, or how many photos you cull.
- **No Advertising or Profiling:** The application contains no advertising SDKs, tracking pixels, cookies, device fingerprinting, or user profiling tools.
- **No Remote Crash Reporting:** Crash logs and errors are not sent automatically to remote telemetry endpoints. Diagnostic files, if created, remain strictly on your local disk.

---

### 3. Local Data Storage

All application configuration, session indexes, and rating caches are stored exclusively in your user directory:

- **macOS / Linux:** `~/.onset-gallery/`
- **Windows:** `%USERPROFILE%\.onset-gallery\`

This directory may store:
- Local cache indexes of opened session paths and thumbnail references.
- User-assigned ratings (Likes, Favorites, Rejects, Star ratings).
- Local FTP server settings (port and local authentication credentials).

**Data Retention & Removal:**  
Removing a session within OnSet Gallery purges only the local metadata index in `~/.onset-gallery/`. Your original image files in the shoot folder remain completely untouched. To remove all cached data, simply delete the `.onset-gallery` directory from your computer.

---

### 4. Network Activity

The application initiates network communication only under the following user-managed scenarios:

1. **Local Camera FTP Ingest (Optional):** When you enable the built-in FTP receiver, the application opens a local network socket (default port `2121`) on your computer or local Wi-Fi network to accept incoming files directly from your camera body. Credentials and incoming files are processed strictly within your local network and never leave your workstation.
2. **Explicit User Actions:** If you click an external web link (such as documentation, GitHub release downloads, or project support links), the link is opened in your default web browser under your browser's own privacy settings.

---

### 5. Third-Party Access

Because OnSet Gallery does not collect or transmit data to remote servers, no personal information, photographic files, or metadata are ever sold, rented, shared, or disclosed to third-party entities, advertisers, or AI training datasets.

---

### 6. Contact & Inquiries

For questions regarding OnSet Gallery privacy practices, please contact:  
**Nikita Konubrikov** — [konubrikov@gmail.com](mailto:konubrikov@gmail.com)  
Project Repository: [github.com/konubrikov/onset-gallery](https://github.com/konubrikov/onset-gallery)
