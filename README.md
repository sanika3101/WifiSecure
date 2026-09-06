# WifiSecure

A Wi-Fi risk-assessment website for a cybersecurity + AI academic project.

## Current website

The GitHub Pages website uses **simulated Wi-Fi network data** because a normal browser cannot freely scan nearby Wi-Fi networks.

The demo now provides:
- 0–100 transparent risk scoring
- Low / Medium / High risk classification
- Dynamic explanations and factor weights
- Network details
- Simulated Evil Twin detection
- Network comparison
- Local scan history
- Educational HTTPS/VPN guidance
- Responsive UI
- Clear demo/safety disclaimer

## Risk engine

The main dashboard uses a transparent **rule-based risk engine** so that every score can be explained. The separate `model.html` page demonstrates the existing trained Random Forest model on captured sample feature rows.

The rule-based dashboard does not claim that its score is produced by machine learning.

## Safety

No real Wi-Fi attack, Evil Twin deployment, packet interception, or nearby-network scanning is performed by this website. Evil Twin behavior is simulated for education.

## Deploy

Upload the contents of this repository to GitHub Pages, or push the updated files to the `main` branch if Pages is configured from the repository root.
