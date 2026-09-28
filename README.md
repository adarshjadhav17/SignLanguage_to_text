# SignLanguage_to_text
Sign language to text converter converts some sign to text
we have used ASL as our reference

![image](https://github.com/prashantpadhy/SignLanguage_to_text/assets/91092287/19aa3421-f2cf-46d0-a29f-bed1113339e5)
![image](https://github.com/prashantpadhy/SignLanguage_to_text/assets/91092287/938d0261-db3a-49f9-ab02-3852c55da502)
![image](https://github.com/prashantpadhy/SignLanguage_to_text/assets/91092287/21b54244-1b1a-4d1a-bcf3-0d84b2d08e4b)
![image](https://github.com/prashantpadhy/SignLanguage_to_text/assets/91092287/ad78270f-730c-46b2-8163-9500bd19919a)

---

# Real-Time Sign Language to Speech Converter

A computer-vision project that interprets hand gestures and converts them into text and speech, designed to support communication between sign-language users and people unfamiliar with signing. The system uses **OpenCV**, **MediaPipe**, a **Flask web interface**, and **text-to-speech integration**, with American Sign Language (ASL) as its reference.

This overview follows the team's research manuscript, **“Real-Time Sign Language to Speech Converter Using OpenCV and MediaPipe.”** The GitHub repository is an earlier implementation snapshot and does not contain all of the later work described in the paper. In particular, the checked-in code exposes text overlays but does not include the speech-output integration reported in the manuscript.

## Project overview

The project explores a webcam-based interface for recognizing selected signs without specialized gloves or wearable sensors. A user performs a gesture in front of the camera; the system tracks hand landmarks, identifies a matching sign, displays its text, and, in the system described by the paper, converts that text into audible speech.

This is an academic gesture-recognition system. The paper's demonstrated examples should not be interpreted as evidence of complete ASL vocabulary coverage or continuous language translation.

## System described in the paper

- **Image capture and preprocessing:** capture webcam images and prepare them for gesture analysis. The paper describes resizing, grayscale conversion, and noise reduction as preprocessing stages.
- **Hand tracking:** use MediaPipe to locate hand landmarks, including the fingertips and thumb.
- **Gesture recognition:** analyze landmark positions and apply sign-specific conditions to identify gestures. The implementation procedure in the paper describes coordinate-based rules.
- **Text output:** display the recognized sign as readable text.
- **Speech output:** pass the recognized text to a text-to-speech mechanism to produce audible output.
- **Web interface:** provide a camera interaction page alongside About and Contact pages explaining the project and team.

```text
Webcam → Image processing → MediaPipe hand tracking
       → Gesture recognition → Recognized text → Speech output
```

The paper reports real-time demonstrations, including **Stop**, **Like**, and **Dislike**, with text and speech output and minimal perceived lag. It does not provide a reproducible numerical accuracy or latency benchmark, so no quantitative performance claim is made here.

## Research and documentation

**Manuscript:** *Real-Time Sign Language to Speech Converter Using OpenCV and MediaPipe*

**Authors:** Anvisha Pathak, Adarsh Jadhav, Niraj Patil, Smita Rukhande, Prashant Padhy, and Lakshmi Gadhikar.

**Institution:** Fr. Conceicao Rodrigues Institute of Technology, Navi Mumbai, India.

The manuscript is the primary reference for this project's broader system description. The [original undergraduate project report](Group-9_Final%20Report.pdf), already included in this repository, provides additional background, interface screenshots, and implementation examples. The manuscript and the original project report are separate documents; the manuscript PDF is not currently included here.

## What this GitHub snapshot contains

The available code uses Python, OpenCV, MediaPipe Hands, and Flask to capture a webcam stream, apply handwritten coordinate rules, and draw labels and landmarks onto frames streamed to a browser. It also includes Home, Manual, About, and Contact pages and a camera Stop control.

| Category | Labels with rules in `helper.py` |
| --- | --- |
| Letters | A, B, C, D, E, F, G, H, I, J, K, L, O, U, W, X, Y, Z |
| Other gestures | LIKE, DISLIKE, FIST, STOP, ROCK |

This list describes the uploaded code, not the full coverage of the later team implementation. The included manual specifies the right hand. Rules are evaluated per frame, including those labeled J and Z; this snapshot does not implement motion-sequence recognition.

MediaPipe provides hand tracking, while this snapshot classifies gestures through coordinate comparisons. No separate classifier training pipeline or custom model checkpoint is included. The webcam used is attached to the computer running Python, rather than a remote browser's device.

The setup and limitations below apply specifically to **this repository snapshot**. They do not establish the capabilities or limitations of the team's later code.

## Repository contents

| File | Purpose |
| --- | --- |
| `app.py` | Flask page routes, video streaming, and camera stop endpoint |
| `helper.py` | Webcam capture, hand tracking, gesture rules, and frame annotation |
| `sign to text.html` | Main recognition interface |
| `manual.html`, `about.html`, `contact.html` | Supporting pages |
| `style.css` | Interface styling |
| `requirements.txt` | Original pinned Python dependencies |
| [Group-9_Final Report.pdf](Group-9_Final%20Report.pdf) | Original project report, screenshots, and background |

## Local setup

The original report specifies **Python 3.10 and 64-bit Windows**. The dependencies date from 2022, including Flask 2.1.0, MediaPipe 0.8.9.1, and OpenCV 4.5.5.64. Installation depends on package availability for your Python version and platform; this is not a verified setup for modern Python or Apple Silicon.

### 1. Clone and create an environment

```bash
git clone https://github.com/adarshjadhav17/SignLanguage_to_text.git
cd SignLanguage_to_text
python -m venv .venv
```

Activate on Windows PowerShell:

```powershell
.venv\Scripts\Activate.ps1
```

Or on macOS/Linux, if the pinned dependencies support your environment:

```bash
source .venv/bin/activate
```

Install the original dependencies:

```bash
python -m pip install -r requirements.txt
```

### 2. Prepare Flask's expected folders

**The repository currently stores HTML and CSS in its root, but `app.py` uses Flask's default `templates/` and `static/` locations.** Before starting, create those folders and copy the files into them. This command works from the repository root:

```bash
python -c "from pathlib import Path; import shutil; Path('templates').mkdir(exist_ok=True); Path('static').mkdir(exist_ok=True); [shutil.copy2(p, Path('templates') / p.name) for p in Path('.').glob('*.html')]; shutil.copy2('style.css', 'static/style.css')"
```

The resulting local layout should include:

```text
templates/
  sign to text.html
  manual.html
  about.html
  contact.html
static/
  style.css
```

### 3. Start and use the application

```bash
python app.py
```

Open [http://127.0.0.1:5000](http://127.0.0.1:5000). Allow the Python process access to your webcam, keep your right hand visible, and show one of the implemented poses. Recognized text appears directly on the video. Use **Stop** to release the active camera stream and `Ctrl+C` in the terminal to stop the server.

The application runs Flask in debug mode and is intended for local experimentation.


## Original project team

**Anvisha H. Pathak · Niraj Patil · Prashant Padhy · Adarsh Jadhav**

Project supervisor: **Mrs. Smita Rukhande**

Department of Information Technology, Fr. C. Rodrigues Institute of Technology, Vashi, Navi Mumbai; University of Mumbai, academic year **2021–22**.
