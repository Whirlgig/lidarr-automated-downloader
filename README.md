
# lidarr-automated-downloader (LAD)
## Requirements
Linux Packages: <br/>
* jq
* find
* ffmpeg
* beets
* flac
* mp3val
* curl<br/>

Baseline OS used for testing is Ubuntu 18.04, so use equivalent package versions

## Setup
1. Edit "config" with a text editor that can write in Unix line endings... see: [Configuration](https://github.com/RandomNinjaAtk/lidarr-automated-downloader#configuration)

## Eecution
Execute script via CLI with the following command: `bash lidarr-automated-downloader.bash`

## Files
* lidarr-automated-downloader.bash
  * script to execute
* config
  * File contains all configuration settings, see: [Configuration](https://github.com/RandomNinjaAtk/lidarr-automated-downloader#configuration)
* notfound.log
  * Log file containing list of albums that could not be found using normal or fuzzy matching, automatically cleared every Saturday via cron
* musicbrainzerror.log
  * Log file containing list of artists without links, open log for more details
* download.log
  * Log file containing list of albums that were downloaded, automatically cleared every Saturday via cron

## Configuration

Modify the "config" file to set your configuration settings using a text editor that can write in Unix line endings...

| Setting | Function |
| --- | --- |
| `downloaddir` |  Deezloader download directory location |
| `LidarrImportLocation` | Temporary location that completed downloads are moved to before lidarr attempts to match and import |
| `PathToDLClient` | Path to DL client directory (d-fi) |
| `BeetConfig` | Location of beets configuration file |
| `BeetLibrary` | Location of beets library file, this file is self-cleaned after every download |
| `LidarrUrl` | Set domain or IP to your Lidarr instance including port. If using reverse proxy, do not use a trailing slash. Ensure you specify http/s. |
| `LidarrApiKey` | Lidarr API key |
| `ARLToken` | User token for dl client, for instructions on obtaining key: https://notabug.org/RemixDevs/DeezloaderRemix/wiki/Login+via+userToken#how-do-i-get-my-usertoken |
| `concurrency` | Number of concurrent tracks to download via the client. Increasing can speed things up but is more resource intensive, lower is safer... |
| `VerifyTrackCount` | true = enabled :: This will verify album track count vs dl track count, if tracks are found missing, it will skip import... |
| `amount` | Maximum: 1000000000 :: Number of missing/cutoff albums to look for... |
| `quality` | SET TO: FLAC or MP3 or OPUS or AAC or FDK-AAC or ALAC |
| `ConversionBitrate` | FLAC -> OPUS/AAC/FDK-AAC will be converted using this bitrate |
| `ReplaygainTagging` | TRUE = ENABLED :: adds replaygain tags for compatible players (FLAC ONLY) |
| `FolderPermissions` | Based on chmod linux permissions |
| `FilePermissions` | Based on chmod linux permissions |
| `DownLoadArtistArtwork` | true = enabled :: Uses Lidarr Artist artwork first with a fallback using LAD as the source |
| `TagWithBeets` | true = enabled :: enable beet tagging to improve matching accuracy, requires beets installation and beets file path configuration |
| `RequireBeetsMatch` | true = enabled :: skips importing files that could not be matched using beets |
| `RequireQuality` | true = enabled :: skips importing files that do not match quality settings |

# Lidarr Configuration Recommendations

## Media Management Settings:
* Disable Track Naming
  * Disabling track renaming enables synced lyrics that are imported as extras to be utilized by media players that support using them

#### Track Naming:

* Artist Folder: `{Artist Name}{ (Artist Disambiguation)}`
* Album Folder: `{Artist Name}{ - ALBUM TYPE}{ - Release Year} - {Album Title}{ ( Album Disambiguation)}`

#### Importing:
* Enable Import Extra Files
  * `lrc,jpg,png`

#### File Management
* Change File Date: Album Release Date
 
#### Permissions
* Enable Set Permissions


# Official Docker: [lidarr-lad](https://github.com/Whirlgig/docker-lidarr-lad)
* Pre-configured, no setup required, includes Lidarr

