# API

## exposed variable and function

### variable

```c
 typedef enum
 {
     EJ_NOT_SUBSCRIBED      = -13,
     EJ_ALREADY_SUBSCRIBED  = -12,
     EJ_TIMEOUT             = -11,
     EF_UNSUBSCRIPTION_ERROR= -10,
     EJ_SUBSCRIPTION_ERROR  = -9,
     EJ_PUBLISH_ERROR       = -8,
     EJ_NOT_CONNECTED       = -7,
     EJ_CONNECTION_FAILED   = -6,
     EJ_BAD_URL             = -5,
     EJ_CERT_REQUIRED_ERROR = -4,
     EJ_MEMORY_ERROR        = -3,
     EJ_BAD_ARGS            = -2,
     EJ_FAILURE             = -1,
     EJ_SUCCESS             =  0,
 } ej_ret_t;

```

```c
typedef int (*ej_callback_t)(void);
```

```c
typedef struct ej_ctx_t* ej_handle_t;
```

```c
typedef enum {
    EJ_SWIFT_CONNECTION_EVENT_SEARCH_INFO,
    EJ_SWIFT_CONNECTION_EVENT_LOCKING_CH,
    EJ_SWIFT_CONNECTION_EVENT_LOCKED_CH,
    EJ_SWIFT_CONNECTION_EVENT_TIMEOUT,
    EJ_SWIFT_CONNECTION_EVENT_DONE
} ej_swift_connection_event_t;
```

```c
typedef enum {
    EJ_SWIFT_CONNECTION_STATUS_FAIL = -1,
    EJ_SWIFT_CONNECTION_STATUS_OK
} ej_swift_connection_status_t
```

```c
typedef void(* ej_swift_connection_callback_t) (ej_swift_connection_event_t event, void *data);
```

### cloud API

```c
ej_ret_t ej_init_handle(ej_handle_t *handle);
```

```c
ej_ret_t ej_detroy_handle(ej_handle_t *handle);
```

```c
ej_ret_t ej_set_channel(uint8_t *mac);
```

```c
ej_ret_t ej_set_connect_callback(ej_callback_t lost_connect_callback, ej_callback_t restore_connect_callback);
```

```c
ej_ret_t ej_set_thread_priority(int priority);
```

```c
ej_ret_t ej_set_thread_stacksize(ej_handle_t *handle, int size);
```

```c
ej_ret_t ej_set_wifi_version_info(wifi_version_info_t *info);
```

```c
ej_ret_t ej_set_ota_callback(wifi_ota_callback_t wifi_ota_cb, dev_ota_callback_t dev_ota_cb);
```

```c
ej_ret_t ej_connect(ej_handle_t *handler);
```

```c
uint8_t ej_set_incoming_msg_cb(wifi_ota_callback_t wifi_ota_cb);
```

```c
ej_ret_t ej_disconnect(ej_handle_t *handler);
```

```c
uint8_t ej_put_msg(void *msg, uint16_t length);
```




### uart communication


### log 

```c
TODO:
set_sdk_log_level()

ej_printf(modue, ...);

```


### smart config


```c
ej_swift_connection_status_t ej_swift_connection_init(const uint8_t *key, const uint8_t key_length, ej_swift_conn_callback cb);
```

```c
ej_swift_connection_status_t ej_swift_connection_start(uint32_t timeout);
```

```c
ej_swift_connection_status_t ej_swift_connection_stop(void);
```

## internal function (platform)

### timer

#### timer of mqtt

```c
void timer_init(Timer *timer);
```

```c
char time_is_expired(Timer *timer);
```

```c
void time_countdown(Timer* timer, unsigned int timeout);
```

```c
int time_left(Timer *timer);
```

#### timer of thread level

```c
int timer_create(timer_t *timer, const char *name, timer_tick ticks, void (*call_back)(ej_timer_arg_t), void *cb_arg, timer_reload_t reload, timer_activate_t activate);
```

```c
int timer_activate(timer_t *timer);
```

```c
int timer_deactivate(timer_t *timer);
```

```c
int timer_change(timer_t *timer, timer_tick ntime, timer_tick block_time);
```

```c
int timer_reset(timer_t *timer);
```

```c
int time_delete(timer_t *timer);
```

### network

#### tcp

```c
void network_init(Network *n);
```

```c
void network_securedinit(Network *n, const char* ca_buf, size_t ca_size);
```

```c
int network_connect(Network *n, char *addr, int port);
```

```c
void network_disconnect(Network *n);
```

```c
int network_write(Network *n, unsigned char *buf, int len, int timeout_ms);
```

```c
int network_read(Network *n, unsigned char *buf, int len, int timeout_ms);
```

#### udp

```c
void network_udp_init(Network *n);
```

```c
int network_udp_bind(Network *n);
```

```c
int network_udp_write(Network *n, unsigned char *buf, int len);
```

```c
int network_udp_read(Network *n, unsigned char *buf, int len);
```

```c
void network_udp_close(Network *n);
```

### mutex

```c
void mutex_init(Mutex *mutex);
```

```c
int mutex_lock(Mutex *mutex);
```

```c
int mutex_unlock(Mutex *mutex);
```

```c
void mutex_deinit(Mutex *mutex);
```

### semaphore

```c
void semaphore_int(Semaphore *semaphore);
```

```c
void semaphore_deinit(Semaphore *semaphore);
```

```c
int semaphore_wait(Semaphore *semaphore, int timeout);
```

```c
int semaphore_post(Semaphore *semaphore);
```

### queue

```c
int queue_create(queue_t *qhandle, const char *name, int msgsize, queue_pool_t *poolname);
```

```c
int queue_send(queue_t *qhandle, const void *msg, unsigned long wait);
```

```c
int queue_recv(queue_t *qhandle, void *msg, unsigned long wait);
```

```c
int queue_delete(queue_t *qhandle);
```

### thread

```c
int thread_create(thread_t *thread, init priority, const char *name, void (*founc)(void *), int stack_size, void *arg);
```

```c
int thread_join(thread_t *thread, int timeout);
```

```c
int thread_destroy(thread_t *thread);
```

### sleep

```c
int sleep(int ms);
```

### memory

```c
void *plat_malloc(int size);
```

```c
void plat_free(void *mem); 
```

### uart

```c
int uart_open(UART_ID uart_id, uint32_t baudrate)
```

```c
void uart_close(UART_ID uart_id);
```

```c
int16_t uart_read(const uint8_t *buf, uint32_t len);
```

```c
int16_t uart_write(uint8_t *buf, uint32_t len);
```

### printf

```c
int plat_printf(const char *fmt, ...);
```
