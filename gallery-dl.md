---
date: March 18, 2025
title: Gallery-dl manual page
---

# NAME

gallery-dl - bulk media downloader

# USAGE

gallery-dl \[*options*\] \[*url*\]

# DESCRIPTION

Gallery-dl is a useful and versatile bulk media downloader written in python.
At the time of writing (March 18 2025) 284 sites are supported. Images are supported
by default but HLS/DASH videos will require either yt-dlp or youtube-dl.

Authored by plshelpidkwhatimdoing

## GENERAL OPTIONS

To specify a filename format "-f / \--filename". Using twitter as an example, the default filename format is "{tweet_id}_{num}.{extension}".

To add the authors name (the @ one, not display name) to that, use this (quotes included):

`gallery-dl -f "{user[name]}_{tweet_id}_{num}.{extension}" <url>`

- Note: keywords must have brackets around them or they will be interpreted as literal, not variables.

- Setting invalid keywords will result in it being replaced with "None".

To set the destination for downloads, use the "-d / \--destination" switch.

`gallery-dl -d . <url>`

Note that that this switch will still create a subfolder for its respective site. 

For example downloading from twitter and using "-d ." will put the downloads in "current directory/twitter/{persons username}"

If you want to avoid that, use "-D / \--directory" instead.

Using `gallery-dl -D .` will place the downloaded media in the current directory.

To load external extractors from PATH, use "-X / \--extractors"

`gallery-dl -X <extractor> <url>`

The extractor to use for a certain site can also be specified in the command line. This is useful if gallery-dl doesn't autodetect the extractor as being used for a site.

- The "generic" extractor is always a good idea to try if a site is not supported by gallery-dl.

`gallery-dl generic:<url>`

The default user agent for gallery-dl is for windows firefox. To change that, set it in the config file or via command.

- Note: some sites require a custom user agent to use properly.

- Also, setting the value to "browser" will attempt to use your default browser user agent.

`gallery-dl --user-agent <whatever you want here> <url>`

If encountering problems with downloading, clearing the cache may help. To do so, run:

`gallery-dl --clear-cache <module>`

Example of clearing the cache for twitter would be:

`gallery-dl --clear-cache twitter`

Put "ALL" for the module to clear everything. (or just delete the "cache.sqlite3" file)

## UPDATE OPTIONS

Use "*-U / \--update*" to check if there is a newer version and update if there is

Use "*\--update-to*" to switch to a different release channel (options are "stable" or "dev") or upgrade/downgrade to a different version

`gallery-dl --update-to <channel[tag]>`

To check if a new version is out, use "*\--update-check*"

## INPUT OPTIONS

URLs can also be read from a text file with "*-i / \--input-file*"

To have urls be commented out after downloading, "*-I / \--input-file-comment*" can be used instead.

To delete the urls, use "*-x / \--input-file-delete*". Failed urls will not be commented or deleted.

`gallery-dl -i list1.txt -i optionallist.txt`

Gallery-dl can also be directed to an online text file such as one on pastebin for example.

`gallery-dl r:<url to text file>`

Use "\--no-input" if you don't want to be prompted for passwords or tokens.

## OUTPUT OPTIONS

Use "*-q / \--quiet*" to activate quiet mode (print nothing).

Use "*-w / \--warning*" to only print errors and warnings.

Use "*-v / \--verbose*" to print debug information.

To print the url of an something without downloading it, use "*-g / \--get-urls*". To have intermediary urls resolved, use "*-G / \--resolve-urls*"

To print the json information, use "*-j / \--dump-json*". To have intermediary urls resolved, use "*-J / \--resolve-json*"

Use "*-s / \--simulate*" to simulate a download, but not download anything (useful to check things like if you did name format correctly)

Use "-E / \--extractor-info" to print information about an extractor. Things like subcategory and default filename format are printed.

`gallery-dl -E <url>`

To list usable keywords, use "*-K / \--list-keywords*". 
This will print keywords to use in the config files and/or switches such as "-f"

`gallery-dl -K <url>`

Use "*-e / \--error-file*" to write error urls to a text file.

`gallery-dl -e errors.txt <url>`

To print additional information, use "*-N / \--print*". To write it to a file, use "*\--print-to-file*".

`gallery-dl -N <event>:<format> <url>`

`gallery-dl --print-to-file <event>:<format> <file> <url>`

Example command `gallery-dl -N prepare:{user[date]} -D . <url>` will have give this output:

```
2024-10-02 15:47:43
./1861876894297117004_1.jpg
```

To list available modules, use "*\--list-modules*".

To list available extractors, use "*\--list-extractors*"

`gallery-dl --list-extractors <specify module or leave blank for all>`

To write to a log file, use "*\--write-log*"

`gallery-dl --write-log log.txt <url>`

Use "*\--write-unsupported*" to write urls that emitted by extractors but can't be handled.

`gallery-dl --write-unsupported log.txt <url>`

Use "*\--write-pages*" to write downloaded pages to a text file in the current directory. (Like a more advanced version of -j).

Use "*\--print-traffic*" to view information about the connection.

Use "*\--no-colors*" to disable color output.

## NETWORKING OPTIONS

To set the amount of retries to do, use "*-R / \--retries*", "-1" for infinite retries, default is 4.

`gallery-dl -R 6 <url>`

To tell gallery-dl how long to wait before timing out, use "*\--http-timeout*". Default is 30 seconds

`gallery-dl --http-timeout 60`

To use a proxy, use "*\--proxy*"

`gallery-dl --proxy <proxyinfo> <url>`

To bind to a client side ip address, use "*\--source-address*"

`gallery-dl --source-address <ip> <url>`

Use "*-4 / \--force-ipv4*" to allow ipv4 connections only

Use "*-6 / \--force-ipv6*" to allow ipv6 connections only

If https certificate checking is creating problems, use "*\--no-check-certificate*" to disable it

## DOWNLOADER OPTIONS

To throttle gallery-dl's bandwidth usage, use "*-r / \--limit-rate*". Values such as "250k" or "2M" are accepted.

`gallery-dl -r 5M <url>`

Set the size of in-memory data chunks with "*\--chunk-size*". Default "32k"

`gallery-dl --chunk-size 64k`

To wait a certain amount of time before each download, use "*\--sleep*". This is not limited to just one number and can include decimals and ranges.

`gallery-dl --sleep 1.5-6 <url>`

That command waits anywhere from 1.5 to 6 seconds before each download. Useful if encountering rate limit errors.

To wait a certain amount of time in between http requests, use "*\--sleep-request*" (same style usage as \--sleep)

To have the extractor wait a certain amount of time before extracting information from the given urls, use "*\--sleep-extractor*" (same style usage as \--sleep)

If you don't want to use .part files while downloading, specify "*\--no-part*"

To overwrite existing files instead of skipping, use "*\--no-skip*"

If you don't want file modification times to be set as they appear in the http header, use "*\--no-mtime*"

If you don't want to download anything, use "*\--no-download*"

## CONFIGURATION OPTIONS

By default, gallery-dl uses json style config files.

json does not support comments, but you can add them to your config file by using an unused variable such as "#" and it will be silently ignored, multiple can be used with no errors.

To specify an additional option, use "*-o / \--option*". Anything that can be used in "-o" can be added to the config file.

`gallery-dl -o "ratelimit=abort" <url>`

That command would stop the downloading upon being ratelimited by the site you're downloading from

To specify an additional config file, use "*-c / \--config*"

`gallery-dl -c /path/to/file <url>`

Gallery-dl is capable reading yaml config files, use "*\--config-yaml*" to specify a yaml file. (Requires PyYAML)

`gallery-dl --config-yaml /path/to/file <url>`

Gallery-dl is also capable of reading toml files, use "*\--config-toml*" to specify a toml file. (Requires toml)

`gallery-dl --config-toml /path/to/file <url>`

To create a config file, use "\--config-create"

To make sure the config files work, use "*\--config-status*"

To open config file in default editor, use "*\--config-open*"

To have the config files ignored, use "*\--config-ignore*"

Gallery-dl looks for config files in the following locations

Windows:
```
%APPDATA%\gallery-dl\config.json
%USERPROFILE%\gallery-dl\config.json
%USERPROFILE%\gallery-dl.conf
```
MacOS/Linux:
```
/etc/gallery-dl.conf
${XDG_CONFIG_HOME}/gallery-dl/config.json
${HOME}/.config/gallery-dl/config.json
${HOME}/.gallery-dl.conf
```
Extensions are included, so a "gallery-dl.json" in "/etc/" will not be recognized.

## AUTHENTICATION OPTIONS

Use "*-u / \--username*" to provide the username to login with (or set it in the config file)

Use "*-p / \--password*" to provide the password to login with

Netrc authentication data can also be used by adding "\--netrc"

Username and password can also be set by using `*-o "username=<username>" -o "password=<password>"*` if you want to do that for whatever reason.

## COOKIE OPTIONS

Getting a cookies.txt file can be done with browser extensions.

To use a cookies.txt file, use "*-C / \--cookies*"

`gallery-dl -C cookies.txt <url>`

To export gallery-dl's cookies to a file, use "*\--cookies-export*"

`gallery-dl --cookies-export cookies.txt`

To use cookies from a browser, use "*\--cookies-from-browser*"

`gallery-dl --cookies-from-browser firefox`

## SELECTION OPTIONS

Use "*-A / \--abort*" to stop the current extractor after a certain number of skipped downloads.

`gallery-dl -A 6 <url>`

Use "*-T / \--terminate*" to stop the current and parent extractor after a certain number of failed downloads.

`gallery-dl -T 6 <url>`

Self explanitory, use "*\--filesize-min*" to skip any files smaller then specified size. Values such as "250k" or "2M" are accepted.

`gallery-dl --filesize-min 250k <url>`

Also self explanitory, use "*\--filesize-max*" to skip any files large then specified size. Values such as "250k" or "2M" are accepted.

`gallery-dl --filesize-max 1G <url>`

To record all downloaded/skipped files in an archive, use "*\--download-archive*". This will download files in an archive and skip existing ones.

`gallery-dl --download-archive <file>`

To specify a range to start at, stop at, to through, use "*\--range*".

- Note: gallery-dl starts counting at 1, not 0. (Ex: 1, 2 ... Not 0, 1, 2 ...)

Using "\--range" to start at 50: (when starting, 50- and 50: will work the same)

`gallery-dl --range 50- <url>`

Using "\--range" to stop at 50 (or "-50" with quotes)

`gallery-dl --range :50 <url>`

Using "\--range" to download 6 - 50: (6-50 is also acceptable)

`gallery-dl --range 6:50 <url>`

The option "*\--chapter-range*" is similar but applies to manga chapters instead of individual posts. It has the same use style as "\--range" so examples will not be written.

To use python expressions and/or keywords from "-K", use "\--filter". This command will skip all images wider then 1200px:

`gallery-dl --filter "width <= 1200" <url>`

The option "*\--chapter-filter*" only applies to manga chapters. This command will only download chapters in english:

`gallery-dl --chapter-filter "lang == 'en'" <url>`

## POSTPROCESSING OPTIONS

To activate a certain postprocessor, use "*-P / \--postprocessor*"

`gallery-dl -P <processor> <url>`

To skip all postprocessors, use "*\--no-postprocessors*"

To run additional postprocessor options, use "*-O / \--postprocessor-option*". Like "-o" anything used in this can be added to the config file.

`gallery-dl -O "mode=tags" <url>`

To write metadata about each image, use "*\--write-metadata*"

To write metadata about the entire gallery to an "info.json" use, "*\--write-info-json*".

- Please note: there is only one info.json, this is for the entire gallery, not each image.

To write image tags to a text file, use "*\--write-tags*"

Use "*\--zip*" to store downloaded files in a zip file. Compression options are "store", "zip", "bzip2", "lzma", default is "store". Compression with brotli (.br) and/or zstandard (.zst) is also possible.

Use "*\--cbz*" to store downloaded files in a cbz file. Compression options are same as zip.

Use "*\--mtime*" to set the modification time to a keyword, usually something like "date". Use "-K" for available options.

To rename already downloaded files from a pattern to what is currently in the config, use "*\--rename*".

For example if you update the twitter filename config to include the posters username (like the earlier example), you would use it like this:

`gallery-dl --rename {tweet_id}_{num}.{extension} <url>`

To rename already downloaded files from what is currently in the config to a different pattern, use "*\--rename-to*".

For example if you have the twitter default filename of just the id and number, and you wanted to add the username to downloaded files, you would run this:

`gallery-dl --rename-to {user[name]}_{tweet_id}_{num}.{extension} <url>`

To convert pixiv ugoira's, use "*\--ugoira*" the options are "webm", "mp4", "gif", "vp8", "vp9", "vp9-lossless", "copy", "zip". (requires ffmpeg)

`gallery-dl --ugoira <format> <url>`

Use "*\--exec*" to run a command after each downloaded file. Supported replacement fields are {} or {_path}, {_directory}, {_filename}.

`gallery-dl --exec "convert {} {}.png && rm {}" <url>`

Use "*\--exec-after*" to run a command after all the files finished downloading. Same replacement fields as "\--exec"

`gallery-dl --exec-after "mogrify -format jpg *.png" <url>`
