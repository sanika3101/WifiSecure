# WiFiGuard

**A Wi-Fi safety project — AI-based risk detection for public/unknown Wi-Fi networks.**

## The Problem

Connecting to unknown Wi-Fi (airports, cafes, hotels) exposes users to real risks: evil twin networks (fake copies of a real hotspot), man-in-the-middle attacks, and open/unencrypted connections that let others read traffic. Most users have no way to tell a safe network from a dangerous one just by looking at its name.

## The Idea

WiFiGuard scans nearby Wi-Fi networks, scores each one for risk using a trained machine learning model, alerts the user in plain language when something looks suspicious, recommends a nearby trusted network based on connection history, and prompts the user to enable a VPN to protect their data when risk is detected.

## Current Status

This repository currently contains the **website demo** — a browser cannot scan real nearby Wi-Fi networks (a browser security restriction), so this stage uses simulated data to demonstrate the full concept: the scan animation, risk scoring, evil-twin alert, and safe-network recommendation.

**Roadmap:**
- [x] Website demo with simulated scan (current)
- [ ] Train risk-detection ML model on real Wi-Fi attack data (AWID/AWID3 dataset)
- [ ] Build Android app with real on-device Wi-Fi scanning (WifiManager API)
- [ ] Integrate trained model on-device (TensorFlow Lite)
- [ ] Add crowd-sourced trusted-network history
- [ ] Add auto-VPN prompt on detected risk

## Model Training Notes

A first Random Forest model was trained on AWID3 data (Evil_Twin + Rogue_AP capture files), combining normal and attack-labeled Wi-Fi frames.

- **Data leakage caught and fixed:** the first version of the model scored a suspicious 100% — investigation showed it had learned to recognize one specific device's MAC address (`wlan.ra`) rather than real attack behavior, since all attack rows in that capture happened to come from the same device. This column (and other identifier/raw-timestamp columns) was removed before retraining.
- **Known limitation:** even after the fix, the model still scores very highly on this dataset. This is expected — the data was captured in a controlled lab setup using one specific attack tool, with a small number of attack examples (166 rows, 33 in the test set). This means the model reliably recognizes *this particular attack signature*, but hasn't yet been proven against more diverse, real-world rogue AP/evil twin behavior. Testing on additional capture sessions is a clear next step before treating this as production-ready.

## Tech Stack

- **Website:** HTML, CSS, JavaScript
- **Model training:** Python, scikit-learn, Google Colab (free)
- **Dataset:** AWID/AWID3 public Wi-Fi intrusion dataset
- **Planned app:** Android (Kotlin/Java), TensorFlow Lite
- **Hosting:** GitHub Pages (free)

## What This Is Not

WiFiGuard detects risk and guides the user toward safer choices (a recommended network, a VPN prompt) — it does not block or intercept an attack directly. This is an accurate and important distinction for how the project is presented.

## Author

Sanika — Computer Science Engineering student, built as a cybersecurity + AI college project.
