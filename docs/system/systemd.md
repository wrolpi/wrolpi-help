# Service Control

WROLPi services can be managed through the [Controller](../controller/services.md) web interface,
or via command line using `systemd`.

## Using the Controller (Recommended)

The Controller provides a web-based interface to start, stop, restart services and view logs.
See [Service Management](../controller/services.md) for details.

## Command Line

For advanced users or scripting, services can be controlled directly with these commands:

| Service    | Status                          | Logs                         | Restart                          | Stop                          | Start                          |
|------------|---------------------------------|------------------------------|----------------------------------|-------------------------------|--------------------------------|
| Controller | `systemctl status wrolpi-controller` | `journalctl -u wrolpi-controller` | `systemctl restart wrolpi-controller` | `systemctl stop wrolpi-controller` | `systemctl start wrolpi-controller` |
| API        | `systemctl status wrolpi-api`   | `journalctl -u wrolpi-api`   | `systemctl restart wrolpi-api`   | `systemctl stop wrolpi-api`   | `systemctl start wrolpi-api`   |
| React App  | `systemctl status wrolpi-app`   | `journalctl -u wrolpi-app`   | `systemctl restart wrolpi-app`   | `systemctl stop wrolpi-app`   | `systemctl start wrolpi-app`   |
| Zim        | `systemctl status wrolpi-kiwix` | `journalctl -u wrolpi-kiwix` | `systemctl restart wrolpi-kiwix` | `systemctl stop wrolpi-kiwix` | `systemctl start wrolpi-kiwix` |
| Caddy      | `systemctl status caddy`        | `journalctl -u caddy`        | `systemctl restart caddy`        | `systemctl stop caddy`        | `systemctl start caddy`        |
| Help       | `systemctl status wrolpi-help`  | `journalctl -u wrolpi-help`  | `systemctl restart wrolpi-help`  | `systemctl stop wrolpi-help`  | `systemctl start wrolpi-help`  |

The SQLite database is a file under `/media/wrolpi/config/` — there is no database systemd service.
Maps are served by Caddy from PMTiles files (no map rendering service).
