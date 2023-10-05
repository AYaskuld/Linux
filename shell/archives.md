## Working with Archives
### zip/unzip

zip - package and compress (archive) files

unzip - list, test and extract compressed files in a ZIP archive

$ zip -rp <file>.zip /path/to/
```# compress folder into .zip```

$ unzip <file>.zip
```# extract files in current location from .zip````

Note: zip and unzip commands have a lot of useful options. Please use man zip or man unzip to get acquainted with all of them 

### TAR

tar - saves many files together into a single tape or disk archive, and can restore individual files from the archive.

$ tar -cvf <file>.tar path/to/  
$ tar -xvf <file>.tar  
$ tar -tf <file>.tar  
$ tar -cvzf <file>.tar.gz path/to/  

$ tar cf - dir1 | (cd dir2 && tar xf -)  
      # move an entire directory structure with tar  

$ ssh root@host1 "cd /somedir/tocopy/ && tar -cf - ." | ssh root@host2 "cd /samedir/tocopyto/ && tar -xf -"   
     # copy from host1 to host2, through your host

Note: tar command has a lot of useful options. Please use man tar to get acquainted with all of them

### GZIP

gzip, gunzip, zcat - compress or expand files

zgrep - search in gzip arhives

gzip -c file1 > foo.gz 
                    # compresses file1 into foo.gz.

gzip -c file2 >> foo.gz
                    # adds file2 into foo.gz.

cat file1 file2 | gzip > foo.gz 
                    # gives better compression compared to above

zcat foo.gz = gunzip -c foo.gz = cat file1 file2 
                    # returns content of file1 and file2

