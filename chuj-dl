#!/bin/bash
# chuj-dl — download music from chomikuj.pl
#
# Usage:
#   chuj-dl URL
#
# Example:
#   chuj-dl 'http://chomikuj.pl/J.D.a.d.1980/Music+Poland/Psychocukier/(2013)++Diamenty/07+-+Psychocukier+-+Czas,3468766147.mp3'

URL="$1"
TMP="$(mktemp /tmp/chujdl.XXXXXX)"

# Download the URL, get the metadata
echo -n "Downloading metadata... " >&2
wget "$URL" -O- -q > "$TMP"
echo "done" >&2

# Fetch real music URL and original filename
FILEURL="$(cat "$TMP" | grep data-fileid | cut -d\" -f14 | sed 's/&amp;/\&/g')"
FILENAME="$(cat "$TMP" | grep data-fileid | cut -d\" -f6 | sed 's/&amp;/\&/g')"

echo "$FILEURL"

# Remove a temporary file
rm -rf "$TMP"

# Echo a filename
echo "$FILENAME"

# Download the file
exec wget "$FILEURL" -O"$FILENAME"
