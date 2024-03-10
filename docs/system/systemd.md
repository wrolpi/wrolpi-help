# Service Control

WROLPi services are controlled by `systemd`.

You can view and control the WROLPi services using these commands:

| Service   | Status                          | Logs                         | Restart                          | Stop                          | Start                          |
|-----------|---------------------------------|------------------------------|----------------------------------|-------------------------------|--------------------------------|
| API       | `systemctl status wrolpi-api`   | `journalctl -u wrolpi-api`   | `systemctl restart wrolpi-api`   | `systemctl stop wrolpi-api`   | `systemctl start wrolpi-api`   |
| React App | `systemctl status wrolpi-app`   | `journalctl -u wrolpi-app`   | `systemctl restart wrolpi-app`   | `systemctl stop wrolpi-app`   | `systemctl start wrolpi-app`   |
| Map       | `systemctl status renderd`      | `journalctl -u renderd`      | `systemctl restart renderd`      | `systemctl stop renderd`      | `systemctl start renderd`      |
| Zim       | `systemctl status wrolpi-kiwix` | `journalctl -u wrolpi-kiwix` | `systemctl restart wrolpi-kiwix` | `systemctl stop wrolpi-kiwix` | `systemctl start wrolpi-kiwix` |
