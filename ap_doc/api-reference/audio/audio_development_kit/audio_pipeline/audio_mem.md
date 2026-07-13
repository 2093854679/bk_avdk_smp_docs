# Audio Memory


Audio Memory is used to handle audio memory.


## API Reference


### Header File


- [bk_audio/audio_pipeline/audio_mem.h](http://192.168.0.46/gerrit/plugins/gitiles/iot/wcn/projects/+/refs/heads/armino_main/components/bk_audio/audio_pipeline/audio_mem.h "http://192.168.0.46/gerrit/plugins/gitiles/iot/wcn/projects/+/refs/heads/armino_main/components/bk_audio/audio_pipeline/audio_mem.h")


### Functions

void *audio_malloc(uint32_t size)
:   Malloc memory.

    参数
    :   **size** – **[in]** memory size

    返回
    :   - valid pointer on success

        - NULL when any errors

void audio_free(void *ptr)
:   Free memory.

    参数
    :   **ptr** – **[in]** memory pointer

    返回
    :   - void

void *audio_hsram_malloc(uint32_t size)
:   Malloc memory from HSRAM.

    参数
    :   **size** – **[in]** memory size

    返回
    :   - valid pointer on success

        - NULL when any errors

void audio_hsram_free(void *ptr)
:   Free memory allocated from HSRAM.

    参数
    :   **ptr** – **[in]** memory pointer

    返回
    :   - void

void *audio_calloc(uint32_t nmemb, uint32_t size)
:   Malloc memory.

    参数
    :   - **nmemb** – **[in]** number of block

        - **size** – **[in]** block memory size

    返回
    :   - valid pointer on success

        - NULL when any errors

void audio_mem_print(char *tag, int line, const char *func)
:   Print heap memory status.

    参数
    :   - **tag** – **[in]** tag of log

        - **line** – **[in]** line of log

        - **func** – **[in]** function name of log

    返回
    :   - void

char *audio_strdup(const char *str)
:   Duplicate given string.

    ```
         Allocate new memory, copy contents of given string into it and return the pointer
    ```

    参数
    :   **str** – **[in]** String to be duplicated

    返回
    :   - Pointer to new malloc’ed string

        - NULL otherwise

void audio_dma_mem_free(void *ptr)
:   Free memory used by dma.

    参数
    :   **ptr** – **[in]** memory pointer

    返回
    :   - void

void *audio_dma_mem_calloc(uint32_t nmemb, uint32_t size)
:   Malloc memory used by dma.

    参数
    :   - **nmemb** – **[in]** number of block

        - **size** – **[in]** block memory size

    返回
    :   - valid pointer on success

        - NULL when any errors


### Macros

AUDIO_MEM_SHOW(x)
