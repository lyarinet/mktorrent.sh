<h3 align="center">
<img src="https://cdn.rawgit.com/odb/official-bash-logo/master/assets/Logos/Identity/PNG/BASH_logo-transparent-bg-color.png">
</h3>

```sh
#!/bin/bash
# Name of script .. : mktorrent.sh
# Date  ........... : 3-27-2017
# Author  ......... : Asif Agaria | https://ready2fun.com
# Description  .... : Folder/File to .torrent + size automated parts
# Software   ...... : mktorrent
# Execution  ...... : "sh mktorrent.sh directory/or/File.mp4"

folder="$1"
output="$folder.torrent"
fsize="$(du -sm $1 | awk '{print $1}')"
announce="https://tracker.com/announce" # Edit this

## Calculate folder/file size
if [ "$fsize" -le 100 ];
  then psize="19";
elif [ "$fsize" -le 700 ];
  then psize="20";
elif [ "$fsize" -le 2000 ];
  then psize="21";
elif [ "$fsize" -le 5000 ];
  then psize="22";
elif [ "$fsize" -le 10000 ];
  then psize="23";
elif [ "$fsize" -le 30000 ];
  then psize="24";
elif [ "$fsize" -le 60000 ];
  then psize="25";
elif [ "$fsize" -le 100000 ];
  then psize="26";

else echo "Please split your files and create a torrent for each part separately" && exit 1;
fi

## Create .torrent
mktorrent -v -p -l "$psize" -a "$announce" -o "$output" "$folder"

```
