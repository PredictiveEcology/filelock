# filelock (development version)

* `unlock()` gains `remove`: `unlock(lock, remove = TRUE)` deletes the lock file before releasing an
  exclusive lock, so lock files exist only while in use. `lock()` now checks that the file it locked is
  still the one at `path`, and starts over if it was deleted while it waited, so deleting is safe.
  `remove` is ignored on Windows.

* `lock()` now closes the lock file if it fails to acquire the lock,
  because of a timeout, an error or an interrupt. Before, every failed
  `lock()` call leaked a file descriptor (a file handle on Windows) (#28).

* Error messages now include the path of the lock file when locking fails,
  and follow the tidyverse error style, e.g. "Can't open lock file
  `<path>`: Permission denied." (#30).

# filelock 1.0.3

* No user visible changes.

# filelock 1.0.2

* `lock()` now removes the timer on Unix, to avoid undefined behavior in
  non-interactive R sessions, when a SIGALRM is delivered after the process
  acquired the lock.

# filelock 1.0.1

First public release.
