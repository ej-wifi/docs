# API

## exposed variable and function

### variable

```
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

```
typedef int (*ej_callback_t)(void);
```

```
typedef struct ej_ctx_t* ej_handle_t;
```

### cloud API

```
ej_ret_t ej_init_handle(ej_handle_t *handle);
```

```
ej_ret_t ej_detroy_handle(ej_handle_t *handle);
```

```
ej_ret_t ej_set_channel(uint8_t *mac);
```

```
ej_ret_t ej_set_connect_callback(ej_callback_t lost_connect_callback, ej_callback_t restore_connect_callback);
```

```
ej_ret_t ej_set_thread_priority(int priority);
```

```
ej_ret_t ej_set_thread_stacksize(ej_handle_t *handle, int size);
```

```
ej_ret_t ej_connect(ej_handle_t *handler);
```

```
ej_ret_t ej_disconnect(ej_handle_t *handler);
```

```
ej_ret_t ej_set_network_staus(int status)
```

### uart communication


### log 

```
TODO:
set_sdk_log_level()

ej_printf(modue, ...);

```

### OTA

```
TODO:
WIFI and machine OTA
```

### smart config



```
TODO:
```

## internal function (platform)

### timer

#### timer of mqtt

```
void timer_init(Timer *timer);
```

```
char time_is_expired(Timer *timer);
```

```
void time_countdown(Timer* timer, unsigned int timeout);
```

```
int time_left(Timer *timer);
```

#### timer of thread level

```
int timer_create(timer_t *timer, const char *name, timer_tick ticks, void (*call_back)(ej_timer_arg_t), void *cb_arg, timer_reload_t reload, timer_activate_t activate);
```

```
int timer_activate(timer_t *timer);
```

```
int timer_deactivate(timer_t *timer);
```

```
int timer_change(timer_t *timer, timer_tick ntime, timer_tick block_time);
```

```
int timer_reset(timer_t *timer);
```

```
int time_delete(timer_t *timer);
```

### network

#### tcp

```
void network_init(Network *n);
```

```
void network_securedinit(Network *n, const char* ca_buf, size_t ca_size);
```

```
int network_connect(Network *n, char *addr, int port);
```

```
void network_disconnect(Network *n);
```

```
int network_write(Network *n, unsigned char *buf, int len, int timeout_ms);
```

```
int network_read(Network *n, unsigned char *buf, int len, int timeout_ms);
```

#### udp

```
void network_udp_init(Network *n);
```

```
int network_udp_bind(Network *n);
```

```
int network_udp_write(Network *n, unsigned char *buf, int len);
```

```
int network_udp_read(Network *n, unsigned char *buf, int len);
```

```
void network_udp_close(Network *n);
```

### mutex

```
void mutex_init(Mutex *mutex);
```

```
int mutex_lock(Mutex *mutex);
```

```
int mutex_unlock(Mutex *mutex);
```

```
void mutex_deinit(Mutex *mutex);
```

### semaphore

```
void semaphore_int(Semaphore *semaphore);
```

```
void semaphore_deinit(Semaphore *semaphore);
```

```
int semaphore_wait(Semaphore *semaphore, int timeout);
```

```
int semaphore_post(Semaphore *semaphore);
```

### queue

```
int queue_create(queue_t *qhandle, const char *name, int msgsize, queue_pool_t *poolname);
```

```
int queue_send(queue_t *qhandle, const void *msg, unsigned long wait);
```

```
int queue_recv(queue_t *qhandle, void *msg, unsigned long wait);
```

```
int queue_delete(queue_t *qhandle);
```

### thread

```
int thread_create(thread_t *thread, init priority, const char *name, void (*founc)(void *), int stack_size, void *arg);
```

```
int thread_join(thread_t *thread, int timeout);
```

```
int thread_destroy(thread_t *thread);
```

### sleep

```
int sleep(int ms);
```

### memory

```
void *plat_malloc(int size);
```

```
void plat_free(void *mem); 
```

### uart

```
int uart_open(UART_ID uart_id, uint32_t baudrate)
```

```
void uart_close(UART_ID uart_id);
```

```
int16_t uart_read(const uint8_t *buf, uint32_t len);
```

```
int16_t uart_write(uint8_t *buf, uint32_t len);
```

### printf

```
int plat_printf(const char *fmt, ...);
```
