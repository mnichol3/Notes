# Miscellaneous Commands

Here is a collection of helpful commands I've compiled over the years

* See the 20 newest files in a directory, updated every 3 seconds
  ```
  watch -n 3 "ls -ltr|tail -20"
  ```
  
* Get the size of a directory
  ```
  du -sh /path/to/dir
  ```
  Note: May need to append `sudo`
  
* Count the number of lines of code in a git repository (only .py source files in this ex)
  ```
  git ls-files | grep py | xargs wc -l
  ```
  
* Kill stopped jobs
  ```
  kill -9 `jobs -ps`
  ```
  
* View memoery usage (in mb)
  ```
  free -m
  ```
  
* Download files from NOAA NCEI/NCDC via ftp
  ```
  ftp ftp.bou.class.noaa.gov
  prompt
  cd <subdir>
  cd <sub-subdir>
  mget *.nc
  ```
  
  or 
  
  ```
  ftp ftp.ncdc.noaa.gov
  prompt
  cd <subdir>
  cd <sub-subdir>
  mget *.nc
  ```
  
* Recursively unzip `.gz` files in the current directory & its subdirectories
  ```
  gunzip -d -f $(find ./ -type f -name '*.gz')
  ```
  
* Download a video using **`ffmpeg`** and a `.m3u8` playlist file
  ```
  ffmpeg -i "[url.m3u8]" -acodec copy -bsf:a aac_adtstoasc -vcodec copy [fname.mp4]
  ```
