---
type: official-document
source_url: https://docs.bekencorp.com/arminodoc/bk_avdk_smp/ap_doc/bk7258/zh_CN/v3.1.1/api-reference/system/posix/fcntl.html
sdk_family: bk_avdk_smp
chip: BK7258
processor: AP
sdk_version: v3.1.1
language: zh_CN
fetched_at: '2026-10-20T16:59:36.586772+00:00'
mirror_status: current
---

<a id="fcntl"></a>

# fcntl接口介绍

> - 需要包含头文件#include \<posix/fcntl.h\>;
> - 定义了posix接口file cntrol相关的宏定义

<a id="header-file"></a>

## Header File

- [fcntl.h](https://docs.bekencorp.com/arminodoc/bk_avdk_smp/ap_doc/bk7258/zh_CN/v3.1.1/_header_files/include/posix/fcntl.h)

<a id="macros"></a>

## Macros

<a id="c.O_CLOEXEC"></a>

<a id="fcntl_8h_1ad6d8fbe4e494b4dbe051612572d3f757"></a> O\_CLOEXEC
:   Close the file descriptor upon exec().

<a id="c.O_CREAT"></a>

<a id="fcntl_8h_1a1cf6b1de1fffedaa1d26b189e9a8d2cc"></a> O\_CREAT
:   Create file if it does not exist.

<a id="c.O_DIRECTORY"></a>

<a id="fcntl_8h_1a6afd3dd2f570069804b40e6aa24fc966"></a> O\_DIRECTORY
:   Fail if file is a non-directory file.

<a id="c.O_EXCL"></a>

<a id="fcntl_8h_1a9f5acfe79fafe14b6694447bd0e9f10b"></a> O\_EXCL
:   Exclusive use flag.

<a id="c.O_NOCTTY"></a>

<a id="fcntl_8h_1a2e375ab32c7ef4581b026be28e4cc116"></a> O\_NOCTTY
:   Do not assign controlling terminal.

<a id="c.O_NOFOLLOW"></a>

<a id="fcntl_8h_1a82d4d551b214905742c9e045185d352a"></a> O\_NOFOLLOW
:   Do not follow symbolic links.

<a id="c.O_TRUNC"></a>

<a id="fcntl_8h_1ad1d67e453fb3031f40f8cd3403773813"></a> O\_TRUNC
:   Truncate flag.

<a id="c.O_TTY_INIT"></a>

<a id="fcntl_8h_1a0ee7b090d0fd09015039f6325118400f"></a> O\_TTY\_INIT
:   termios structure provides conforming behavior.

<a id="c.O_APPEND"></a>

<a id="fcntl_8h_1ae036f789407d21f07b211552d67b3214"></a> O\_APPEND
:   Set append mode.

<a id="c.O_DSYNC"></a>

<a id="fcntl_8h_1af63e33218e573b9461b5f17d0ea79f2a"></a> O\_DSYNC
:   Write according to synchronized I/O data integrity completion.

<a id="c.O_NONBLOCK"></a>

<a id="fcntl_8h_1a39d33ce33804efd4d52606d59071c6d8"></a> O\_NONBLOCK
:   Non-blocking mode.

<a id="c.O_RSYNC"></a>

<a id="fcntl_8h_1ac9cf617d7c8fba45a5062f1f7322e6f8"></a> O\_RSYNC
:   Synchronized read I/O operations.

<a id="c.O_SYNC"></a>

<a id="fcntl_8h_1aae85139bfa94236d126bb1e3b772998f"></a> O\_SYNC
:   Write according to synchronized I/O file integrity completion.

<a id="c.O_ACCMODE"></a>

<a id="fcntl_8h_1a4dc4d45e07d2abc899bcaf04b2846a87"></a> O\_ACCMODE

<a id="c.O_EXEC"></a>

<a id="fcntl_8h_1a459542206659fbe295eb4183f8b8f06c"></a> O\_EXEC
:   Open for execute only (non-directory files).

<a id="c.O_RDONLY"></a>

<a id="fcntl_8h_1a7a68c9ffaac7dbcd652225dd7c06a54b"></a> O\_RDONLY
:   Open for reading only.

<a id="c.O_RDWR"></a>

<a id="fcntl_8h_1abb0586253488ee61072b73557eeb873b"></a> O\_RDWR
:   Open for reading and writing.

<a id="c.O_SEARCH"></a>

<a id="fcntl_8h_1ac7984b2eaa7166aea31f0c4f6c91fb2d"></a> O\_SEARCH
:   Open directory for search only.

<a id="c.O_WRONLY"></a>

<a id="fcntl_8h_1a11b644a8526139c4cc1850dac1271ced"></a> O\_WRONLY
:   Open for writing only.
