# Logs

Service logs can be viewed through the [Controller](../controller/services.md#viewing-service-logs)
web interface, or via command line using `journalctl`.

## Using the Controller

Click the **Logs** button next to any service in the Controller to view its recent log output.
See [Viewing Service Logs](../controller/services.md#viewing-service-logs) for details.

## Command Line

The following is a simple overview to view the logs of the [WROLPi Services](index.md#services). WROLPi logs are
gathered by `systemd`. Logs are viewed using `journalctl`.

You can watch all the logs on your WROLPi:

```shell
journalctl -f
```

More detailed logs can be viewed:

```shell
journalctl -f -p debug
```

To view logs only from the most recent boot:

```shell
journalctl -f -b
```

The above commands use `-f` (follow) which will display logs as soon as they are created. You can view older logs by
removing `-f` from the command, but you will need to use your keyboard to navigate the logs. Use `up`, `down`,
`page-up` and `page-down` keys. You can also use `g` to navigate to the top of the log, and `shift-g` to navigate to
the bottom of the logs.

## API

To watch the API logs:

```shell
journalctl -f -u wrolpi-api
```

## React App

To watch the React App logs:

```shell
journalctl -f -u wrolpi-app
```

## Map

To watch the Map logs:

```shell
journalctl -f -u renderd
```

## Zim

To watch the React App logs:

```shell
journalctl -f -u wrolpi-kiwix
```
