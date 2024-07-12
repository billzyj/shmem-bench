# shmem-bench
This intent of this benchmarking suite is to test the functions defined
in the OpenSHMEM spec (currently 1.5) for speed and scalability. What this benchmark
does not do is test correctness or reliability, which could be found at https://github.com/michael-beebe/shmemvv.

### OpenSHMEM Library API
- [Library Setup, Exit, and Query Routines](#library-setup-exit-and-query-routines)
- [Thread Support](#thread-support)
- [Memory Management Routines](#memory-management-routines)
- [Team Management Routines](#team-management-routines)
- [Communication/Context Management Routines](#communicationcontext-management-routines)
- [Remote Memory Access Routines](#remote-memory-access-routines)
- [Atomic Memory Operations](#atomic-memory-operations)
- [Signaling Operations](#signaling-operations)
- [Collective Routines](#collective-routines)
- [Point-Point Synchronization Routines](#point-point-synchronization-routines)
- [Memory Ordering Routines](#memory-ordering-routines)
- [Distributed Locking Routines](#distributed-locking-routines)

#### Library Setup, Exit, and Query Routines
```
--test_setup
```
Will ONLY test the following routines:
- shmem_init()
- shmem_my_pe()
- shmem_n_pes()
- shmem_finalize()
- shmem_global_exit()
- shmem_pe_accessible()
- shmem_addr_accessible()
- shmem_ptr()
- shmem_info_get_version()
- shmem_info_get_name()

#### Thread Support
```
--test_threads
```
Will test the following routines:
- shmem_init_thread()
- shmem_query_thread()

#### Memory Management Routines
```
--test_mem
```
Will test the following routines:
- shmem_malloc()
- shmem_free()
- shmem_realloc()
- shmem_align()
- shmem_malloc_with_hints()
- shmem_calloc()

#### Team Managment Routines
```
--test_teams
```
Will test the following routines:
- shmem_team_my_pe()
- shmem_team_n_pes()
- shmem_team_get_config() (shmem_team_config_t )
- shmem_team_translate_pe()
- shmem_team_split_strided()
- shmem_team_split_2d()
- shmem_team_destroy()

#### Communication/Context Management Routines
```
--test_comms
```
Will test the following routines:
- shmem_ctx_create()
- shmem_team_create_ctx()
- shmem_ctx_destroy()
- shmem_ctx_get_team()

#### Remote Memory Access Routines
```
--test_remote
```
Will test the following routines:

##### Standard RMA Types and Names

| TYPE                  | TYPENAME   |
|-----------------------|------------|
| float                 | float      |
| double                | double     |
| long double           | longdouble |
| char                  | char       |
| signed char           | schar      |
| short                 | short      |
| int                   | int        |
| long                  | long       |
| long long             | longlong   |
| unsigned char         | uchar      |
| unsigned short        | ushort     |
| unsigned int          | uint       |
| unsigned long         | ulong      |
| unsigned long long    | ulonglong  |
| int8_t                | int8       |
| int16_t               | int16      |
| int32_t               | int32      |
| int64_t               | int64      |
| uint8_t               | uint8      |
| uint16_t              | uint16     |
| uint32_t              | uint32     |
| uint64_t              | uint64     |
| size_t                | size       |
| ptrdiff_t             | ptrdiff    |

##### Blocking RMA Routines
- shmem_put()
    - shmem_TYPENAME_put()
    - shmem_ctx_TYPENAME_put()
    - shmem_putSIZE()
    - shmem_ctx_putSIZE()
- shmem_p()
- shmem_iput()
- shmem_get()
- shmem_g()
- shmem_iget()

##### Nonblocking RMA Routines
- shmem_put_nbi()
- shmem_get_nbi()

where TYPE is one of the standard RMA types and has a corresponding TYPENAME specified by Table 

where SIZE is one of 8, 16, 32, 64, 128.

#### Atomic Memory Operations
```
--test_atomics
```
Will test the following routines:

##### Table: Standard AMO Types and Names

| TYPE                  | TYPENAME   |
|-----------------------|------------|
| int                   | int        |
| long                  | long       |
| long long             | longlong   |
| unsigned int          | uint       |
| unsigned long         | ulong      |
| unsigned long long    | ulonglong  |
| int32_t               | int32      |
| int64_t               | int64      |
| uint32_t              | uint32     |
| uint64_t              | uint64     |
| size_t                | size       |
| ptrdiff_t             | ptrdiff    |

##### Table: Extended AMO Types and Names

| TYPE                  | TYPENAME   |
|-----------------------|------------|
| float                 | float      |
| double                | double     |
| int                   | int        |
| long                  | long       |
| long long             | longlong   |
| unsigned int          | uint       |
| unsigned long         | ulong      |
| unsigned long long    | ulonglong  |
| int32_t               | int32      |
| int64_t               | int64      |
| uint32_t              | uint32     |
| uint64_t              | uint64     |
| size_t                | size       |
| ptrdiff_t             | ptrdiff    |

##### Table: Bitwise AMO Types and Names

| TYPE                  | TYPENAME   |
|-----------------------|------------|
| unsigned int          | uint       |
| unsigned long         | ulong      |
| unsigned long long    | ulonglong  |
| int32_t               | int32      |
| int64_t               | int64      |
| uint32_t              | uint32     |
| uint64_t              | uint64     |


#### Blocking
- shmem_atomic_fetch()
- shmem_atomic_set()
- shmem_atomic_compare_swap()
- shmem_atomic_swap
- shmem_atomic_fetch_inc()
- shmem_atomic_inc()
- shmem_atomic_fetch_add()
- shmem_atomic_add()
- shmem_atomic_fetch_and()
- shmem_atomic_and()
- shmem_atomic_fetch_or()
- shmem_atomic_or()
- shmem_atomic_fetch_xor()
- shmem_atomic_xor()

#### Nonblocking
- shmem_atomic_fetch_nbi()
- shmem_atomic_compare_swap_nbi()
- shmem_atomic_swap_nbi()
- shmem_atomic_fetch_inc_nbi()
- shmem_atomic_fetch_add_nbi()
- shmem_atomic_fetch_and_nbi()
- shmem_atomic_fetch_or_nbi()
- shmem_atomic_fetch_xor_nbi()

#### Signaling Operations
```
--test_signaling
```
Will test the following routines:
- shmem_put_signal()
- shmem_put_signal_nbi()
- shmem_signal_fetch()

#### Collective Routines
```
--test_collectives
```
Will test the following routines:
- shmem_barrier_all()
- shmem_barrier()
- shmem_sync()
- shmem_sync_all()
- shmem_alltoall()
- shmem_alltoalls()
- shmem_broadcast()
- shmem_collect()
- shmem_fcollect()
- shmem_and_reduce()
- shmem_or_reduce()
- shmem_xor_reduce()
- shmem_max_reduce()
- shmem_min_reduce()
- shmem_sum_reduce()
- shmem_prod_reduce()

#### Point-Point Synchronization Routines
```
--test_pt2pt_synch
```
Will test the following routines:
- shmem_wait_until()
- shmem_wait_until_all()
- shmem_wait_until_any()
- shmem_wait_until_some()
- shmem_wait_until_all_vector()
- shmem_wait_until_any_vector()
- shmem_wait_until_some_vector()
- shmem_test()
- shmem_test_all()
- shmem_test_any()
- shmem_test_some()
- shmem_test_all_vector()
- shmem_test_any_vector()
- shmem_test_some_vector()
- shmem_signal_wait_until()

#### Memory Ordering Routines
```
--test_mem_ordering
```
Will test the following routines:
- shmem_fence()
- shmem_quiet()

#### Distributed Locking Routines
```
--test_locking
```
Will test the following routines:
- shmem_set_lock()
- shmem_clear_unlock()

#### All tests
```
--all
```
Will run all the tests