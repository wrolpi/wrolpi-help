# Primary, Secondary, Tertiary.

WROLPi attempts to integrate all services in an easy to learn interface. But, if the React app is unavailable, secondary
and tertiary options to use your WROLPi may be available.

| Module   | Primary                                   | Secondary                                                                      | Tertiary                                                          |
|----------|-------------------------------------------|--------------------------------------------------------------------------------|-------------------------------------------------------------------|
| System   | [React App](../controller/index.md)       | [Controller](../controller/index.md) on port `:8087`                           | CLI tools (systemctl, mount, etc.)                                |
| Videos   | [React App](../modules/videos/index.md)   | [Open video files with VLC.](../modules/videos/index.md#videos-without-wrolpi) | Open subtitle files with a text editor.                           |
| Archives | [React App](../modules/archives/index.md) | Open Archive files directly with Chromium                                      | Readability files can be opened with a text editor.               |
| Map      | [React App](../modules/map/index.md)      | Map is accessible on port `:8084`                                              | None                                                              |
| Zim      | [React App](../modules/zim/index.md)      | Kiwix server is accessible on port `:8085`                                     | [Kiwix application](../modules/zim/index.md#kiwix-without-wrolpi) |
| Help     | React App                                 | Help server is accessible on port `:8086`                                      | Markdown files are available in `/opt/wrolpi-help/docs`           |
| Tags     | React App                                 | Browse the Tags Directory: `/media/wrolpi/tags`                                | Read the config: `/media/wrolpi/config/tags.yaml`                 |
| Files    | [React App](../modules/files/index.md)    | Browse the files on port `:8443` path `/media` (https://localhost:8443/media)  | Browse the files using the desktop file browser                   |
