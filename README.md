When archiving files or converting the format in which archived files are saved, it can be useful to copy file creation timestamps across those files. This is not functionality which is typically exposed via most operating systems, but the original date is useful metadata which shouldn't be lost simply because it became necessary to format shift.

Here's a Bash function which copies the creation date from a source file to a target file.

```bash
#!/bin/bash

# fail on error
set -e

copy_timestamp() {
  source=$1
  target=$2
  # ensure both files exist
  if [ -f "${source}" ] && [ -f "${target}" ]; then
    # get timestamp from source file
    timestamp="$(stat -f%SB -t %Y%m%d%H%M "${file}")"
    # copy to target file
    touch -t "${timestamp}" "${target}"
  else
    exit 1
  fi
}
```

Cursory research leads me to believe that the technique above probably only works on MacOS and it may be picky about the formatting of the storage media. I don't really know because it worked for me so I promptly moved on with my life. I wish the same good fortunes for you.