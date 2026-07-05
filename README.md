# WorkTrackr installers

One-click installers for **WorkTrackr**, a local activity tracker and timesheet. Java is bundled inside each installer, so there is nothing else to install.

WorkTrackr runs entirely on your own machine. Your activity never leaves your computer; only the optional integrations below send anything out, and only what they need.

## Download

Get the latest installer from the [releases page](https://github.com/Akshaydesai221/WorkTrackr-Installers/releases/latest):

- **Windows:** `WorkTrackr-1.0.0-windows-x64-installer.exe`
- **Linux (Ubuntu):** `WorkTrackr-1.0.0-linux-x64-installer.run`

## What it does

- Records the app and window you are using in the background and turns it into a clear timesheet.
- Rolls your day up into an application summary and an hour-by-hour view.
- Suggests timesheet entries from your tracked activity, which you can edit however you like, and export as CSV.
- Optional integrations add detail: web activity, calendar meetings, code activity and issue tracking.

## Windows

1. Download and run the `.exe`. No administrator rights are needed.
2. Choose an install folder and a **web port** (default `8081`). Change the port only if `8081` is already in use.
3. Finish. WorkTrackr starts immediately, runs hidden in the background, and starts on its own every time you log in.
4. Open the dashboard from the Start Menu (**WorkTrackr > Open WorkTrackr**) or browse to `http://localhost:<port>/`.
5. On first launch the dashboard asks you to create an admin account (a new install starts with the login `1` / `1`).

Start Menu folder **WorkTrackr**: Open, Start, Stop, Uninstall.

## Linux (Ubuntu)

Run the installer as your **normal user** (not with `sudo`) so it installs under your home directory and registers a per-user startup service for your account.

```bash
chmod +x WorkTrackr-1.0.0-linux-x64-installer.run
./WorkTrackr-1.0.0-linux-x64-installer.run
```

Choose an install folder and a web port (default `8081`).

Activity tracking needs a few tools and an X11 session:

```bash
sudo apt update
sudo apt install -y xdotool x11-utils xprintidle
```

Modern Ubuntu defaults to Wayland, which blocks reading other windows. At the login screen click the gear icon and choose **Ubuntu on Xorg**. Check with `echo $XDG_SESSION_TYPE` (should print `x11`).

If auto-start did not kick in, open a terminal in the install folder and run `./install-autostart-linux.sh` once.

## Optional integrations (all set up in Settings)

Everything below is optional. WorkTrackr works fully without any of it. Each has step-by-step help on its Settings screen.

- **Google Calendar** — click "Continue with Google" and sign in. It reads your events (read-only) and lists your meetings, ready to add to your timesheet. Browser video calls (Google Meet, Microsoft Teams, Zoom) are detected automatically even without this.
- **AI (Google Gemini, free)** — get a free key at [aistudio.google.com/apikey](https://aistudio.google.com/apikey), paste it into Settings, and WorkTrackr will rewrite your timesheet comments and write the hourly summaries. Anthropic Claude is also supported.
- **Redmine** — enter your Redmine base URL (e.g. `https://redmine.yourcompany.com`) and your API key (Redmine > My account > API access key), then click Test Connection. You can push timesheet hours to Redmine as time entries.
- **GitHub** — add a read-only personal access token to pull in your commits, pull requests, reviews and issues.
- **Browser extension (bundled)** — a companion Chrome/Edge extension adds per-site web activity, so a day in the browser becomes real named activity instead of a blur. It is included with the install (see below).

Privacy: before any text is sent to an AI provider, URLs, emails, domain names and your own redaction terms are stripped, so client and company names stay on your machine.

## Browser extension (optional)

The extension is installed alongside the app in the `browser-extension` folder inside your install directory. To load it:

1. Open your browser's extensions page: `chrome://extensions` (Chrome) or `edge://extensions` (Edge).
2. Turn on **Developer mode** (top right).
3. Click **Load unpacked** and select the `browser-extension` folder in your WorkTrackr install directory.
4. That is it. It talks to WorkTrackr on `http://localhost:8081` by default. If you installed WorkTrackr on a different port, open the extension's popup (its icon in the toolbar) and set the matching address.

The extension only reads the active tab's URL, domain, title and idle/engagement state, and sends it to WorkTrackr on your own machine. Nothing goes anywhere else.

## Uninstall

- **Windows:** Start Menu **WorkTrackr > Uninstall WorkTrackr**, or run `uninstall.exe` in the install folder.
- **Linux:** run the `uninstall` in your chosen folder.

Uninstalling stops the app and removes auto-start, but leaves the `data` folder in place so your history is not lost. Delete the install folder manually if you want it gone.

## Notes

- Your data lives in the `data` folder inside the install directory. Back it up to keep your history.
- Only one copy can run at a time.
- The web UI and timesheet work even without the tracking tools; you would just miss automatic activity capture.
