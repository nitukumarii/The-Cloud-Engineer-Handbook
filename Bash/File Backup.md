#!/bin/bash

backup_dir="/path/to/backup"
source_dir="/path/to/source"

tar -czf "$backup_dir/backup_$(date +%Y%m%d_%H%M%S).tar.gz" "$source_dir"




**How do you restore the backup?**

tar -xzf backup_20260728_153045.tar.gz

Options:

-x → Extract
-z → Decompress gzip
-f → Specify the archive file


<img width="357" height="245" alt="image" src="https://github.com/user-attachments/assets/e3c2d743-c638-49e3-9e88-b965195dad23" />




