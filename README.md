# Server Log Cleaner

A simple bash script that deletes log files older than 14 days from standard Linux and ZimaOS paths, helping keep your server's disk usage under control. Made with laziness by Server Log Cleaner Dev team🦥

## Usage

Make the script executable and run it:

```bash
chmod +x Code-log-Cleaner.sh
sudo ./Code-log-Cleaner.sh
```

Always do a dry run first to preview what will be deleted before actually removing anything:

```bash
sudo ./Code-log-Cleaner.sh --dry-run
```

## Options

| Flag | Description |
|------|-------------|
| `--dry-run` | Preview files that would be deleted without removing anything |
| `--help` | Show usage information |

## What It Cleans

By default the script scans these directories:

| Path | Purpose |
|------|---------|
| `/var/log` | Standard Linux system logs |
| `/root/.casaos/logs` | ZimaOS / CasaOS core logs |
| `/var/lib/casaos/logs` | ZimaOS service logs |
| `/DATA/AppData` | Docker app data |

It only targets files with log-related extensions (`.log`, `.gz`, `.old`, and numbered rotations like `.1`–`.5`), so your actual data files are safe.

## Configuration

At the top of the script you can change:

- `MAX_AGE_DAYS` — how old a file must be before it's deleted (default: `14`)
- `DRY_RUN` — set to `true` to always run in preview mode (default: `false`)
- `LOG_DIRS` — add or remove directories to scan
- `LOG_PATTERNS` — add or remove file extensions to target

## Automating with Cron

To run the script automatically every Saturday at 3 PM:

```bash
sudo crontab -e
```

Add this line:

```
0 15 * * 6 /path/to/Code-log-Cleaner.sh >> /var/log/log_cleaner.log 2>&1
```

## Requirements

- Bash
- `sudo` / root access
- `numfmt` (part of GNU coreutils, installed by default on most Linux systems)
