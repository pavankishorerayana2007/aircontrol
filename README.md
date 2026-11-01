# AirControl AI — Vercel-ready package

## Important architecture note

This project has two parts:

- `site/` is the static web dashboard. Deploy **this folder** to Vercel.
- `agent/` is the Python desktop agent. It must run on the Windows laptop whose webcam and mouse you want to control.

The Python agent cannot run as a Vercel Function: Vercel runs server-side functions in the cloud, which cannot access your laptop's webcam, physical mouse, or keyboard. This project therefore does not need a FastAPI/API endpoint on Vercel.

## Deploy the website to Vercel

1. Extract this ZIP.
2. Push the `aircontrol-ai-final` folder to GitHub.
3. In Vercel, import that repository.
4. In **Root Directory**, select `site`.
5. Framework Preset: **Other**.
6. Build Command: leave empty.
7. Output Directory: leave empty (or `.` if Vercel requires a value).
8. Deploy.

`site/vercel.json` is included for static-site routing/headers.

## Run real hand control on your Windows laptop

For actual webcam and mouse control, run the local dashboard/agent on the same laptop:

1. Install Python 3.12 if it is not installed.
2. Double-click `agent/run_windows.bat`.
3. Keep the terminal window open.
4. It opens the local dashboard at `http://127.0.0.1:8766`.
5. Use that local dashboard and press **Start sensing**.

The hosted Vercel page can be used to view the interface/preview. A normal HTTPS website cannot reliably connect to the desktop agent's plain `ws://127.0.0.1:8765` WebSocket because browsers restrict insecure WebSockets from HTTPS pages. The local dashboard is provided for the real-control workflow.

## Safety and privacy

Camera processing happens locally on the laptop. Do not expose the desktop agent port to the public internet. Only run the agent on a computer you own or are authorized to control.

## Original project files

- `agent/aircontrol_agent.py` — local Python desktop agent
- `agent/requirements.txt` — Python dependencies
- `agent/run_windows.bat` — Windows launcher
- `site/index.html` — dashboard UI
