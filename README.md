# WorkTrackr installers

One-click installers for **WorkTrackr**, a local activity tracker and timesheet. Java is bundled inside each installer, so there is nothing else to install.

WorkTrackr runs entirely on your own machine. Nothing is sent anywhere.

## Download

Get the latest installer from the [releases page](https://github.com/Akshaydesai221/WorkTrackr-Installers/releases/latest):

- **Windows:** `WorkTrackr-1.0.0-windows-x64-installer.exe`
- **Linux (Ubuntu):** `WorkTrackr-1.0.0-linux-x64-installer.run`

## Windows

1. Download and run the `.exe`. No administrator rights are needed.
2. Choose an install folder and a **web port** (default `8081`). Change the port only if `8081` is already in use.
3. Finish. WorkTrackr starts immediately, runs hidden in the background, and starts on its own every time you log in.
4. Open the dashboard from the Start Menu (**WorkTrackr > Open WorkTrackr**) or browse to `http://localhost:<port>/`.
5. On first launch the dashboard asks you to create an admin account.

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

Open the dashboard at `http://localhost:<port>/` and create an admin account on first launch.

## Uninstall

- **Windows:** Start Menu **WorkTrackr > Uninstall WorkTrackr**, or run `uninstall.exe` in the install folder.
- **Linux:** run `~/WorkTrackr/uninstall` (or the uninstaller in your chosen folder).

Uninstalling stops the app and removes auto-start, but leaves the `data` folder in place so your history is not lost. Delete the install folder manually if you want it gone.

## Notes

- Your data lives in the `data` folder inside the install directory. Back it up to keep your history.
- Only one copy can run at a time.
- The web UI and timesheet work even without the tracking tools; you would just miss automatic activity capture.
