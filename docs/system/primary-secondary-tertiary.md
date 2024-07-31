# Primary, Secondary, Tertiary.

WROLPi attempts to integrate all services in an easy to learn interface. But, if the React app is unavailable, secondary
and tertiary options to use your WROLPi may be available.

| Module   | Primary                                   | Secondary                                                                      | Tertiary                                                          |
|----------|-------------------------------------------|--------------------------------------------------------------------------------|-------------------------------------------------------------------|
| Videos   | [React App](../modules/videos/index.md)   | [Open video files with VLC.](../modules/videos/index.md#videos-without-wrolpi) | Open subtitle files with a text editor.                           |
| Archives | [React App](../modules/archives/index.md) | Open Archive files directly with Chromium                                      | Readability files can be opened with a text editor.               |
| Map      | [React App](../modules/map/index.md)      | Map is directly accessible on port `:8084`                                     | None                                                              |
| Zim      | [React App](../modules/zim/index.md)      | Kiwix server is directly accessible on port `:8085`                            | [Kiwix application](../modules/zim/index.md#kiwix-without-wrolpi) |
| Help     | React App                                 | Help server is directly accessible on port `:8086`                             | Markdown files are available in `/opt/wrolpi-help/docs`           |
| Tags     | React App                                 | Browse the Tags Directory: `/media/wrolpi/tags`                                | Read the config: `/media/wrolpi/config/tags.yaml`                 |