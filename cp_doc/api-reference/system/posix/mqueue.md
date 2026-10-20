---
type: official-document
source_url: https://docs.bekencorp.com/arminodoc/bk_avdk_smp/cp_doc/bk7259/zh_CN/v4.0.1/api-reference/system/posix/mqueue.html
sdk_family: bk_avdk_smp
chip: BK7259
processor: CP
sdk_version: v4.0.1
language: zh_CN
fetched_at: '2026-10-20T16:59:36.586772+00:00'
mirror_status: current
---

<a id="mqueue"></a>

# mqueue接口介绍

> - 需要包含头文件#include \<posix/mqueue.h\>;
> - 定义了系统消息队列相关的接口

<a id="header-file"></a>

## Header File

- [mqueue.h](https://docs.bekencorp.com/arminodoc/bk_avdk_smp/cp_doc/bk7259/zh_CN/v4.0.1/_header_files/include/posix/mqueue.h)

<a id="functions"></a>

## Functions

<a id="_CPPv48mq_close5mqd_t"></a>

<a id="_CPPv38mq_close5mqd_t"></a> <a id="_CPPv28mq_close5mqd_t"></a> <a id="mq_close__mqd_t"></a> <a id="mqueue_8h_1a3fbd3906296be63451c64d69be2bc371"></a> int mq\_close([mqd\_t](#_CPPv45mqd_t "mqd_t") mqdes)
:   Close a message queue.

    <http://pubs.opengroup.org/onlinepubs/9699919799/functions/mq_close.html>

    @sideeffect Possible errno values

    EBADF \- The mqdes argument is not a valid message queue descriptor.

    Return values
    :   - **0** – \- Upon successful completion
        - **-1** – \- A error occurred. errno is also set.

<a id="_CPPv410mq_getattr5mqd_tP7mq_attr"></a>

<a id="_CPPv310mq_getattr5mqd_tP7mq_attr"></a> <a id="_CPPv210mq_getattr5mqd_tP7mq_attr"></a> <a id="mq_getattr__mqd_t.mq_attrP"></a> <a id="mqueue_8h_1a5a55ce03d8466a53a36601aaca9ee328"></a> int mq\_getattr([mqd\_t](#_CPPv45mqd_t "mqd_t") mqdes, struct [mq\_attr](#_CPPv47mq_attr "mq_attr") \*mqstat)
:   Get message queue attributes.

    <http://pubs.opengroup.org/onlinepubs/9699919799/functions/mq_getattr.html>

    @sideeffect Possible errno values

    DBADF \- The mqdes argument is not a valid message queue descriptor.

    Return values
    :   - **0** – \- Upon successful completion
        - **-1** – \- A error occurred. errno is also set.

<a id="_CPPv47mq_openPKci6mode_tP7mq_attr"></a>

<a id="_CPPv37mq_openPKci6mode_tP7mq_attr"></a> <a id="_CPPv27mq_openPKci6mode_tP7mq_attr"></a> <a id="mq_open__cCP.i.mode_t.mq_attrP"></a> <a id="mqueue_8h_1ade83e7ff8d3ed30d8641355377373638"></a> [mqd\_t](#_CPPv45mqd_t "mqd_t") mq\_open(const char \*name, int oflag, mode\_t mode, struct [mq\_attr](#_CPPv47mq_attr "mq_attr") \*attr)
:   Open a message queue.

    <http://pubs.opengroup.org/onlinepubs/9699919799/functions/mq_open.html>

    @sideeffect Possible errno values

    EINVAL \- name argument is invalid (not following name pattern), OR if O\_CREAT is specified in oflag with attr argument not NULL and either mq\_maxmsg or mq\_msgsize is equal to or less than zero, OR either O\_CREAT or O\_EXCL is not set and a queue with the same name is unlinked but pending to be removed.

    EEXIST \- O\_CREAT and O\_EXCL are set and the named message queue already exists.

    ENOSPC \- There is insufficient space for the creation of the new message queue.

    ENOENT \- O\_CREAT is not set and the named message queue does not exist.

    备注

    Supported name pattern: leading \<slash\> character in name is always required; the maximum length (excluding null-terminator) of the name argument can be NAME\_MAX. The default value of NAME\_MAX in FreeRTOS\_POSIX\_portable\_default.h is 64, which can be overwritten by user.

    备注

    mode argument is not supported.

    备注

    Supported oflags: O\_RDWR, O\_CREAT, O\_EXCL, and O\_NONBLOCK.

    Return values
    :   - **Message** – queue descriptor \&#8212; Upon successful completion
        - **(mqd\_t)** – \- 1 \&#8212; An error occurred. errno is also set.

<a id="_CPPv410mq_receive5mqd_tPc6size_tPj"></a>

<a id="_CPPv310mq_receive5mqd_tPc6size_tPj"></a> <a id="_CPPv210mq_receive5mqd_tPc6size_tPj"></a> <a id="mq_receive__mqd_t.cP.s.unsigned-iP"></a> <a id="mqueue_8h_1ab89c825740fe27d3821ccbe32bd68dfa"></a> ssize\_t mq\_receive([mqd\_t](#_CPPv45mqd_t "mqd_t") mqdes, char \*msg\_ptr, size\_t msg\_len, unsigned int \*msg\_prio)
:   Receive a message from a message queue.

    <http://pubs.opengroup.org/onlinepubs/9699919799/functions/mq_receive.html>

    @sideeffect Possible errno values

    EBADF \- The mqdes argument is not a valid message queue descriptor open for reading.

    EMSGSIZE \- The specified message buffer size, msg\_len, is less than the message size attribute of the message queue.

    ETIMEDOUT \- The O\_NONBLOCK flag was not set when the message queue was opened, but no message arrived on the queue before the specified timeout expired.

    EAGAIN \- O\_NONBLOCK was set in the message description associated with mqdes, and the specified message queue is empty.

    备注

    msg\_prio argument is not supported. Messages are not checked for corruption.

    Return values
    :   - **The** – length of the selected message in bytes \- Upon successful completion. The message is removed from the queue
        - **-1** – \- An error occurred. errno is also set.

<a id="_CPPv47mq_send5mqd_tPKc6size_tj"></a>

<a id="_CPPv37mq_send5mqd_tPKc6size_tj"></a> <a id="_CPPv27mq_send5mqd_tPKc6size_tj"></a> <a id="mq_send__mqd_t.cCP.s.unsigned"></a> <a id="mqueue_8h_1a753177f77f6eec2a80b57e8a68b36bed"></a> int mq\_send([mqd\_t](#_CPPv45mqd_t "mqd_t") mqdes, const char \*msg\_ptr, size\_t msg\_len, unsigned msg\_prio)
:   Send a message to a message queue.

    <http://pubs.opengroup.org/onlinepubs/9699919799/functions/mq_send.html>

    @sideeffect Possible errno values

    EBADF \- The mqdes argument is not a valid message queue descriptor open for writing.

    EMSGSIZE \- The specified message length, msg\_len, exceeds the message size attribute of the message queue, OR insufficient memory for the message to be sent.

    ETIMEDOUT \- The O\_NONBLOCK flag was not set when the message queue was opened, but the timeout expired before the message could be added to the queue.

    EAGAIN \- The O\_NONBLOCK flag is set in the message queue description associated with mqdes, and the specified message queue is full.

    备注

    msg\_prio argument is not supported.

    Return values
    :   - **0** – \- Upon successful completion.
        - **-1** – \- An error occurred. errno is also set.

<a id="_CPPv415mq_timedreceive5mqd_tPc6size_tPjPK8timespec"></a>

<a id="_CPPv315mq_timedreceive5mqd_tPc6size_tPjPK8timespec"></a> <a id="_CPPv215mq_timedreceive5mqd_tPc6size_tPjPK8timespec"></a> <a id="mq_timedreceive__mqd_t.cP.s.unsignedP.timespecCP"></a> <a id="mqueue_8h_1a8749e8f6d2efe37457e955a21ed98691"></a> ssize\_t mq\_timedreceive([mqd\_t](#_CPPv45mqd_t "mqd_t") mqdes, char \*msg\_ptr, size\_t msg\_len, unsigned \*msg\_prio, const struct [timespec](time.md#_CPPv48timespec "timespec") \*abstime)
:   Receive a message from a message queue with timeout.

    <http://pubs.opengroup.org/onlinepubs/9699919799/functions/mq_timedreceive.html>

    @sideeffect Possible errno values

    EBADF \- The mqdes argument is not a valid message queue descriptor open for reading.

    EMSGSIZE \- The specified message buffer size, msg\_len, is less than the message size attribute of the message queue.

    EINVAL \- The process or thread would have blocked, and the abstime parameter specified a nanoseconds field value less than zero or greater than or equal to 1000 million.

    ETIMEDOUT \- The O\_NONBLOCK flag was not set when the message queue was opened, but no message arrived on the queue before the specified timeout expired.

    EAGAIN \- O\_NONBLOCK was set in the message description associated with mqdes, and the specified message queue is empty.

    备注

    msg\_prio argument is not supported. Messages are not checked for corruption.

    Return values
    :   - **The** – length of the selected message in bytes \- Upon successful completion. The message is removed from the queue
        - **-1** – \- An error occurred. errno is also set.

<a id="_CPPv412mq_timedsend5mqd_tPKc6size_tjPK8timespec"></a>

<a id="_CPPv312mq_timedsend5mqd_tPKc6size_tjPK8timespec"></a> <a id="_CPPv212mq_timedsend5mqd_tPKc6size_tjPK8timespec"></a> <a id="mq_timedsend__mqd_t.cCP.s.unsigned.timespecCP"></a> <a id="mqueue_8h_1a021882ffe3cfd53c10d95d314b29ab2d"></a> int mq\_timedsend([mqd\_t](#_CPPv45mqd_t "mqd_t") mqdes, const char \*msg\_ptr, size\_t msg\_len, unsigned msg\_prio, const struct [timespec](time.md#_CPPv48timespec "timespec") \*abstime)
:   Send a message to a message queue with timeout.

    <http://pubs.opengroup.org/onlinepubs/9699919799/functions/mq_timedsend.html>

    @sideeffect Possible errno values

    EBADF \- The mqdes argument is not a valid message queue descriptor open for writing.

    EMSGSIZE \- The specified message length, msg\_len, exceeds the message size attribute of the message queue, OR insufficient memory for the message to be sent.

    EINVAL \- The process or thread would have blocked, and the abstime parameter specified a nanoseconds field value less than zero or greater than or equal to 1000 million.

    ETIMEDOUT \- The O\_NONBLOCK flag was not set when the message queue was opened, but the timeout expired before the message could be added to the queue.

    EAGAIN \- The O\_NONBLOCK flag is set in the message queue description associated with mqdes, and the specified message queue is full.

    备注

    msg\_prio argument is not supported.

    Return values
    :   - **0** – \- Upon successful completion.
        - **-1** – \- An error occurred. errno is also set.

<a id="_CPPv49mq_unlinkPKc"></a>

<a id="_CPPv39mq_unlinkPKc"></a> <a id="_CPPv29mq_unlinkPKc"></a> <a id="mq_unlink__cCP"></a> <a id="mqueue_8h_1accd8c5ee36e60d990963e1d544ef4140"></a> int mq\_unlink(const char \*name)
:   Remove a message queue.

    <http://pubs.opengroup.org/onlinepubs/9699919799/functions/mq_unlink.html>

    @sideeffect Possible errno values

    EINVAL \- name argument is invalid. Refer to requirements on name argument in

    [mq\_open()](#mqueue_8h_1ade83e7ff8d3ed30d8641355377373638)

    .

    ENOENT \- The named message queue does not exist.

    Return values
    :   - **0** – \- Upon successful completion.
        - **-1** – \- An error occurred. errno is also set.

<a id="structures"></a>

## Structures

<a id="_CPPv47mq_attr"></a>

<a id="_CPPv37mq_attr"></a> <a id="_CPPv27mq_attr"></a> <a id="mq_attr"></a> <a id="structmq__attr"></a> struct mq\_attr
:   Message queue attributes.

    <a id="breathe-section-title-public-members"></a>

    Public Members

    <a id="_CPPv4N7mq_attr8mq_flagsE"></a>

    <a id="_CPPv3N7mq_attr8mq_flagsE"></a> <a id="_CPPv2N7mq_attr8mq_flagsE"></a> <a id="mq_attr::mq_flags__l"></a> <a id="structmq__attr_1a19c05fa88c6d1126120d800647ddb0dd"></a> long mq\_flags
    :   Message queue flags.

    <a id="_CPPv4N7mq_attr9mq_maxmsgE"></a>

    <a id="_CPPv3N7mq_attr9mq_maxmsgE"></a> <a id="_CPPv2N7mq_attr9mq_maxmsgE"></a> <a id="mq_attr::mq_maxmsg__l"></a> <a id="structmq__attr_1aa535e1fa6c07c1d189e720ba15f9af08"></a> long mq\_maxmsg
    :   Maximum number of messages.

    <a id="_CPPv4N7mq_attr10mq_msgsizeE"></a>

    <a id="_CPPv3N7mq_attr10mq_msgsizeE"></a> <a id="_CPPv2N7mq_attr10mq_msgsizeE"></a> <a id="mq_attr::mq_msgsize__l"></a> <a id="structmq__attr_1ae975d1d907081c1e53b079c981c32209"></a> long mq\_msgsize
    :   Maximum message size.

    <a id="_CPPv4N7mq_attr10mq_curmsgsE"></a>

    <a id="_CPPv3N7mq_attr10mq_curmsgsE"></a> <a id="_CPPv2N7mq_attr10mq_curmsgsE"></a> <a id="mq_attr::mq_curmsgs__l"></a> <a id="structmq__attr_1a08cfd508cef817ba351c1af8d9af50f5"></a> long mq\_curmsgs
    :   Number of messages currently queued.

<a id="type-definitions"></a>

## Type Definitions

<a id="_CPPv45mqd_t"></a>

<a id="_CPPv35mqd_t"></a> <a id="_CPPv25mqd_t"></a> <a id="mqd_t"></a> <a id="mqueue_8h_1aa03ac56b19aba70879b7e2934da6a507"></a> typedef void \*mqd\_t
:   Message queue descriptor.
