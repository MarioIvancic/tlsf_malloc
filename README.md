# TLSF malloc

This is implementation on malloc/calloc/realloc/free based on Two Level Segregated Fit memory allocator written by Matthew Conte. For original documentation see Readme.txt or http://tlsf.baisoku.org

### Implemented functions

Implemented are standard C functions for memory management:
```
void malloc_init(void* ptr, size_t size); /* optional */
void* malloc (size_t size);
void* calloc (size_t nmemb, size_t size);
void* realloc (void* ptr, size_t size);
void free (void* ptr);
```

Note that `malloc_init()` is used to define memory block managed by TLSF malloc, and it should be called before any other functions from this library. But it is optional, and if it is not called explicitly it will be called implicitly by malloc/calloc on the first call to malloc/calloc.

### Compile time options

| Option | Description |
|----------------------------------------|------------------------------------------------------|
| TLSF_MALLOC_MEMSIZE | Size of the heap memory block to be used by TLSF allocator. Default is (_stack - _heap) / 2. |
| TLSF_MALLOC_FL_INDEX_BITS | Number of bits used for addressing memory. Default is 15 which is good for 32kB of memory. Note that 2^TLSF_MALLOC_FL_INDEX_BITS >= TLSF_MALLOC_MEMSIZE |
| TLSF_MALLOC_SL_INDEX_BITS | How many bits is used to calculate subdivisions between 2^n and 2^(n+1). Default is 2. Higher values will give lower memory trashing but higher internal memory usage. |

### Dependencies

This implementation depends on several functions and symbols:

-	memset function from libc (used in calloc). 
-	_heap symbol, if malloc_init() is not explicitly called by the user.
-	_heap and _stack symbols, if TLSF_MALLOC_MEMSIZE macro is not defined.

