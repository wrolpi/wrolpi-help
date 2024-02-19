# Service Control

You can view and control the WROLPi services using these commands:

| Service   | Status                          | Logs                      | Restart                          | Stop                          | Start                          |
|-----------|---------------------------------|---------------------------|----------------------------------|-------------------------------|--------------------------------|
| API       | `systemctl status wrolpi-api`   | `journalctl wrolpi-api`   | `systemctl restart wrolpi-api`   | `systemctl stop wrolpi-api`   | `systemctl start wrolpi-api`   |
| React App | `systemctl status wrolpi-app`   | `journalctl wrolpi-app`   | `systemctl restart wrolpi-app`   | `systemctl stop wrolpi-app`   | `systemctl start wrolpi-app`   |
| Map       | `systemctl status renderd`      | `journalctl renderd`      | `systemctl restart renderd`      | `systemctl stop renderd`      | `systemctl start renderd`      |
| Zim       | `systemctl status wrolpi-kiwix` | `journalctl wrolpi-kiwix` | `systemctl restart wrolpi-kiwix` | `systemctl stop wrolpi-kiwix` | `systemctl start wrolpi-kiwix` |
