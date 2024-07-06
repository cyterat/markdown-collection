<span style="color:#333333; font-size:18px; font-weight:bold"> Compiled by <a href=https://github.com/cyterat style="color:#00b2b7;">cyterat</a></span>

# **Linux Commands for Data Manipilation** (unsorted)

## curl
* **Basic file download**
	```
	curl "https://...filename.csv"
	```
* **Download file, unzip it, import into sqlite, and write 'sqlite' query for the dataset**: 
	```
	curl -s https://www.some-website.com/additional/interesting-file.zip | gunzip | sqlite3 -csv ':memory:' '.import /dev/stdin stdin' "select Name from stdin order by USD asc limit 1;"
	```

* **Download file, unzip it, import into sqlite, and use some python 'pandas' on the dataset**:
	```
	curl -s https://www.some-website.com/additional/interesting-file.zip | gunzip | python3 -c 'import sys, pandas as pd pd.read_csv(sys.stdin).melt("Name").to_csv(sys.stdout, index=False)'
	```

* **Download file, unzip it, import into sqlite, use some python 'pandas' on the dataset, and upload it to a cloud csv storage**:
	```
	curl -s https://www.some-website.com/additional/interesting-file.zip | gunzip | python3 -c 'import sys, pandas as pd pd.read_csv(sys.stdin).iloc[:,:-1].melt("Name").to_csv(sys.stdout,index=False)' | curl -n --upload-file - 'https://csvbase.com/myname/secret-dump?public=yes'
	```

***

## wget
* **Basic file download**:
	```
	wget "https://...filename.csv"
	```

* **Download 'large json file' into directory using some custom headers**:
	```
	wget --secure-protocol=TLSv1_2 -c --retry-connrefused --waitretry=1 --read-timeout=20 --timeout=15 -t 0 --continue -O "myfolder/desired-filename.json" "https://...filename.json"
	```

***

## more
* **To view the contents of a file page by page, you can use the more command:** 
	```
	more largefile.txt
	```

***

## less
* **Similar to more, but allows backward navigation:** 
	```
	less largefile.txt
	```

***

## head
* **This command displays the first 100 lines of a file:** 
	```
	head -n 100 largefile.txt
	```

***

## tail 
* **This command displays the last 100 lines of a file:** 
	```
	tail  -n 100 largefile.txt
	```

***

## split 
* **This command can be used to split a large file into smaller files (e.g. into max 100mb each):** 
	```
	split -b 100M largefile.txt
	```

***

## cat 
* **This command concatenates and displays the content of files:** 
	```
	cat file.txt
	```

***

## tac 
* **This command displays the content of files in reverse:** 
	```
	tac file.txt
	```

***

## nl 
* **This command adds line numbers to the content of files:** 
	```
	nl file.txt
	```

***

## od 
* **This command dumps the content of files in octal and other formats:** 
	```
	od -c file.txt
	```

***

## base64 
* **This command encodes or decodes file in base64 format:** 
	```
	base64 file.txt
	```

***

## zcat 
* **This command displays the content of gzipped files:** 
	```
	zcat file.txt.gz
	```

***

## zless 
* **This command allows you to view gzipped files in a pager with backward navigation:** 
	```
	zless file.txt.gz
	```

***

## zmore 
* **This command allows you to view gzipped files in a pager:** 
	```
	zmore file.txt.gz
	```

***

## zgrep 
* **This command allows you to search inside gzipped files:** 
	```
	zgrep "search term" file.txt.gz
	```

***

## zdiff 
* **This command allows you to compare gzipped files:** 
	```
	zdiff file1.txt.gz file2.txt.gz
	```

***

## znew 
* **This command allows you to recompress .Z files to .gz files:** 
	```
	znew file.txt.Z
	```

***

## file 
* **This command allows you to determine the type of a file:** 
	```
	file file.txt
	```

* **This command allows you to determine the encoding of a file:** 
	```
	file -i file.txt
	```

***

## stat 
* **This command allows you to display file or file system status:** 
	```
	stat file.txt
	```

***

## touch 
* **This command allows you to change file timestamps:** 
	```
	touch file.txt
	```

***

## cp 
* **This command allows you to copy files and directories:** 
	```
	cp source.txt destination.txt
	```

***

## mv 
* **This command allows you to move or rename files:** 
	```
	mv oldname.txt newname.txt
	```

***

## rm 
* **This command allows you to remove files or directories:** 
	```
	rm file.txt
	```

***

## ln 
* **This command allows you to make links between files:** 
	```
	ln -s file.txt link.txt
	```

***

## find 
* **This command allows you to search for files in a directory hierarchy:** 
	```
	find . -name "*.txt"
	```

***

## locate 
* **This command allows you to find files by name:** 
	```
	locate file.txt
	```

***

## grep 
* **This command allows you to print lines matching a pattern:** 
	```
	grep "search term" file.txt
	```

***

## egrep 
* **This command allows you to print lines matching a pattern (extended regexp):** 
	```
	egrep "search term" file.txt
	```

***

## fgrep 
* **This command allows you to print lines matching a pattern (fixed strings):** 
	```
	fgrep "search term" file.txt
	```

***

## diff 
* **This command allows you to compare files line by line:** 
	```
	diff file1.txt file2.txt
	```

***

## comm 
* **This command allows you to compare two sorted files line by line:** 
	```
	comm file1.txt file2.txt
	```

***

## wc 
* **This command allows you to print newline, word, and byte counts for each file:** 
	```
	wc file.txt
	```

***

## cut 
* **This command allows you to remove sections from each line of files:** 
	```
	cut -d' ' -f1 file.txt
	```

***

## paste 
* **This command allows you to merge lines of files:** 
	```
	paste file1.txt file2.txt
	```

***

## join 
* **This command allows you to join lines of two files on a common field:** 
	```
	join -1 1 -2 1 file1.txt file2.txt
	```

***

## sort 
* **This command allows you to sort lines in text files:** 
	```
	sort file.txt
	```

***

## iconv 
* **This command allows you to list all known coded character sets:** 
	```
	iconv -l
	```

* **This command allows you to convert an 'input.file' using a selected encoding and save it as 'output.file':** 
	```
	iconv -f ISO-8859-1 -t UTF-8//TRANSLIT input.file -o out.file
	```

***

## zip
* __Unzip zip archive__
	```
	unzip filename.zip
	```

* __List contents of a zipped archive__
	```
	unzip -l filename.zip
	```

* __Unzip multiple zip archives__
	```
	unzip "*.zip"
	```

* __Unzip zip archive with password__
	```
	unzip -P PaSSwOrd filename.zip
	```

* __Unzip zip archive excluding some files__
	```
	unzip filename.zip -x file1 file2 file3
	```

* __Unzip zip archive excluding a git directory with all its contents__
	```
	unzip filename.zip -x "*.git/*"
	```

* __Unzip rar archive__
	```
	unrar e -p filename.rar
	```

* __Unzip tzr.gz archive__
	```
	tar zxvf filename.tar.gz
	```

***

## ls
* __List all files in a parent directory__
	```
	ls ..
	```

* __List all files in a user's home directory__
	```
	ls ~
	```

* __List only directories__
	```
	ls -d */
	```

* __List files with subdirectories__
	```
	ls *
	```

* __List files recursively (all files with their directories and subdirectories)__
	```
	ls -R Downloads
	```

* __List files in long format with readable file sizes__
	```
	ls -lh Downloads
	```

* __List files including hidden files (i.e. those starting with dot)__
	```
	ls -a Downloads
	```

* __List files and sort by time modified (newest to oldest)__
	```
	ls -t
	```

* __List files and sort by time modified (oldest to newest)__
	```
	ls -tr
	```

* __List files and sort by size (biggest to smallest)__
	```
	ls -S
	```

* __List files and sort by size (smallest to biggest)__
	```
	ls -Sr
	```

***

## > and >>

* __Write (overwrite) command output to a file__
	```
	date > log.txt
	```

* __Write (append) command output to a file__
	```
	date >> log.txt
	```

***

## tee

* __Display and write (overwrite) command output to a new file__
	```
	date | tee log.txt
	```

* __Display and write (append) command output to a new file__
	```
	date | tee -a log.txt
	```

***

## printf
* __Save a list of all files in directory to a text file__
	```
	printf '%s\n' * > output.txt
	```

***
***