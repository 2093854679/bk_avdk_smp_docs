# Audio Port


The Audio port is an abstract class. Based on this class, three types of ports are implemented, namely callback port, ringbuffer port, and framebuffer port.
Each type of port has a corresponding creation interface, and other control functions are uniformly managed using the interfaces provided by the audio port.


## API Reference


### Header File


- [bk_audio/audio_pipeline/audio_port.h](http://192.168.0.46/gerrit/plugins/gitiles/iot/wcn/projects/+/refs/heads/armino_main/components/bk_audio/audio_pipeline/audio_port.h "http://192.168.0.46/gerrit/plugins/gitiles/iot/wcn/projects/+/refs/heads/armino_main/components/bk_audio/audio_pipeline/audio_port.h")


### Functions

[audio_port_handle_t](#_CPPv419audio_port_handle_t "audio_port_handle_t") audio_port_init([audio_port_cfg_t](#_CPPv416audio_port_cfg_t "audio_port_cfg_t") *config)

[bk_err_t](../../../system/os.md#_CPPv48bk_err_t "bk_err_t") audio_port_deinit([audio_port_handle_t](#_CPPv419audio_port_handle_t "audio_port_handle_t") port)

[bk_err_t](../../../system/os.md#_CPPv48bk_err_t "bk_err_t") audio_port_set_tag([audio_port_handle_t](#_CPPv419audio_port_handle_t "audio_port_handle_t") port, const char *tag)

char *audio_port_get_tag([audio_port_handle_t](#_CPPv419audio_port_handle_t "audio_port_handle_t") port)

[bk_err_t](../../../system/os.md#_CPPv48bk_err_t "bk_err_t") audio_port_open([audio_port_handle_t](#_CPPv419audio_port_handle_t "audio_port_handle_t") port)

[bk_err_t](../../../system/os.md#_CPPv48bk_err_t "bk_err_t") audio_port_close([audio_port_handle_t](#_CPPv419audio_port_handle_t "audio_port_handle_t") port)

[bk_err_t](../../../system/os.md#_CPPv48bk_err_t "bk_err_t") audio_port_abort([audio_port_handle_t](#_CPPv419audio_port_handle_t "audio_port_handle_t") port)

[bk_err_t](../../../system/os.md#_CPPv48bk_err_t "bk_err_t") audio_port_reset([audio_port_handle_t](#_CPPv419audio_port_handle_t "audio_port_handle_t") port)

[bk_err_t](../../../system/os.md#_CPPv48bk_err_t "bk_err_t") audio_port_read([audio_port_handle_t](#_CPPv419audio_port_handle_t "audio_port_handle_t") port, char *buffer, int len, TickType_t ticks_to_wait)

[bk_err_t](../../../system/os.md#_CPPv48bk_err_t "bk_err_t") audio_port_write([audio_port_handle_t](#_CPPv419audio_port_handle_t "audio_port_handle_t") port, char *buffer, int len, TickType_t ticks_to_wait)

[bk_err_t](../../../system/os.md#_CPPv48bk_err_t "bk_err_t") audio_port_write_done([audio_port_handle_t](#_CPPv419audio_port_handle_t "audio_port_handle_t") port)

[bk_err_t](../../../system/os.md#_CPPv48bk_err_t "bk_err_t") audio_port_get_size([audio_port_handle_t](#_CPPv419audio_port_handle_t "audio_port_handle_t") port)

[bk_err_t](../../../system/os.md#_CPPv48bk_err_t "bk_err_t") audio_port_get_filled_size([audio_port_handle_t](#_CPPv419audio_port_handle_t "audio_port_handle_t") port)

[bk_err_t](../../../system/os.md#_CPPv48bk_err_t "bk_err_t") audio_port_get_free_size([audio_port_handle_t](#_CPPv419audio_port_handle_t "audio_port_handle_t") port)

[bk_err_t](../../../system/os.md#_CPPv48bk_err_t "bk_err_t") audio_port_set_data([audio_port_handle_t](#_CPPv419audio_port_handle_t "audio_port_handle_t") port, void *data)

void *audio_port_get_data([audio_port_handle_t](#_CPPv419audio_port_handle_t "audio_port_handle_t") port)

[bk_err_t](../../../system/os.md#_CPPv48bk_err_t "bk_err_t") audio_port_set_type([audio_port_handle_t](#_CPPv419audio_port_handle_t "audio_port_handle_t") port, [port_type_t](#_CPPv411port_type_t "port_type_t") type)

[bk_err_t](../../../system/os.md#_CPPv48bk_err_t "bk_err_t") audio_port_get_type([audio_port_handle_t](#_CPPv419audio_port_handle_t "audio_port_handle_t") port)


### Structures

struct audio_port_cfg_t
:   Audio Port configurations. Each Element at startup will be a self-running task. These tasks will execute the callback open -> [loop: read -> write] -> close. These callback functions are provided by the user corresponding to this configuration.


### Macros

PORT_OK

PORT_FAIL

PORT_DONE

PORT_ABORT

PORT_TIMEOUT

PORT_SIZE_OUT_RANGE


### Type Definitions

typedef struct audio_port *audio_port_handle_t

typedef [bk_err_t](../../../system/os.md#_CPPv48bk_err_t "bk_err_t") (*port_io_func)([audio_port_handle_t](#_CPPv419audio_port_handle_t "audio_port_handle_t") self)

typedef int (*port_stream_func)([audio_port_handle_t](#_CPPv419audio_port_handle_t "audio_port_handle_t") self, char *buffer, int len, TickType_t ticks_to_wait, void *context)


### Enumerations

enum port_type_t
:   *Values:*

    enumerator PORT_TYPE_RB

    enumerator PORT_TYPE_FB

    enumerator PORT_TYPE_CB


### Header File


- [bk_audio/audio_pipeline/cb_port.h](http://192.168.0.46/gerrit/plugins/gitiles/iot/wcn/projects/+/refs/heads/armino_main/components/bk_audio/audio_pipeline/cb_port.h "http://192.168.0.46/gerrit/plugins/gitiles/iot/wcn/projects/+/refs/heads/armino_main/components/bk_audio/audio_pipeline/cb_port.h")


### Functions

[audio_port_handle_t](#_CPPv419audio_port_handle_t "audio_port_handle_t") callback_port_init([callback_port_cfg_t](#_CPPv419callback_port_cfg_t "callback_port_cfg_t") *config)


### Structures

struct callback_port_cfg_t


### Macros

CALLBACK_PORT_CFG_DEFAULT()


### Header File


- [bk_audio/audio_pipeline/rb_port.h](http://192.168.0.46/gerrit/plugins/gitiles/iot/wcn/projects/+/refs/heads/armino_main/components/bk_audio/audio_pipeline/rb_port.h "http://192.168.0.46/gerrit/plugins/gitiles/iot/wcn/projects/+/refs/heads/armino_main/components/bk_audio/audio_pipeline/rb_port.h")


### Functions

[audio_port_handle_t](#_CPPv419audio_port_handle_t "audio_port_handle_t") ringbuf_port_init([ringbuf_port_cfg_t](#_CPPv418ringbuf_port_cfg_t "ringbuf_port_cfg_t") *config)


### Structures

struct ringbuf_port_cfg_t


### Macros

RINGBUF_PORT_RINGBUF_SIZE

RINGBUF_PORT_CFG_DEFAULT()


### Header File


- [bk_audio/audio_pipeline/fb_port.h](http://192.168.0.46/gerrit/plugins/gitiles/iot/wcn/projects/+/refs/heads/armino_main/components/bk_audio/audio_pipeline/fb_port.h "http://192.168.0.46/gerrit/plugins/gitiles/iot/wcn/projects/+/refs/heads/armino_main/components/bk_audio/audio_pipeline/fb_port.h")


### Functions

[audio_port_handle_t](#_CPPv419audio_port_handle_t "audio_port_handle_t") framebuf_port_init([framebuf_port_cfg_t](#_CPPv419framebuf_port_cfg_t "framebuf_port_cfg_t") *config)


### Structures

struct framebuf_port_cfg_t


### Macros

FRAMEBUF_PORT_NODE_SIZE

FRAMEBUF_PORT_NODE_NUM

FRAMEBUF_PORT_CFG_DEFAULT()
