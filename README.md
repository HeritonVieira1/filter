# Filter — List Cleaning Tool for Bug Bounty & Pentesting

**Filter** is a lightweight and efficient command-line tool designed to clean large URL or file lists commonly used in security testing, bug bounty, recon and pentest workflows. It automatically removes lines containing irrelevant file extensions (images, videos, fonts, documents, assets, etc.) so you can focus only on actionable targets such as endpoints, directories, APIs, and backend routes.

---

## ⚙️ Quick Installation

### **1. Download the binary**
```
curl -L https://github.com/HeritonVieira1/filter.git -o filter
```

### **2. Make it executable**
```
chmod +x filter
```

### **3. Move it to your system binary path**
```
sudo mv filter /usr/local/bin/
```

### **4. Test**
```
filter -h
```

Now the command `filter` is available globally.

---

## 📌 Basic Usage

### **Filter a file**
```
filter urls.txt
```

### **Filter via pipe (stdin)**
```
cat urls.txt | filter
```

Only relevant lines will remain.

---

## ❌ Extensions Automatically Removed

Filter removes lines ending with the following (default) extensions:

- **Images:** png, jpg, jpeg, gif, webp, svg, ico, bmp, tiff, psd, raw
- **Videos:** mp4, mkv, avi, mov, wmv, flv, webm
- **Audio:** mp3, wav, flac, ogg, aac
- **Documents:** pdf, doc, docx, xls, xlsx, ppt, pptx
- **Archives:** zip, rar, 7z, tar, gz, bz2
- **Web assets:** css, js, map, ttf, woff, woff2, eot
- **Executables:** exe, dll, so, bin, dat
- **Temporary files:** tmp, cache, log, bak

These files are usually noise during recon, where the goal is to find potential attack surfaces.

---

## 🆘 Help Menu (`filter -h`)

```
Usage: filter [options] [file]

Options:
  -v                     Verbose mode (shows removed lines)
  --keep ext1,ext2       Keep ONLY the specified extensions (whitelist mode)
  --config file.txt      Load custom extensions to exclude
  -h, --help             Show this help menu

Examples:
  filter urls.txt
  cat urls.txt | filter
  filter --keep php,js urls.txt
  filter --config exts.txt urls.txt
```

---

## 🔎 Detailed Explanation of Each Option

### **1. `-v` — Verbose Mode**
Shows each removed line so you can understand how Filter is processing your data.

**Example:**
```
filter -v urls.txt
```
Output example:
```
[REMOVED] /static/logo.png
[REMOVED] /assets/main.css
```

Useful for debugging or fine-tuning your extension lists.

---

### **2. `--keep ext1,ext2` — Whitelist Mode**
Instead of removing known irrelevant extensions, this mode keeps **only** the extensions you specify.

**Usage:**
```
filter --keep php,js urls.txt
```

**Input:**
```
/index.php
/app.js
/logo.png
/main.css
```

**Output:**
```
/index.php
/app.js
```

Use this when you only care about backend files, specific tech stacks, etc.

---

### **3. `--config file.txt` — Load Custom Exclusion List**
Allows you to create an external file containing extensions you want Filter to exclude.

Example `exts.txt`:
```
png
jpg
css
pdf
ttf
```

**Usage:**
```
filter --config exts.txt urls.txt
```

Great for customizing behavior or using different profiles (web, mobile, API, assets-only, etc.).

---

### **4. `-h`, `--help` — Display Help**
Shows the help menu and exits.

**Usage:**
```
filter -h
```

---

## 🧪 Practical Usage Examples

### **1. Basic filtering**
```
filter hosts.txt
```

### **2. Using pipelines**
```
cat urls.txt | filter
```

### **3. Only keep PHP and JS files**
```
filter --keep php,js urls.txt
```

### **4. Load custom config**
```
filter --config exts.txt urls.txt
```

### **5. Debug removed entries**
```
filter -v urls.txt
```

---

## ✔️ License
MIT License — free for use and modification.

---

## 💬 Contributing
Pull requests and improvements are welcome!

If you want, I can also generate:
- An **English README optimized for GitHub**
- Badges (build, version, license, contributions)
- A project logo (SVG)
- A GIF demonstrating usage
- A full CHANGELOG
- Release templates

