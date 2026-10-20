---
type: official-document
source_url: https://docs.bekencorp.com/arminodoc/bk_avdk_smp/ap_doc/bk7258/zh_CN/v3.1.1/api-reference/audio/audio_development_kit/audio_pipeline/audio_mem.html
sdk_family: bk_avdk_smp
chip: BK7258
processor: AP
sdk_version: v3.1.1
language: zh_CN
fetched_at: '2026-10-20T16:59:36.586772+00:00'
mirror_status: current
---

<a id="audio-memory"></a>

# Audio Memory

Audio Memory is used to handle audio memory.

<a id="api-reference"></a>

## API Reference

<a id="header-file"></a>

### Header File

- [audio\_mem.h](https://docs.bekencorp.com/arminodoc/bk_avdk_smp/ap_doc/bk7258/zh_CN/v3.1.1/_header_files/include/components/bk_audio/audio_pipeline/audio_mem.h)

<a id="functions"></a>

### Functions

<a id="_CPPv412audio_malloc8uint32_t"></a>

<a id="_CPPv312audio_malloc8uint32_t"></a> <a id="_CPPv212audio_malloc8uint32_t"></a> <a id="audio_malloc__uint32_t"></a> <a id="audio__mem_8h_1abd2f47fa0da92ea3e0a503b1304a6d4c"></a> void \*audio\_malloc(uint32\_t size)
:   Malloc memory.

    参数
    :   **size** – **\[in\]** memory size

    返回
    :   - valid pointer on success
        - NULL when any errors

<a id="_CPPv410audio_freePv"></a>

<a id="_CPPv310audio_freePv"></a> <a id="_CPPv210audio_freePv"></a> <a id="audio_free__voidP"></a> <a id="audio__mem_8h_1a08b7ffec44019a6adc3db6f8174c276f"></a> void audio\_free(void \*ptr)
:   Free memory.

    参数
    :   **ptr** – **\[in\]** memory pointer

    返回
    :   - void

<a id="_CPPv412audio_calloc8uint32_t8uint32_t"></a>

<a id="_CPPv312audio_calloc8uint32_t8uint32_t"></a> <a id="_CPPv212audio_calloc8uint32_t8uint32_t"></a> <a id="audio_calloc__uint32_t.uint32_t"></a> <a id="audio__mem_8h_1ac81b922b67163fce600bf594c6b42c66"></a> void \*audio\_calloc(uint32\_t nmemb, uint32\_t size)
:   Malloc memory.

    参数
    :   - **nmemb** – **\[in\]** number of block
        - **size** – **\[in\]** block memory size

    返回
    :   - valid pointer on success
        - NULL when any errors

<a id="_CPPv415audio_mem_printPciPKc"></a>

<a id="_CPPv315audio_mem_printPciPKc"></a> <a id="_CPPv215audio_mem_printPciPKc"></a> <a id="audio_mem_print__cP.i.cCP"></a> <a id="audio__mem_8h_1a71b3d341b63b4a20e88398eec1a58f36"></a> void audio\_mem\_print(char \*tag, int line, const char \*func)
:   Print heap memory status.

    参数
    :   - **tag** – **\[in\]** tag of log
        - **line** – **\[in\]** line of log
        - **func** – **\[in\]** function name of log

    返回
    :   - void

<a id="_CPPv412audio_strdupPKc"></a>

<a id="_CPPv312audio_strdupPKc"></a> <a id="_CPPv212audio_strdupPKc"></a> <a id="audio_strdup__cCP"></a> <a id="audio__mem_8h_1a721402953926000d512a1a18511dcbed"></a> char \*audio\_strdup(const char \*str)
:   Duplicate given string.

    ```
         Allocate new memory, copy contents of given string into it and return the pointer
    ```

    参数
    :   **str** – **\[in\]** String to be duplicated

    返回
    :   - Pointer to new malloc’ed string
        - NULL otherwise

<a id="_CPPv418audio_dma_mem_freePv"></a>

<a id="_CPPv318audio_dma_mem_freePv"></a> <a id="_CPPv218audio_dma_mem_freePv"></a> <a id="audio_dma_mem_free__voidP"></a> <a id="audio__mem_8h_1a453b171f84c8b2eac70d800dc05e179c"></a> void audio\_dma\_mem\_free(void \*ptr)
:   Free memory used by dma.

    参数
    :   **ptr** – **\[in\]** memory pointer

    返回
    :   - void

<a id="_CPPv420audio_dma_mem_calloc8uint32_t8uint32_t"></a>

<a id="_CPPv320audio_dma_mem_calloc8uint32_t8uint32_t"></a> <a id="_CPPv220audio_dma_mem_calloc8uint32_t8uint32_t"></a> <a id="audio_dma_mem_calloc__uint32_t.uint32_t"></a> <a id="audio__mem_8h_1ac03a65e010c878d89aca53ea43617487"></a> void \*audio\_dma\_mem\_calloc(uint32\_t nmemb, uint32\_t size)
:   Malloc memory used by dma.

    参数
    :   - **nmemb** – **\[in\]** number of block
        - **size** – **\[in\]** block memory size

    返回
    :   - valid pointer on success
        - NULL when any errors

<a id="macros"></a>

### Macros

<a id="c.AUDIO_MEM_SHOW"></a>

<a id="audio__mem_8h_1ad951ff516b47f646c8339ccaa8a6f9b6"></a> AUDIO\_MEM\_SHOW(x)
