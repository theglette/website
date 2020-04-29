# Star Trek Timelines Data Core

As of May 2020, I'm preparing to archive the project (documentation, source code, data) in case someone wants to take over development in the future. The current situation (covid) doesn't afford me the time to continue working on it, and I'm also no longer having fun working on it alone.

## System overview

The assets (parsing, hosting) is set up on a separate machine to allow for more aggressive CDN / caching configuration, but the functionality could be combined with the main VM.

![assets VM](assets.svg "assets.datacore.app")

![main VM](main.svg "datacore.app")

### System requirements
A Linux VM with 2 CPUs and 4Gb of dedicated RAM should suffice for the current levels of traffic. Total space used (by assets, the static website, uploaded profiles and the DB) is under 2Gb (SSD preferred). Average traffic is 1200 unique users / day (13000 unique users / month) with 630Gb CDN cached bandwidth (+210Gb non-cached).

### Components

#### assets
This VM runs a cronjob every 10 minutes that scans, downloads and unpacks new assets (crew images) to the local file system. There's also an nginx HTTP server that publishes the assets.

- [ ] TODO upload source code

#### Image analysis
Written in dotnet core and using OpenCV and Tesseract OCR, this is the most taxing (CPU and RAM) component of the system, used by the bot for recognizing behold (and voyage setup) screenshots. Code is hosted [here](https://github.com/TemporalAgent7/datacore-bot).

#### site-server
Serves the dynamic aspects of datacore.app (profile uploads / views, fleet info, crew comments).

- [ ] TODO upload source code

#### discord bot
The Discord bot implementation (written in TypeScript with discord.js).

- [ ] TODO upload source code

#### DB
A simple DB (currently PostgreSQL but configurable) that links discord user ids with uploaded profiles (where associated) and includes the crew comments.

#### misc scripts
Scripts that take care of parsing the big / little book data, new items, ships and crew info and event details. These are currently manually executed by the maintainer 2-3 times a week and require regular maintenance to keep up with changes to the various upstream sources.

- [ ] TODO upload source code

# CONTRIBUTING

Contributions are always welcome, no matter how large or small. Before contributing, please read the [code of conduct](CODE_OF_CONDUCT.md).