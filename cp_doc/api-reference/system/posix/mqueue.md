# mqueue接口介绍

> - 需要包含头文件#include <posix/mqueue.h>;
> - 定义了系统消息队列相关的接口



## Header File


- [mqueue.h](http://192.168.0.46/gerrit/plugins/gitiles/iot/wcn/projects/+/refs/heads/armino_main/components/mqueue.h "http://192.168.0.46/gerrit/plugins/gitiles/iot/wcn/projects/+/refs/heads/armino_main/components/mqueue.h")


## Functions

int mq_close([mqd_t](#_CPPv45mqd_t "mqd_t") mqdes)
:   Close a message queue.

    [http://pubs.opengroup.org/onlinepubs/9699919799/functions/mq_close.html](http://pubs.opengroup.org/onlinepubs/9699919799/functions/mq_close.html "http://pubs.opengroup.org/onlinepubs/9699919799/functions/mq_close.html")

    @sideeffect Possible errno values

    EBADF - The mqdes argument is not a valid message queue descriptor.

    Return values
    :   - **0** – - Upon successful completion

        - **-1** – - A error occurred. errno is also set.

int mq_getattr([mqd_t](#_CPPv45mqd_t "mqd_t") mqdes, struct [mq_attr](#_CPPv47mq_attr "mq_attr") *mqstat)
:   Get message queue attributes.

    [http://pubs.opengroup.org/onlinepubs/9699919799/functions/mq_getattr.html](http://pubs.opengroup.org/onlinepubs/9699919799/functions/mq_getattr.html "http://pubs.opengroup.org/onlinepubs/9699919799/functions/mq_getattr.html")

    @sideeffect Possible errno values

    DBADF - The mqdes argument is not a valid message queue descriptor.

    Return values
    :   - **0** – - Upon successful completion

        - **-1** – - A error occurred. errno is also set.

[mqd_t](#_CPPv45mqd_t "mqd_t") mq_open(const char *name, int oflag, mode_t mode, struct [mq_attr](#_CPPv47mq_attr "mq_attr") *attr)
:   Open a message queue.

    [http://pubs.opengroup.org/onlinepubs/9699919799/functions/mq_open.html](http://pubs.opengroup.org/onlinepubs/9699919799/functions/mq_open.html "http://pubs.opengroup.org/onlinepubs/9699919799/functions/mq_open.html")

    @sideeffect Possible errno values

    EINVAL - name argument is invalid (not following name pattern), OR if O_CREAT is specified in oflag with attr argument not NULL and either mq_maxmsg or mq_msgsize is equal to or less than zero, OR either O_CREAT or O_EXCL is not set and a queue with the same name is unlinked but pending to be removed.

    EEXIST - O_CREAT and O_EXCL are set and the named message queue already exists.

    ENOSPC - There is insufficient space for the creation of the new message queue.

    ENOENT - O_CREAT is not set and the named message queue does not exist.

    备注

    Supported name pattern: leading <slash> character in name is always required; the maximum length (excluding null-terminator) of the name argument can be NAME_MAX. The default value of NAME_MAX in FreeRTOS_POSIX_portable_default.h is 64, which can be overwritten by user.

    备注

    mode argument is not supported.

    备注

    Supported oflags: O_RDWR, O_CREAT, O_EXCL, and O_NONBLOCK.

    Return values
    :   - **Message** – queue descriptor &#8212; Upon successful completion

        - **(mqd_t)** – - 1 &#8212; An error occurred. errno is also set.

ssize_t mq_receive([mqd_t](#_CPPv45mqd_t "mqd_t") mqdes, char *msg_ptr, size_t msg_len, unsigned int *msg_prio)
:   Receive a message from a message queue.

    [http://pubs.opengroup.org/onlinepubs/9699919799/functions/mq_receive.html](http://pubs.opengroup.org/onlinepubs/9699919799/functions/mq_receive.html "http://pubs.opengroup.org/onlinepubs/9699919799/functions/mq_receive.html")

    @sideeffect Possible errno values

    EBADF - The mqdes argument is not a valid message queue descriptor open for reading.

    EMSGSIZE - The specified message buffer size, msg_len, is less than the message size attribute of the message queue.

    ETIMEDOUT - The O_NONBLOCK flag was not set when the message queue was opened, but no message arrived on the queue before the specified timeout expired.

    EAGAIN - O_NONBLOCK was set in the message description associated with mqdes, and the specified message queue is empty.

    备注

    msg_prio argument is not supported. Messages are not checked for corruption.

    Return values
    :   - **The** – length of the selected message in bytes - Upon successful completion. The message is removed from the queue

        - **-1** – - An error occurred. errno is also set.

int mq_send([mqd_t](#_CPPv45mqd_t "mqd_t") mqdes, const char *msg_ptr, size_t msg_len, unsigned msg_prio)
:   Send a message to a message queue.

    [http://pubs.opengroup.org/onlinepubs/9699919799/functions/mq_send.html](http://pubs.opengroup.org/onlinepubs/9699919799/functions/mq_send.html "http://pubs.opengroup.org/onlinepubs/9699919799/functions/mq_send.html")

    @sideeffect Possible errno values

    EBADF - The mqdes argument is not a valid message queue descriptor open for writing.

    EMSGSIZE - The specified message length, msg_len, exceeds the message size attribute of the message queue, OR insufficient memory for the message to be sent.

    ETIMEDOUT - The O_NONBLOCK flag was not set when the message queue was opened, but the timeout expired before the message could be added to the queue.

    EAGAIN - The O_NONBLOCK flag is set in the message queue description associated with mqdes, and the specified message queue is full.

    备注

    msg_prio argument is not supported.

    Return values
    :   - **0** – - Upon successful completion.

        - **-1** – - An error occurred. errno is also set.

ssize_t mq_timedreceive([mqd_t](#_CPPv45mqd_t "mqd_t") mqdes, char *msg_ptr, size_t msg_len, unsigned *msg_prio, const struct [timespec](time.md#_CPPv48timespec "timespec") *abstime)
:   Receive a message from a message queue with timeout.

    [http://pubs.opengroup.org/onlinepubs/9699919799/functions/mq_timedreceive.html](http://pubs.opengroup.org/onlinepubs/9699919799/functions/mq_timedreceive.html "http://pubs.opengroup.org/onlinepubs/9699919799/functions/mq_timedreceive.html")

    @sideeffect Possible errno values

    EBADF - The mqdes argument is not a valid message queue descriptor open for reading.

    EMSGSIZE - The specified message buffer size, msg_len, is less than the message size attribute of the message queue.

    EINVAL - The process or thread would have blocked, and the abstime parameter specified a nanoseconds field value less than zero or greater than or equal to 1000 million.

    ETIMEDOUT - The O_NONBLOCK flag was not set when the message queue was opened, but no message arrived on the queue before the specified timeout expired.

    EAGAIN - O_NONBLOCK was set in the message description associated with mqdes, and the specified message queue is empty.

    备注

    msg_prio argument is not supported. Messages are not checked for corruption.

    Return values
    :   - **The** – length of the selected message in bytes - Upon successful completion. The message is removed from the queue

        - **-1** – - An error occurred. errno is also set.

int mq_timedsend([mqd_t](#_CPPv45mqd_t "mqd_t") mqdes, const char *msg_ptr, size_t msg_len, unsigned msg_prio, const struct [timespec](time.md#_CPPv48timespec "timespec") *abstime)
:   Send a message to a message queue with timeout.

    [http://pubs.opengroup.org/onlinepubs/9699919799/functions/mq_timedsend.html](http://pubs.opengroup.org/onlinepubs/9699919799/functions/mq_timedsend.html "http://pubs.opengroup.org/onlinepubs/9699919799/functions/mq_timedsend.html")

    @sideeffect Possible errno values

    EBADF - The mqdes argument is not a valid message queue descriptor open for writing.

    EMSGSIZE - The specified message length, msg_len, exceeds the message size attribute of the message queue, OR insufficient memory for the message to be sent.

    EINVAL - The process or thread would have blocked, and the abstime parameter specified a nanoseconds field value less than zero or greater than or equal to 1000 million.

    ETIMEDOUT - The O_NONBLOCK flag was not set when the message queue was opened, but the timeout expired before the message could be added to the queue.

    EAGAIN - The O_NONBLOCK flag is set in the message queue description associated with mqdes, and the specified message queue is full.

    备注

    msg_prio argument is not supported.

    Return values
    :   - **0** – - Upon successful completion.

        - **-1** – - An error occurred. errno is also set.

int mq_unlink(const char *name)
:   Remove a message queue.

    [http://pubs.opengroup.org/onlinepubs/9699919799/functions/mq_unlink.html](http://pubs.opengroup.org/onlinepubs/9699919799/functions/mq_unlink.html "http://pubs.opengroup.org/onlinepubs/9699919799/functions/mq_unlink.html")

    @sideeffect Possible errno values

    EINVAL - name argument is invalid. Refer to requirements on name argument in

    [mq_open()](#mqueue_8h_1ade83e7ff8d3ed30d8641355377373638 "#mqueue_8h_1ade83e7ff8d3ed30d8641355377373638")

    .

    ENOENT - The named message queue does not exist.

    Return values
    :   - **0** – - Upon successful completion.

        - **-1** – - An error occurred. errno is also set.


## Structures

struct mq_attr
:   Message queue attributes.

    Public Members

    long mq_flags
    :   Message queue flags.

    long mq_maxmsg
    :   Maximum number of messages.

    long mq_msgsize
    :   Maximum message size.

    long mq_curmsgs
    :   Number of messages currently queued.


## Type Definitions

typedef void *mqd_t
:   Message queue descriptor.
