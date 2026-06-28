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


