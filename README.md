#!/bin/bash
# Name of script .. : mktorrent.sh
# Date  ........... : 3-27-2017
# Author  ......... : Asif Agaria | https://ready2fun.com
# Description  .... : Folder/File to .torrent + size automated parts
# Software   ...... : mktorrent
# Execution  ...... : "sh mktorrent.sh directory/or/File.mp4"


# Variables ...... : To define here and not to modify the continuation of the script
# TRACKER ........ : Tracker announce URL


TRACKER="http://tracker.bittorrent.com:6969/announce"

TORRENTFILE=$(basename "$TORRENT")
TAILLE=$(du -s "$TORRENT" | awk '{ print $TORRENT }')
    if [ $TAILLE -lt 524288 ]; then
        PIECE=18
    elif [ $TAILLE -lt 1048576 ]; then
        PIECE=19
    elif [ $TAILLE -lt 2097152 ]; then
        PIECE=20
    elif [ $TAILLE -lt 4194304 ]; then
        PIECE=21
    elif [ $TAILLE -lt 8388608 ]; then
        PIECE=22
    elif [ $TAILLE -lt 16777216 ]; then
        PIECE=23
    elif [ $TAILLE -lt 33554432 ]; then
        PIECE=24
    else
        PIECE=25
    fi

# Script ......... : NOT MODIFIED
# -p . ........... : private (no DHT)
# -l . ........... : length (size pieces)
# -a . ........... : announce (URL tracker)
# -o . ........... : output (Name of .torrent)
# $1 . ........... : Folder/Target file

mktorrent -p -l "$PIECE" -a "$TRACKER" -o "$TORRENTFILE".torrent "$TORRENT"

# Variables     ...... : Not to be modified
# TORRENTFILE ........ : Name of the .torrent, from the folder / target file
# TAILLE     ......... : Size of rooms defined according to File/File (cf https://wiki.vuze.com/w/Torrent_Piece_Size)
