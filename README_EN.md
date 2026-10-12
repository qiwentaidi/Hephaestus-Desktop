<div align="center">
<a href="https://github.com/qiwentaidi/Hephaestus-Desktop"><img src="assets/appicon.png" width="120"/></a>
</div>
<h1 align="center">Hephaestus Desktop</h1>

<div align="center">
  <a href="README.md">中文</a> •
  <a href="README_EN.md">English</a>
</div>
<br />

Hephaestus Desktop is the desktop client for [Hephaestus](https://github.com/qiwentaidi/Hephaestus). It combines attack surface assessment, AI penetration testing conversations, asset and vulnerability management, and a launcher for local tools. An embedded local service and SQLite database make it suitable for security testing on a single machine and integration with local tools.

- Desktop downloads: [Releases](https://github.com/qiwentaidi/Hephaestus-Desktop/releases)
- Web service and platform overview: [Hephaestus](https://github.com/qiwentaidi/Hephaestus)
- Scanning nodes and command-line tools: [Hephaestus-Agent](https://github.com/qiwentaidi/Hephaestus-Agent)
- License registration: [Official website](http://47.97.59.120)

## Highlights

- **Local operation**: An embedded service and SQLite database support standalone use without a separate Web service or PostgreSQL deployment.
- **Combined scans**: Combine website, port, directory, subdomain, and JS/API scanning as needed, and review progress and results within a single task.
- **AI penetration testing conversations**: Use tools to investigate authorized targets and record findings, reproduction steps, and evidence for review.
- **Remote execution**: Connect to a shared PostgreSQL database and run scans on remote Agents, with centralized access to tasks and results.

## Main Features

| Module | Features |
| --- | --- |
| Attack Surface Assessment | Website fingerprinting, vulnerability scanning, port and service identification, weak password testing, directory, subdomain, and JS/API scanning |
| Task Management | Concurrency control, pause and resume, cancellation, history, scheduling, and parameter templates |
| AI Workbench | Projects, sessions, tool calls, image input, testing records, evidence review, and batch tasks |
| Assets and Vulnerabilities | Asset results, topology, maps, scan and AI findings, and manual remediation tracking |
| Report Management | Centralized scan reports, with individual and merged exports |
| Requests and PoCs | HTTP request editing and response inspection, plus Nuclei template search, editing, refinement, and debugging |
| Information Gathering | FOFA, Hunter, and Quake queries and aggregated searches, plus company information and related assets |
| Analysis and Credentials | Encoding and decoding, JWT, API documentation testing, text comparison, database connections, and key management |

For the full platform overview and Web deployment instructions, see the [Hephaestus repository](https://github.com/qiwentaidi/Hephaestus).

## Desktop Features

- **Local launcher**: Manage local tools and JDK configurations, launch tools, and open their folders or terminals.
- **Separate settings window**: Use the gear button at the top to open settings for scanning, AI, appearance, and language.
- **Mini-program decompilation**: Access mini-program decompilation from the desktop client.

## Quick Start

### 1. Download and Install

Download the installer for your operating system and CPU architecture from [Releases](https://github.com/qiwentaidi/Hephaestus-Desktop/releases), then install and launch the client.

The client starts its embedded service automatically. The default SQLite standalone mode requires no external database.

### 2. Activate Your License and Set Up Your Account

1. Register for a license key on the [official website](http://47.97.59.120) and follow the client instructions to activate online. For an isolated network, follow the page instructions to import an offline license.
2. After activation, a new instance prompts you to create an administrator account. If the instance has already been initialized, sign in.

### 3. Prepare Scanning Resources and AI Configuration

After signing in, configure the features you plan to use:

- **Scanning resources**: Open **System Settings → System Update** and use **Config Update** to download or update resources such as PoCs, directory wordlists, and weak password dictionaries.
- **Search engines**: Before using services such as FOFA, Hunter, or Quake, enter their keys under **System Settings → API Keys**.
- **AI Workbench**: Configure the provider, API URL, key, and model under **System Settings → AI Config**, then test the connection.
- **Local tools**: Open the launcher and configure tool paths and any JDKs you need.

Once the required configuration is ready, create a scan task or start an AI Workbench session with your authorized target and testing scope.

## Configuration and Data

In the paths below, `~` represents the current user's home directory.

| Item | Default or Description |
| --- | --- |
| Configuration file | `~/.config/hephaestus/config-desktop.yaml` |
| Local database | `~/.config/hephaestus/data/hephaestus.db` (SQLite) |
| Embedded service | `127.0.0.1:38456`; a temporary port is used if this port is occupied |
| Preferred service port | Set with `HEPHAESTUS_DESKTOP_BACKEND_PORT` |
| Configuration directory | Set with `HEPHAESTUS_CONFIG_DIR` |

The desktop client and Web service use separate configuration files but share the same default configuration directory. Set a different `HEPHAESTUS_CONFIG_DIR` for each to keep their configuration and local data separate.

To share platform data with the Web service or remote Agents, configure the desktop client to connect to the same PostgreSQL database. See the [Web deployment instructions](https://github.com/qiwentaidi/Hephaestus) for a connection example. Changing the database type does not migrate existing records automatically.

## Frequently Asked Questions

### Can the Desktop Client and Web Service Share Data?

Both can connect to the same PostgreSQL database to share platform records. They still use separate configuration files. Sharing a database does not automatically synchronize local tool paths or files in session working directories.

### What If Scanning Resources Are Unavailable or Search Engine Queries Fail?

Check that configuration resources have been downloaded under **System Settings → System Update** and that the relevant PoCs or dictionaries are available. Search engines also require valid API keys and sufficient query quota.

### What If the Embedded Service Port Is Occupied?

The client attempts to use a temporary port and continue startup. To specify a preferred port, set `HEPHAESTUS_DESKTOP_BACKEND_PORT` before launching the client.
