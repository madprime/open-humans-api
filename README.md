# open-humans-api

This is work in progress.

## Command line tools

### ohpub-download

```
Usage: ohpub-download [OPTIONS]

  Download public data from Open Humans.

Options:
  -s, --source TEXT     the source to download files from
  -u, --username TEXT   the user to download files from
  -d, --directory TEXT  the directory for downloaded files
  -m, --max-size TEXT   the maximum file size to download
  --help                Show this message and exit.
```

#### Examples

```
# download all 23andMe files to 23andme/
$ mkdir 23andme
$ oh-download --source twenty_three_and_me --directory 23andme
# download all of beau's files to the current directory
$ oh-download --username beau
```

### ohproj-download

```
Usage: ohproj-download [OPTIONS]

  Download data from project members to the target directory.

  Unless this is a member-specific download, directories will be created for
  each project member ID. Also, unless a source is specified, all shared
  sources are downloaded and data is sorted into subdirectories according to
  source.

  Projects can optionally return data to Open Humans member accounts. If
  project_data is True (or the "--project-data" flag is used), this data
  (the project's own data files, instead of data from other sources) will be
  downloaded for each member.

Options:
  -d, --directory TEXT     Target directory for downloaded files.  [required]
  -T, --master-token TEXT  Project master access token.
  -m, --member TEXT        Project member ID.
  -t, --access-token TEXT  OAuth2 user access token.
  -s, --source TEXT        Only download files from this source.
  --project-data TEXT      Download this project's own data.
  --max-size TEXT          Maximum file size to download.  [default: 128m]
  -v, --verbose            Report INFO level logging to stdout
  --debug                  Report DEBUG level logging to stdout.
  --help                   Show this message and exit.
```

## ohproj-metadata

```
Usage: ohproj-metadata [OPTIONS]

  Draft or review metadata files for uploading files to Open Humans.

  The target directory should either represent files for a single member (no
  subdirectories), or contain a subdirectory for each project member ID.

Options:
  -d, --directory TEXT  Target directory  [required]
  --create-csv TEXT     Create draft CSV metadata  [required]
  --max-size TEXT       Maximum file size to consider.  [default: 128m]
  -v, --verbose         Show INFO level logging
  --debug               Show DEBUG level logging.
  --help                Show this message and exit.
```

### ohproj-upload
```
Usage: ohproj-upload [OPTIONS]

  Upload files for the project to Open Humans member accounts.

  If using a master access token and not specifying member ID:

  (1) Files should be organized in subdirectories according to project
  member ID, e.g.:
    main_directory/01234567/data.json
    main_directory/12345678/data.json
    main_directory/23456789/data.json
  (2) The metadata CSV should have the following format:
    1st column: Project member ID
    2nd column: filenames
    3rd & additional columns: Metadata fields (see below)

  If uploading for a specific member:
   (1) The local directory should not contain subdirectories.
   (2) The metadata CSV should have the following format:
     1st column: filenames
     2nd & additional columns: Metadata fields (see below)

  The default behavior is to overwrite files with matching filenames on Open
  Humans, but not otherwise delete files. (Use --safe or --sync to change
  this behavior.)

  If included, the following metadata columns should be correctly formatted:
    'tags': should be comma-separated strings
    'md5': should match the file's md5 hexdigest
    'creation_date', 'start_date', 'end_date': ISO 8601 dates or datetimes

  Other metedata fields (e.g. 'description') can be arbitrary strings.

Options:
  -d, --directory TEXT     Target directory for downloaded files.  [required]
  --metadata-csv TEXT      CSV file containing file metadata.  [required]
  -T, --master-token TEXT  Project master access token.
  -m, --member TEXT        Project member ID.
  -t, --access-token TEXT  OAuth2 user access token.
  --safe                   Do not overwrite files in Open Humans.
  --sync                   Delete files not present in local directories.
  --max-size TEXT          Maximum file size to download.  [default: 128m]
  -v, --verbose            Report INFO level logging to stdout
  --debug                  Report DEBUG level logging to stdout.
  --help                   Show this message and exit.
```
