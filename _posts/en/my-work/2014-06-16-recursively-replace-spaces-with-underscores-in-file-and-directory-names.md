---
id: 418
lang: en
ref: recursively-replace-spaces-with-underscores-in-file-and-directory-names
title: Recursively replace spaces with underscores in file and directory names
date: 2014-06-16T05:22:13+00:00
author: Arthur Gareginyan
layout: post
guid: http://mycyberuniverse.com/?p=418
permalink: /linux/recursively-replace-spaces-with-underscores-in-file-and-directory-names.html
categories:
  - Debian/Ubuntu
  - Linux
  - Raspberry Pi
  - Мои программы
  - my-work
tags:
  - rename
  - replace
  - space
  - underscore

---

![thumb]()
A safe solution to recursively replace spaces with underscores in file and directory names starting from the current directory.


### Example.

<pre>
tree
.
|-- a dir
|        `-- file with spaces.txt
`-- b dir
         |-- another file with spaces.txt
         `-- yet another file with spaces.pdf
</pre>

becomes:

<pre>
tree
.
|-- a_dir
|        `-- file_with_spaces.txt
`-- b_dir
         |-- another_file_with_spaces.txt
         `-- yet_another_file_with_spaces.pdf
</pre>


### Code.

* **Name:** space_to_underscore.sh
* **Description:** Recursively replace spaces with underscores in file and directory names.
* **Language:** BASH</strong>

```
#!/bin/bash
#=============================================================#
# Name:         Space to Underscore	                      #
# Description:  Recursively replace spaces with underscores   #
#               in file and directory names.                  #
# Version:      ver 1.2                                       #
# Data:         16.6.2014                                     #
# Author:       Arthur (Berserkr) Gareginyan                  #
# Author URI:   http://mycyberuniverse.com/author.html        #
# Email:        arthurgareginyan@gmail.com                    #
# License:      GNU General Public License, version 3 (GPLv3) #
# License URI:  http://www.gnu.org/licenses/gpl-3.0.html      #
#=============================================================#

#               	USAGE:
#		chmod +x space_to_underscore.sh
#		cd /home/user/example
#		~/space_to_underscore.sh

# Check for proper priveliges
[ "`whoami`" = root ] || exec sudo "$0" "$@"


####################### DIALOG ############################
echo -en "\n BEWARE! Starting from current directory (`pwd`),"
echo -en " files and directories with spaces in name  will be renamed automatically.\n"
echo -en "\n Press \"ENTER\" to continue or \"N\" to exit:"
read ops
case "$ops" in
        n|N)
            echo -en "\n Canceled by User. Exiting...\n"
            exit 1 ;;
        *)
            echo -en "\n Begining...\n" ;;
esac


################### SETUP VARIABLES #######################
number=0                    # Number of renamed.
number_not=0		    # Number of not renamed.
IFS=$'\n'
array=( `find ./ -type d` ) # Find catalogs recursively.


######################## GO ###############################
# Reverse cycle.
for (( i = ${#array[@]}; i; )); do
     # Go in to catalog.
     pushd "${array[--i]}" >/dev/null 2>&1
     # Search of all files in the current directory.
     for name in *
     do
     	     # Check for spaces in names of files and directories.
	     echo "$name" | grep -q " "
	     if [ $? -eq 0 ]
	     then
	     	# Replacing spaces with underscores.
	        newname=`echo $name | sed -e "s/ /_/g"`
		if [ -e $newname ]
        	then
			let "number_not +=1"
                	echo " Not renaming: $name"
        	else
        		# Plus one to number.
                	let "number += 1"
                    	# Message about rename.
                	echo "$number Renaming: $name"
                	# Rename.
		        mv "$name" "$newname"
		fi
	     fi
     done
     # Go back.
     popd >/dev/null 2>&1
done

echo -en "\n All operations is complited."

if [ "$number_not" -ne "0" ]
  then echo -en "\n $number_not not renamed."
fi

if [ "$number" -eq "0" ]
  then echo -en "\n Nothing been renamed.\n"
elif [ "$number" -eq "1" ]
   then echo -en "\n $number renamed.\n"
   else echo -en "\n Renamed files and catalogs: $number\n"
fi

exit 0
```


### Usage

Give execute permissions:

```
chmod +x space_to_underscore.sh
```

Go to needed directory:

```
cd /home/user/example
```

Run the `space_to_underscore.sh` which placed in user home directory: 

```
~/space_to_underscore.sh
```

[github_btn url="https://github.com/ArthurGareginyan/space_to_underscore/"]
