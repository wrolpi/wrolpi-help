# Variables

## API Variables

The behavior of the API can be modified by adding an environment variable file at `/opt/wrolpi/.env`

### Downloads

Download behavior can be modified by using these variables:

| Name                            | Type  | Default Value |
|---------------------------------|-------|---------------|
| `SIMULTANEOUS_DOWNLOAD_DOMAINS` | `Int` | 4             |

### Database

Connecting to the database can be modified using these variables:

| Name          | Type     | Default Value |
|---------------|----------|---------------|
| `DB_HOST`     | `String` | '127.0.0.1'   |
| `DB_PORT`     | `Int`    | 5432          |
| `DB_NAME`     | `String` | 'wrolpi'      |
| `DB_USER`     | `String` | 'wrolpi'      |
| `DB_PASSWORD` | `String` | 'wrolpi'      |

### Raspberry Pi

Raspberry Pi behavior can be modified by using these variables:

| Name                    | Type     | Default Value |
|-------------------------|----------|---------------|
| `DEFAULT_CPU_FREQUENCY` | `String` | 'ondemand'    |
