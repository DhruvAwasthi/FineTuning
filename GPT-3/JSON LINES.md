# JSON Lines 
JSON Lines text format, also called newline-delimited JSON. JSON Lines  
is a convenient format for storing structured data that may be processed  
one record at a time. It works well with unix-style text processing  
tolls and shell pipelines. It's a great format for log files. It's also  
flexible format for passing messages between cooperating processes.  
<br>
The JSON Lines format has three requirements:
1. UTF-8 encoding,
2. Each line is a valid JSON value, and
3. Line separator is `\n`  


JSON Lines files may be saved with the file extension `.jsonl`.  
<br>  
Stream compressors like `gzip` or `bzip2` are recommended for saving  
space, resulting in `.jsonl.gz` or `.jsonl.bz2` files. 
