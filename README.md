# CloudApp Bash

Basic CloudApp implementation for Linux written in Bash. It will watch a directory for new files, upload to your CloudApp account and copy the share URL to your clipboard.

## Installation

First, you'll need the following:

+ `jq` (required) To handle JSON
+ `inotify-tools` (required) For watching the directory
+ `curl` (required) For sending cURL commands
+ `ffmpeg` (optional) If you plan on having videos converted for you
+ `notify-send` (optional) To send notification to desktop

On Debian-based systems the following should work:

`sudo apt install jq inotify-tools curl ffmpeg libnotify-bin`

Next, create a file in your home directory named `.cloudapp` with the following contents:

```conf
watch_dir=/home/(yourname)/CloudApp # Directory to watch
username="your-email"
password="yout-password"
convert_video=1 # 1 = Convert videos to MP4, 0 = Leave them
notify=1 # 1 = Use notify-send to notify when available in the clipboard.
```

## Running

`chmod +X (path to cloudapp script)`. Then simply add a start script pointing to `cloudapp` script or run directly.

## Tips

### GNOME Screenshot

Change the defautl directory to your CloudApp configured directory:

`gsettings set org.gnome.gnome-screenshot auto-save-directory 'file:///home/(your-name)/(path to your folder in .cloudapp config)'`.
