# CloudApp Bash

Basic CloudApp implementation for Linux written in Bash.

This script will watch a set directory for new files (created or moved into the directory). It will then upload to your CloudApp account and copy the share URL to your clipboard.

Currently, CloudApp has no native Linux client. The advantage of this script is its completely agnostic; you can use any screenshot software, recording software, or simply drop files into the watched directory and it will process them for you.

![Sample](sample.gif?raw=true "Sample")

## Installation

First, you'll need the following libraries:

+ `jq` (required) To handle JSON
+ `inotify-tools` (required) For watching the directory
+ `curl` (required) For sending cURL commands
+ `ffmpeg` (optional) If you plan on having videos converted for you
+ `notify-send` (optional) To send notification to desktop

On Debian-based systems the following will work:

`sudo apt install jq inotify-tools curl ffmpeg libnotify-bin`

Next, create a file in your `$XDG_CONFIG_HOME/cloudapp-bash/config` (ex: `~/.config/cloudapp-bash/config`) directory named `.cloudapp` with the following contents:

```conf
watch_dir=/home/(yourname)/CloudApp # Directory to watch
username="your-email"
password="yout-password"
convert_video=1 # 1 = Convert videos to MP4, 0 = Leave them as-is
notify=1 # 1 = Use notify-send to notify when available in the clipboard, 0 = Ignore clipboard action
```

## Usage

`chmod +X (path to cloudapp script)`. Then simply add a start script pointing to `cloudapp watch` script or run directly to start watching.

```bash
$ ./cloudapp 
Usage: ./cloudapp {watch|recent|copy-recent}
  watch - Watches files in the configured directory to upload
  recent - Lists your most recent uploads in table format
  copy-recent - Copy the most recent upload to the clipboard
```

## Tips

### GNOME Screenshot

Change the default directory to your CloudApp configured directory:

`gsettings set org.gnome.gnome-screenshot auto-save-directory 'file:///home/(your-name)/(path to your folder in .cloudapp config)'`.
