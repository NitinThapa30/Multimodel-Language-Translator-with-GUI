<div align="center">

#  Multi-Modal Language Translator

A cross-platform desktop application that translates **Text**, **Speech**, and **Images** offline — built with **Qt/QML + C++** for the GUI and **Python** for the translation engine.

![Status](https://img.shields.io/badge/status-active-success)
![Platform](https://img.shields.io/badge/platform-Windows%20%7C%20Linux%20%7C%20macOS-blue)
![License](https://img.shields.io/badge/license-Academic%20Project-lightgrey)

🔗 [**View Repository**](https://github.com/NitinThapa30/Multimodel-Language-Translator-with-GUI)

</div>

---

<div align="center">

## 📖 Overview

</div>

Language is the bridge that connects people, cultures, and ideas — but it can also be a barrier. The **Multi-Modal Language Translator** breaks that barrier by combining **text, speech, and image-based translation** into a single, offline-capable desktop application with a sleek, modern UI.

Whether you're decoding a foreign menu, translating a conversation on the fly, or extracting text from a photo, this app handles it — all without needing an internet connection.

---

<div align="center">

## ✨ Features

</div>

- 📝 **Text-to-Text Translation** — type and translate instantly
- 🎙️ **Speech-to-Text Translation** — speak and get translated text
- 🖼️ **Image-to-Text Translation** — upload an image, extract text via OCR, and translate it
- 🌙 **Dark Mode / Light Mode** toggle
- 🔄 **Language Swap** button for quick source ↔ target switching
- 🕘 **Translation History** — view and delete recent translations (SQLite3-backed)
- 📊 **Language Facts Sidebar** — fun facts about the selected languages
- 🐞 **Built-in Issue Reporting** form
- 🔌 **Offline Functionality** — no internet dependency for core translation tasks

---

<div align="center">

## 🏗️ Architecture



The application uses a **hybrid Python–C++ architecture**:

```
User Interaction (Qt/QML Frontend)
            │
            ▼
    C++ Backend Logic (Qt Framework)
            │
            ▼
  Python Process (Argos Translate, SpeechRecognition, EasyOCR, OpenCV)
            │
            ▼
     Return Processed Data
            │
            ▼
   Qt/QML GUI (Display Output)
```
</div align="center">

**Bridging strategies explored:**

<div align="center">

| Approach | Description |
|---|---|
| **Pybind11** | Wraps Python functions as native C++ callable modules |
| **Monolithic (IPC/Process-based)** | C++ launches Python as a subprocess via `QProcess`, exchanging data via stdout/stdin |
| **Qt/QML → C++ → Python** | C++ acts as an intermediary layer between the QML frontend and Python backend |

</div>

The shipped implementation uses the **`QProcess`-based monolithic approach**, where C++ spawns `translator.py` with mode-specific arguments and parses its output.

---

<div align="center">

## 🛠️ Tech Stack

</div>

### Frontend (GUI)
- **Qt Framework** (C++ + QML)
- `QtQuick`, `QtQuick.Controls`, `QtQuick.Controls.Material`, `QtQuick.Layouts`, `QtQuick.Dialogs`

### Backend (Processing)
- **Python 3**
- [`argostranslate`](https://github.com/argosopentech/argos-translate) — offline text-to-text translation
- [`SpeechRecognition`](https://pypi.org/project/SpeechRecognition/) — speech-to-text conversion
- [`EasyOCR`](https://github.com/JaidedAI/EasyOCR) — image-to-text (OCR)
- [`OpenCV (cv2)`](https://opencv.org/) — image preprocessing
- [`SQLite3`](https://www.sqlite.org/) — local storage for translation history

### Bridge
- `QProcess` (C++ ↔ Python subprocess communication)
- `Pybind11` *(explored as an alternative integration method)*

---

## 📂 Project Structure

```
Multimodel-Language-Translator-with-GUI/
├── main.qml                        # Primary QML UI (mode selection, translation, sidebar)
├── main2.qml
├── ReportPage.qml                  # "Report an Issue" page
├── RecentTranslationsPage.qml
├── SocialMediaButton.qml
├── translator.cpp / translator.h   # C++ <-> Python bridge (QProcess)
├── database.py                     # SQLite3 wrapper for translation history
├── translator.py                   # Python translation engine (text/speech/image modes)
├── resources.qrc / qml.qrc         # Qt resource files
└── tra.pro                         # Qt project file
```

---

<div align="center">

## ⚙️ How It Works

</div>

### 1. Text Translation
```
User Input → Argos Translate → Translated Output
```

### 2. Speech Translation
```
Microphone Input → SpeechRecognition (Speech-to-Text) → Argos Translate → Translated Output
```

### 3. Image Translation
```
Image Upload → OpenCV (Preprocessing) → EasyOCR (Text Extraction) → Argos Translate → Translated Output
```

All translations are automatically saved to a local **SQLite3 database** and can be viewed or cleared from the sidebar.

---

<div align="center">

## 🚀 Getting Started

</div>

### Prerequisites
- Qt Creator (Qt 5.15+ recommended) with QML support
- Python 3.8+
- pip packages:
  ```bash
  pip install argostranslate SpeechRecognition easyocr opencv-python pyaudio
  ```

### Setup
1. Clone the repository:
   ```bash
   git clone https://github.com/NitinThapa30/Multimodel-Language-Translator-with-GUI.git
   ```
2. Open `tra.pro` in **Qt Creator**.
3. Make sure `translator.py` and `database.py` are accessible at the path referenced in `translator.cpp` (via `QProcess`).
4. Build and run the project from Qt Creator.
5. On first run, Argos Translate will download the required offline language packages.

---

<div align="center">

## 🖥️ Screenshots

| Light Mode | Dark Mode |
|---|---|
| Clean, minimal text translation interface | Sidebar with recent translations & language facts |

</div>

*(See the full project report for detailed UI walkthroughs — front page, sidebar, recent translations, image/speech modes, credits, and issue reporting.)*

---

<div align="center">

## ⚠️ Limitations

</div>

- Translation accuracy depends on Argos Translate's offline models (may struggle with idioms/complex sentences)
- OCR accuracy varies with image quality, fonts, and resolution
- Speech recognition performance drops in noisy environments or with strong accents
- Limited language coverage compared to commercial cloud-based translators
- C++ ↔ Python process calls introduce some performance overhead
- No advanced features like contextual learning or handwriting recognition (yet)

---

<div align="center">

## 🔮 Future Improvements

</div>

- Real-time/live translation mode
- Expanded language support
- Integration with modern AI/LLM-based translation models
- Improved OCR accuracy for stylized or low-res text
- Enhanced data privacy and local-only audio handling

---

<div align="center">

## 👥 Contributors

| Name | Roll No. |
|---|---|
| **Nitin Thapa** | 22082050015 |
| Vansh Kumar | 22082050028 |
| Saurav Kumar | 22082050023 |

**Submitted to:** Ms. Vishakha Sharma, Assistant Professor
**Institution:** GRD Institute of Polytechnic, Rajpur, Dehradun, Uttarakhand
**Department:** Computer Science & Engineering

</div>

---

<div align="center">

## 🙏 Acknowledgements

</div>

Built with gratitude to the open-source community behind **Qt**, **Argos Translate**, **EasyOCR**, **OpenCV**, and **SQLite3** — whose tools made offline, multimodal translation possible.

---

<div align="center">

## 📄 License

This project was developed as an academic minor project. Feel free to explore, learn from, and build upon it for educational purposes.

</div>
