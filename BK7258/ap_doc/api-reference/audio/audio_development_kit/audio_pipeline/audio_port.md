---
type: official-document
source_url: https://docs.bekencorp.com/arminodoc/bk_avdk_smp/ap_doc/bk7258/zh_CN/v3.1.1/api-reference/audio/audio_development_kit/audio_pipeline/audio_port.html
sdk_family: bk_avdk_smp
chip: BK7258
processor: AP
sdk_version: v3.1.1
language: zh_CN
fetched_at: '2026-10-20T16:59:36.586772+00:00'
mirror_status: current
---

<a id="audio-port"></a>

# Audio Port

The Audio port is an abstract class. Based on this class, three types of ports are implemented, namely callback port, ringbuffer port, and framebuffer port.
Each type of port has a corresponding creation interface, and other control functions are uniformly managed using the interfaces provided by the audio port.

<a id="api-reference"></a>

## API Reference

<a id="header-file"></a>

### Header File

- [audio\_port.h](https://docs.bekencorp.com/arminodoc/bk_avdk_smp/ap_doc/bk7258/zh_CN/v3.1.1/_header_files/include/components/bk_audio/audio_pipeline/audio_port.h)

<a id="functions"></a>

### Functions

<a id="_CPPv415audio_port_initP16audio_port_cfg_t"></a>

<a id="_CPPv315audio_port_initP16audio_port_cfg_t"></a> <a id="_CPPv215audio_port_initP16audio_port_cfg_t"></a> <a id="audio_port_init__audio_port_cfg_tP"></a> <a id="audio__port_8h_1aab66b05dbaf65a93deb19d08b7fb55f2"></a> [audio\_port\_handle\_t](#_CPPv419audio_port_handle_t "audio_port_handle_t") audio\_port\_init([audio\_port\_cfg\_t](#_CPPv416audio_port_cfg_t "audio_port_cfg_t") \*config)

<a id="_CPPv417audio_port_deinit19audio_port_handle_t"></a>

<a id="_CPPv317audio_port_deinit19audio_port_handle_t"></a> <a id="_CPPv217audio_port_deinit19audio_port_handle_t"></a> <a id="audio_port_deinit__audio_port_handle_t"></a> <a id="audio__port_8h_1aad4690e7ba020e28e0f06bad3d7ebb64"></a> [bk\_err\_t](../../../system/os.md#_CPPv48bk_err_t "bk_err_t") audio\_port\_deinit([audio\_port\_handle\_t](#_CPPv419audio_port_handle_t "audio_port_handle_t") port)

<a id="_CPPv418audio_port_set_tag19audio_port_handle_tPKc"></a>

<a id="_CPPv318audio_port_set_tag19audio_port_handle_tPKc"></a> <a id="_CPPv218audio_port_set_tag19audio_port_handle_tPKc"></a> <a id="audio_port_set_tag__audio_port_handle_t.cCP"></a> <a id="audio__port_8h_1a8321b80e3a7cb8cd6c573c2d1244dba2"></a> [bk\_err\_t](../../../system/os.md#_CPPv48bk_err_t "bk_err_t") audio\_port\_set\_tag([audio\_port\_handle\_t](#_CPPv419audio_port_handle_t "audio_port_handle_t") port, const char \*tag)

<a id="_CPPv418audio_port_get_tag19audio_port_handle_t"></a>

<a id="_CPPv318audio_port_get_tag19audio_port_handle_t"></a> <a id="_CPPv218audio_port_get_tag19audio_port_handle_t"></a> <a id="audio_port_get_tag__audio_port_handle_t"></a> <a id="audio__port_8h_1a555d08eed522de398c6122bb4401d4f1"></a> char \*audio\_port\_get\_tag([audio\_port\_handle\_t](#_CPPv419audio_port_handle_t "audio_port_handle_t") port)

<a id="_CPPv415audio_port_open19audio_port_handle_t"></a>

<a id="_CPPv315audio_port_open19audio_port_handle_t"></a> <a id="_CPPv215audio_port_open19audio_port_handle_t"></a> <a id="audio_port_open__audio_port_handle_t"></a> <a id="audio__port_8h_1a1004476d7270f8f0fafecb58ac3559f9"></a> [bk\_err\_t](../../../system/os.md#_CPPv48bk_err_t "bk_err_t") audio\_port\_open([audio\_port\_handle\_t](#_CPPv419audio_port_handle_t "audio_port_handle_t") port)

<a id="_CPPv416audio_port_close19audio_port_handle_t"></a>

<a id="_CPPv316audio_port_close19audio_port_handle_t"></a> <a id="_CPPv216audio_port_close19audio_port_handle_t"></a> <a id="audio_port_close__audio_port_handle_t"></a> <a id="audio__port_8h_1ab771f79c72268949d75495ee3291dea7"></a> [bk\_err\_t](../../../system/os.md#_CPPv48bk_err_t "bk_err_t") audio\_port\_close([audio\_port\_handle\_t](#_CPPv419audio_port_handle_t "audio_port_handle_t") port)

<a id="_CPPv416audio_port_abort19audio_port_handle_t"></a>

<a id="_CPPv316audio_port_abort19audio_port_handle_t"></a> <a id="_CPPv216audio_port_abort19audio_port_handle_t"></a> <a id="audio_port_abort__audio_port_handle_t"></a> <a id="audio__port_8h_1aad1e48865255598058fa40bce27fa1c3"></a> [bk\_err\_t](../../../system/os.md#_CPPv48bk_err_t "bk_err_t") audio\_port\_abort([audio\_port\_handle\_t](#_CPPv419audio_port_handle_t "audio_port_handle_t") port)

<a id="_CPPv416audio_port_reset19audio_port_handle_t"></a>

<a id="_CPPv316audio_port_reset19audio_port_handle_t"></a> <a id="_CPPv216audio_port_reset19audio_port_handle_t"></a> <a id="audio_port_reset__audio_port_handle_t"></a> <a id="audio__port_8h_1ace38c40f835b3168e9d807b1e9ea0054"></a> [bk\_err\_t](../../../system/os.md#_CPPv48bk_err_t "bk_err_t") audio\_port\_reset([audio\_port\_handle\_t](#_CPPv419audio_port_handle_t "audio_port_handle_t") port)

<a id="_CPPv415audio_port_read19audio_port_handle_tPci10TickType_t"></a>

<a id="_CPPv315audio_port_read19audio_port_handle_tPci10TickType_t"></a> <a id="_CPPv215audio_port_read19audio_port_handle_tPci10TickType_t"></a> <a id="audio_port_read__audio_port_handle_t.cP.i.TickType_t"></a> <a id="audio__port_8h_1a5166672e15cbfa90921512f72c2a0156"></a> [bk\_err\_t](../../../system/os.md#_CPPv48bk_err_t "bk_err_t") audio\_port\_read([audio\_port\_handle\_t](#_CPPv419audio_port_handle_t "audio_port_handle_t") port, char \*buffer, int len, TickType\_t ticks\_to\_wait)

<a id="_CPPv416audio_port_write19audio_port_handle_tPci10TickType_t"></a>

<a id="_CPPv316audio_port_write19audio_port_handle_tPci10TickType_t"></a> <a id="_CPPv216audio_port_write19audio_port_handle_tPci10TickType_t"></a> <a id="audio_port_write__audio_port_handle_t.cP.i.TickType_t"></a> <a id="audio__port_8h_1a73bd831c58b1d35f8fa90167e6410b7f"></a> [bk\_err\_t](../../../system/os.md#_CPPv48bk_err_t "bk_err_t") audio\_port\_write([audio\_port\_handle\_t](#_CPPv419audio_port_handle_t "audio_port_handle_t") port, char \*buffer, int len, TickType\_t ticks\_to\_wait)

<a id="_CPPv421audio_port_write_done19audio_port_handle_t"></a>

<a id="_CPPv321audio_port_write_done19audio_port_handle_t"></a> <a id="_CPPv221audio_port_write_done19audio_port_handle_t"></a> <a id="audio_port_write_done__audio_port_handle_t"></a> <a id="audio__port_8h_1a34e17e33fa4e77ebba68618193f0a5cc"></a> [bk\_err\_t](../../../system/os.md#_CPPv48bk_err_t "bk_err_t") audio\_port\_write\_done([audio\_port\_handle\_t](#_CPPv419audio_port_handle_t "audio_port_handle_t") port)

<a id="_CPPv419audio_port_get_size19audio_port_handle_t"></a>

<a id="_CPPv319audio_port_get_size19audio_port_handle_t"></a> <a id="_CPPv219audio_port_get_size19audio_port_handle_t"></a> <a id="audio_port_get_size__audio_port_handle_t"></a> <a id="audio__port_8h_1a57ace2c0013c63f6c5e4277d2b89026e"></a> [bk\_err\_t](../../../system/os.md#_CPPv48bk_err_t "bk_err_t") audio\_port\_get\_size([audio\_port\_handle\_t](#_CPPv419audio_port_handle_t "audio_port_handle_t") port)

<a id="_CPPv426audio_port_get_filled_size19audio_port_handle_t"></a>

<a id="_CPPv326audio_port_get_filled_size19audio_port_handle_t"></a> <a id="_CPPv226audio_port_get_filled_size19audio_port_handle_t"></a> <a id="audio_port_get_filled_size__audio_port_handle_t"></a> <a id="audio__port_8h_1a0a650f5f5ba8c671de33ddcdd7941d3c"></a> [bk\_err\_t](../../../system/os.md#_CPPv48bk_err_t "bk_err_t") audio\_port\_get\_filled\_size([audio\_port\_handle\_t](#_CPPv419audio_port_handle_t "audio_port_handle_t") port)

<a id="_CPPv424audio_port_get_free_size19audio_port_handle_t"></a>

<a id="_CPPv324audio_port_get_free_size19audio_port_handle_t"></a> <a id="_CPPv224audio_port_get_free_size19audio_port_handle_t"></a> <a id="audio_port_get_free_size__audio_port_handle_t"></a> <a id="audio__port_8h_1a546ca0506656b76b21aa5b241b2ba009"></a> [bk\_err\_t](../../../system/os.md#_CPPv48bk_err_t "bk_err_t") audio\_port\_get\_free\_size([audio\_port\_handle\_t](#_CPPv419audio_port_handle_t "audio_port_handle_t") port)

<a id="_CPPv419audio_port_set_data19audio_port_handle_tPv"></a>

<a id="_CPPv319audio_port_set_data19audio_port_handle_tPv"></a> <a id="_CPPv219audio_port_set_data19audio_port_handle_tPv"></a> <a id="audio_port_set_data__audio_port_handle_t.voidP"></a> <a id="audio__port_8h_1a8179860c340b4e5bd7f2f8eb47dc5783"></a> [bk\_err\_t](../../../system/os.md#_CPPv48bk_err_t "bk_err_t") audio\_port\_set\_data([audio\_port\_handle\_t](#_CPPv419audio_port_handle_t "audio_port_handle_t") port, void \*data)

<a id="_CPPv419audio_port_get_data19audio_port_handle_t"></a>

<a id="_CPPv319audio_port_get_data19audio_port_handle_t"></a> <a id="_CPPv219audio_port_get_data19audio_port_handle_t"></a> <a id="audio_port_get_data__audio_port_handle_t"></a> <a id="audio__port_8h_1a7857b4a92f900dff452e9d8a6aa2bd86"></a> void \*audio\_port\_get\_data([audio\_port\_handle\_t](#_CPPv419audio_port_handle_t "audio_port_handle_t") port)

<a id="_CPPv419audio_port_set_type19audio_port_handle_t11port_type_t"></a>

<a id="_CPPv319audio_port_set_type19audio_port_handle_t11port_type_t"></a> <a id="_CPPv219audio_port_set_type19audio_port_handle_t11port_type_t"></a> <a id="audio_port_set_type__audio_port_handle_t.port_type_t"></a> <a id="audio__port_8h_1a1ef80b5e40e06d23d98fef265906a82f"></a> [bk\_err\_t](../../../system/os.md#_CPPv48bk_err_t "bk_err_t") audio\_port\_set\_type([audio\_port\_handle\_t](#_CPPv419audio_port_handle_t "audio_port_handle_t") port, [port\_type\_t](#_CPPv411port_type_t "port_type_t") type)

<a id="_CPPv419audio_port_get_type19audio_port_handle_t"></a>

<a id="_CPPv319audio_port_get_type19audio_port_handle_t"></a> <a id="_CPPv219audio_port_get_type19audio_port_handle_t"></a> <a id="audio_port_get_type__audio_port_handle_t"></a> <a id="audio__port_8h_1af17dbf15c43a8511a0bb8bda9393fddc"></a> [bk\_err\_t](../../../system/os.md#_CPPv48bk_err_t "bk_err_t") audio\_port\_get\_type([audio\_port\_handle\_t](#_CPPv419audio_port_handle_t "audio_port_handle_t") port)

<a id="structures"></a>

### Structures

<a id="_CPPv416audio_port_cfg_t"></a>

<a id="_CPPv316audio_port_cfg_t"></a> <a id="_CPPv216audio_port_cfg_t"></a> <a id="audio_port_cfg_t"></a> <a id="structaudio__port__cfg__t"></a> struct audio\_port\_cfg\_t
:   Audio Port configurations. Each Element at startup will be a self-running task. These tasks will execute the callback open -\> \[loop: read -\> write\] -\> close. These callback functions are provided by the user corresponding to this configuration.

    <a id="breathe-section-title-public-members"></a>

    Public Members

    <a id="_CPPv4N16audio_port_cfg_t4openE"></a>

    <a id="_CPPv3N16audio_port_cfg_t4openE"></a> <a id="_CPPv2N16audio_port_cfg_t4openE"></a> <a id="audio_port_cfg_t::open__port_io_func"></a> <a id="structaudio__port__cfg__t_1ad527bd911365df376106e27f394d746f"></a> [port\_io\_func](#_CPPv412port_io_func "port_io_func") open
    :   Open callback function

    <a id="_CPPv4N16audio_port_cfg_t5closeE"></a>

    <a id="_CPPv3N16audio_port_cfg_t5closeE"></a> <a id="_CPPv2N16audio_port_cfg_t5closeE"></a> <a id="audio_port_cfg_t::close__port_io_func"></a> <a id="structaudio__port__cfg__t_1aae6b0c6131cf4596bea66510a527b8d2"></a> [port\_io\_func](#_CPPv412port_io_func "port_io_func") close
    :   Close callback function

    <a id="_CPPv4N16audio_port_cfg_t7destroyE"></a>

    <a id="_CPPv3N16audio_port_cfg_t7destroyE"></a> <a id="_CPPv2N16audio_port_cfg_t7destroyE"></a> <a id="audio_port_cfg_t::destroy__port_io_func"></a> <a id="structaudio__port__cfg__t_1a4616e0456936c4c9a05bce235eed83d0"></a> [port\_io\_func](#_CPPv412port_io_func "port_io_func") destroy
    :   Destroy callback function

    <a id="_CPPv4N16audio_port_cfg_t5abortE"></a>

    <a id="_CPPv3N16audio_port_cfg_t5abortE"></a> <a id="_CPPv2N16audio_port_cfg_t5abortE"></a> <a id="audio_port_cfg_t::abort__port_io_func"></a> <a id="structaudio__port__cfg__t_1a3683bd8a9bc0399e6d5ff88fbd4b1aa6"></a> [port\_io\_func](#_CPPv412port_io_func "port_io_func") abort
    :   Abort callback function

    <a id="_CPPv4N16audio_port_cfg_t5resetE"></a>

    <a id="_CPPv3N16audio_port_cfg_t5resetE"></a> <a id="_CPPv2N16audio_port_cfg_t5resetE"></a> <a id="audio_port_cfg_t::reset__port_io_func"></a> <a id="structaudio__port__cfg__t_1a57519de503522132d9b7f51d66bb9f66"></a> [port\_io\_func](#_CPPv412port_io_func "port_io_func") reset
    :   Reset callback function

    <a id="_CPPv4N16audio_port_cfg_t4readE"></a>

    <a id="_CPPv3N16audio_port_cfg_t4readE"></a> <a id="_CPPv2N16audio_port_cfg_t4readE"></a> <a id="audio_port_cfg_t::read__port_stream_func"></a> <a id="structaudio__port__cfg__t_1a2166c9dec8ccca72e61937c8cfdb3d4a"></a> [port\_stream\_func](#_CPPv416port_stream_func "port_stream_func") read
    :   Read callback function

    <a id="_CPPv4N16audio_port_cfg_t5writeE"></a>

    <a id="_CPPv3N16audio_port_cfg_t5writeE"></a> <a id="_CPPv2N16audio_port_cfg_t5writeE"></a> <a id="audio_port_cfg_t::write__port_stream_func"></a> <a id="structaudio__port__cfg__t_1a4139a2be41dcc41e77d6ad2da6ab9222"></a> [port\_stream\_func](#_CPPv416port_stream_func "port_stream_func") write
    :   Write callback function

    <a id="_CPPv4N16audio_port_cfg_t10write_doneE"></a>

    <a id="_CPPv3N16audio_port_cfg_t10write_doneE"></a> <a id="_CPPv2N16audio_port_cfg_t10write_doneE"></a> <a id="audio_port_cfg_t::write_done__port_io_func"></a> <a id="structaudio__port__cfg__t_1a67250b90ed0a524884a505093e1a5ae2"></a> [port\_io\_func](#_CPPv412port_io_func "port_io_func") write\_done
    :   write done callback function

    <a id="_CPPv4N16audio_port_cfg_t8get_sizeE"></a>

    <a id="_CPPv3N16audio_port_cfg_t8get_sizeE"></a> <a id="_CPPv2N16audio_port_cfg_t8get_sizeE"></a> <a id="audio_port_cfg_t::get_size__port_io_func"></a> <a id="structaudio__port__cfg__t_1a1e2a932adfdab64da7d7bb501958ab5a"></a> [port\_io\_func](#_CPPv412port_io_func "port_io_func") get\_size
    :   Get ringbuffer size or frame buffer node number function

    <a id="_CPPv4N16audio_port_cfg_t15get_filled_sizeE"></a>

    <a id="_CPPv3N16audio_port_cfg_t15get_filled_sizeE"></a> <a id="_CPPv2N16audio_port_cfg_t15get_filled_sizeE"></a> <a id="audio_port_cfg_t::get_filled_size__port_io_func"></a> <a id="structaudio__port__cfg__t_1af61c2cda248366aa5b668df86636b01d"></a> [port\_io\_func](#_CPPv412port_io_func "port_io_func") get\_filled\_size
    :   Get ringbuffer filled size or ready frame buffer node number function

    <a id="_CPPv4N16audio_port_cfg_t13get_free_sizeE"></a>

    <a id="_CPPv3N16audio_port_cfg_t13get_free_sizeE"></a> <a id="_CPPv2N16audio_port_cfg_t13get_free_sizeE"></a> <a id="audio_port_cfg_t::get_free_size__port_io_func"></a> <a id="structaudio__port__cfg__t_1a08b2249dc0b42836a69cbb6a5add0e03"></a> [port\_io\_func](#_CPPv412port_io_func "port_io_func") get\_free\_size
    :   Get ringbuffer free size or free frame buffer node number function

    <a id="_CPPv4N16audio_port_cfg_t3tagE"></a>

    <a id="_CPPv3N16audio_port_cfg_t3tagE"></a> <a id="_CPPv2N16audio_port_cfg_t3tagE"></a> <a id="audio_port_cfg_t::tag__cP"></a> <a id="structaudio__port__cfg__t_1a7bc490ada1d22a42fa7ad712bf25bebd"></a> char \*tag
    :   Port tag

<a id="macros"></a>

### Macros

<a id="c.PORT_OK"></a>

<a id="audio__port_8h_1a3df3bb9d0f879f85045034f0403d9b62"></a> PORT\_OK

<a id="c.PORT_FAIL"></a>

<a id="audio__port_8h_1abdad060c13e60c44049f3185b8f1a810"></a> PORT\_FAIL

<a id="c.PORT_DONE"></a>

<a id="audio__port_8h_1acd29280aa43520de64791f7b388165aa"></a> PORT\_DONE

<a id="c.PORT_ABORT"></a>

<a id="audio__port_8h_1a4f6f895939b5238b3a684483b459c5e9"></a> PORT\_ABORT

<a id="c.PORT_TIMEOUT"></a>

<a id="audio__port_8h_1a473f3aa340eca6bb78b65e5d51546872"></a> PORT\_TIMEOUT

<a id="c.PORT_SIZE_OUT_RANGE"></a>

<a id="audio__port_8h_1af9b454da95a2cf410f87e66208137071"></a> PORT\_SIZE\_OUT\_RANGE

<a id="type-definitions"></a>

### Type Definitions

<a id="_CPPv419audio_port_handle_t"></a>

<a id="_CPPv319audio_port_handle_t"></a> <a id="_CPPv219audio_port_handle_t"></a> <a id="audio_port_handle_t"></a> <a id="audio__port_8h_1afb2176db05bf8a6238930a9b293c4766"></a> typedef struct audio\_port \*audio\_port\_handle\_t

<a id="_CPPv412port_io_func"></a>

<a id="_CPPv312port_io_func"></a> <a id="_CPPv212port_io_func"></a> <a id="port_io_func"></a> <a id="audio__port_8h_1a2b8a52418f25356f5ebe5960d134eb31"></a> typedef [bk\_err\_t](../../../system/os.md#_CPPv48bk_err_t "bk_err_t") (\*port\_io\_func)([audio\_port\_handle\_t](#_CPPv419audio_port_handle_t "audio_port_handle_t") self)

<a id="_CPPv416port_stream_func"></a>

<a id="_CPPv316port_stream_func"></a> <a id="_CPPv216port_stream_func"></a> <a id="port_stream_func"></a> <a id="audio__port_8h_1ab6399548d131b96f61dd0333e93b3701"></a> typedef int (\*port\_stream\_func)([audio\_port\_handle\_t](#_CPPv419audio_port_handle_t "audio_port_handle_t") self, char \*buffer, int len, TickType\_t ticks\_to\_wait, void \*context)

<a id="enumerations"></a>

### Enumerations

<a id="_CPPv411port_type_t"></a>

<a id="_CPPv311port_type_t"></a> <a id="_CPPv211port_type_t"></a> <a id="audio__port_8h_1aeb624a1369a8ea2bf2bf5fb7044af3e1"></a> enum port\_type\_t
:   *Values:*

    <a id="_CPPv4N11port_type_t12PORT_TYPE_RBE"></a>

    <a id="_CPPv3N11port_type_t12PORT_TYPE_RBE"></a> <a id="_CPPv2N11port_type_t12PORT_TYPE_RBE"></a> <a id="audio__port_8h_1aeb624a1369a8ea2bf2bf5fb7044af3e1ab40f1a4dd83b819463722a4af9383ada"></a> enumerator PORT\_TYPE\_RB

    <a id="_CPPv4N11port_type_t12PORT_TYPE_FBE"></a>

    <a id="_CPPv3N11port_type_t12PORT_TYPE_FBE"></a> <a id="_CPPv2N11port_type_t12PORT_TYPE_FBE"></a> <a id="audio__port_8h_1aeb624a1369a8ea2bf2bf5fb7044af3e1ac04d1e22c5bc34aed7ecaa757956f0a1"></a> enumerator PORT\_TYPE\_FB

    <a id="_CPPv4N11port_type_t12PORT_TYPE_CBE"></a>

    <a id="_CPPv3N11port_type_t12PORT_TYPE_CBE"></a> <a id="_CPPv2N11port_type_t12PORT_TYPE_CBE"></a> <a id="audio__port_8h_1aeb624a1369a8ea2bf2bf5fb7044af3e1a388c9ebbe6e31354df5a8c760efc6c56"></a> enumerator PORT\_TYPE\_CB

<a id="id1"></a>

### Header File

- [cb\_port.h](https://docs.bekencorp.com/arminodoc/bk_avdk_smp/ap_doc/bk7258/zh_CN/v3.1.1/_header_files/include/components/bk_audio/audio_pipeline/cb_port.h)

<a id="id2"></a>

### Functions

<a id="_CPPv418callback_port_initP19callback_port_cfg_t"></a>

<a id="_CPPv318callback_port_initP19callback_port_cfg_t"></a> <a id="_CPPv218callback_port_initP19callback_port_cfg_t"></a> <a id="callback_port_init__callback_port_cfg_tP"></a> <a id="cb__port_8h_1a922413a2daff1d6757f8ca4406fdb023"></a> [audio\_port\_handle\_t](#_CPPv419audio_port_handle_t "audio_port_handle_t") callback\_port\_init([callback\_port\_cfg\_t](#_CPPv419callback_port_cfg_t "callback_port_cfg_t") \*config)

<a id="id3"></a>

### Structures

<a id="_CPPv419callback_port_cfg_t"></a>

<a id="_CPPv319callback_port_cfg_t"></a> <a id="_CPPv219callback_port_cfg_t"></a> <a id="callback_port_cfg_t"></a> <a id="structcallback__port__cfg__t"></a> struct callback\_port\_cfg\_t

<a id="id4"></a>

### Macros

<a id="c.CALLBACK_PORT_CFG_DEFAULT"></a>

<a id="cb__port_8h_1ab43ecb835749e1be590417b34309ad82"></a> CALLBACK\_PORT\_CFG\_DEFAULT()

<a id="id5"></a>

### Header File

- [rb\_port.h](https://docs.bekencorp.com/arminodoc/bk_avdk_smp/ap_doc/bk7258/zh_CN/v3.1.1/_header_files/include/components/bk_audio/audio_pipeline/rb_port.h)

<a id="id6"></a>

### Functions

<a id="_CPPv417ringbuf_port_initP18ringbuf_port_cfg_t"></a>

<a id="_CPPv317ringbuf_port_initP18ringbuf_port_cfg_t"></a> <a id="_CPPv217ringbuf_port_initP18ringbuf_port_cfg_t"></a> <a id="ringbuf_port_init__ringbuf_port_cfg_tP"></a> <a id="rb__port_8h_1a87a6bab335b9f7de99d88fbd745a51a2"></a> [audio\_port\_handle\_t](#_CPPv419audio_port_handle_t "audio_port_handle_t") ringbuf\_port\_init([ringbuf\_port\_cfg\_t](#_CPPv418ringbuf_port_cfg_t "ringbuf_port_cfg_t") \*config)

<a id="id7"></a>

### Structures

<a id="_CPPv418ringbuf_port_cfg_t"></a>

<a id="_CPPv318ringbuf_port_cfg_t"></a> <a id="_CPPv218ringbuf_port_cfg_t"></a> <a id="ringbuf_port_cfg_t"></a> <a id="structringbuf__port__cfg__t"></a> struct ringbuf\_port\_cfg\_t

<a id="id8"></a>

### Macros

<a id="c.RINGBUF_PORT_RINGBUF_SIZE"></a>

<a id="rb__port_8h_1a4a9027133098210fb23fb4fad7af361d"></a> RINGBUF\_PORT\_RINGBUF\_SIZE

<a id="c.RINGBUF_PORT_CFG_DEFAULT"></a>

<a id="rb__port_8h_1a9d095bd9f732b564a56ca439e680aeae"></a> RINGBUF\_PORT\_CFG\_DEFAULT()

<a id="id9"></a>

### Header File

- [fb\_port.h](https://docs.bekencorp.com/arminodoc/bk_avdk_smp/ap_doc/bk7258/zh_CN/v3.1.1/_header_files/include/components/bk_audio/audio_pipeline/fb_port.h)

<a id="id10"></a>

### Functions

<a id="_CPPv418framebuf_port_initP19framebuf_port_cfg_t"></a>

<a id="_CPPv318framebuf_port_initP19framebuf_port_cfg_t"></a> <a id="_CPPv218framebuf_port_initP19framebuf_port_cfg_t"></a> <a id="framebuf_port_init__framebuf_port_cfg_tP"></a> <a id="fb__port_8h_1af75a305489a6cf4912f7430645028939"></a> [audio\_port\_handle\_t](#_CPPv419audio_port_handle_t "audio_port_handle_t") framebuf\_port\_init([framebuf\_port\_cfg\_t](#_CPPv419framebuf_port_cfg_t "framebuf_port_cfg_t") \*config)

<a id="id11"></a>

### Structures

<a id="_CPPv419framebuf_port_cfg_t"></a>

<a id="_CPPv319framebuf_port_cfg_t"></a> <a id="_CPPv219framebuf_port_cfg_t"></a> <a id="framebuf_port_cfg_t"></a> <a id="structframebuf__port__cfg__t"></a> struct framebuf\_port\_cfg\_t

<a id="id12"></a>

### Macros

<a id="c.FRAMEBUF_PORT_NODE_SIZE"></a>

<a id="fb__port_8h_1a9958c77bd703527e63e59852f8b2cab1"></a> FRAMEBUF\_PORT\_NODE\_SIZE

<a id="c.FRAMEBUF_PORT_NODE_NUM"></a>

<a id="fb__port_8h_1a38b705eaba79792fc2932f262eb3ca3c"></a> FRAMEBUF\_PORT\_NODE\_NUM

<a id="c.FRAMEBUF_PORT_CFG_DEFAULT"></a>

<a id="fb__port_8h_1ab021d4a4a0c9aad09d6cdc4f37b4daad"></a> FRAMEBUF\_PORT\_CFG\_DEFAULT()
