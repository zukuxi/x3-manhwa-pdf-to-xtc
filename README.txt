X3 PDF Batch Converter → XTC/XTCH

Files
- index.html: interface, including count/chapter merge modes and three download modes.
- app.js: PDF rendering, XTC/XTCH packing, grouping, preview, download and ZIP logic.

How to use
1. Upload index.html and app.js to the same GitHub Pages directory (overwrite the old versions).
2. Open the page and refresh it. The script URL has a new cache-busting version.
3. Choose PDFs or a folder, set the merge mode and conversion options, then choose a download mode.

Download modes
- Manual download (default): download each output individually or create a ZIP manually.
- Save automatically to a chosen folder: asks for one output folder, writes each completed output there, and releases the in-memory Blob after saving. Requires a browser with File System Access API support, generally a desktop Chromium browser on HTTPS/localhost.
- Create ZIP automatically when finished: creates a ZIP after conversion. ZIP generation can still consume substantial memory for very large batches; direct folder saving is preferable for hundreds of files.

Notes
- All PDF processing happens locally in the browser; files are not uploaded.
- PDF.js and JSZip are loaded from CDNs, so the page needs network access to those resources.
- Folder-save mode is not supported by every mobile browser. The app reports unsupported browsers rather than pretending to save.
- The code was syntax-checked with Node.js, but a full browser conversion test was not run in this environment. Test with a few small PDFs before a large batch.
- Encoding/container structure references srokl/xtcjsapp (MIT). This project is not affiliated with the device manufacturer.
