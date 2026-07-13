# fcntl接口介绍

> - 需要包含头文件#include <posix/fcntl.h>;
> - 定义了posix接口file cntrol相关的宏定义



## Header File


- [fcntl.h](http://192.168.0.46/gerrit/plugins/gitiles/iot/wcn/projects/+/refs/heads/armino_main/components/fcntl.h "http://192.168.0.46/gerrit/plugins/gitiles/iot/wcn/projects/+/refs/heads/armino_main/components/fcntl.h")


## Macros

O_CLOEXEC
:   Close the file descriptor upon exec().

O_CREAT
:   Create file if it does not exist.

O_DIRECTORY
:   Fail if file is a non-directory file.

O_EXCL
:   Exclusive use flag.

O_NOCTTY
:   Do not assign controlling terminal.

O_NOFOLLOW
:   Do not follow symbolic links.

O_TRUNC
:   Truncate flag.

O_TTY_INIT
:   termios structure provides conforming behavior.

O_APPEND
:   Set append mode.

O_DSYNC
:   Write according to synchronized I/O data integrity completion.

O_NONBLOCK
:   Non-blocking mode.

O_RSYNC
:   Synchronized read I/O operations.

O_SYNC
:   Write according to synchronized I/O file integrity completion.

O_ACCMODE

O_EXEC
:   Open for execute only (non-directory files).

O_RDONLY
:   Open for reading only.

O_RDWR
:   Open for reading and writing.

O_SEARCH
:   Open directory for search only.

O_WRONLY
:   Open for writing only.
