---
title: "kmem_cache 정리"
last_modified_at: 2025-09-21T00:00:00-09:00
categories:
- Linux
- Kernel
excerpt: "kmem cache를 생성하는 방법에 대해서 상세히 정리"
---

## 0. 전체 요약

- `kmem_cache_create()`는 **고정 크기 커널 오브젝트를 위한 전용 슬랩 캐시를 생성하는 함수**다.
    
- 인자별 핵심:
    
    - `name` : 캐시 이름, 디버깅/모니터링용 식별자.
        
    - `size` : 오브젝트 1개 크기 (`sizeof(struct foo)`).
        
    - `align` : 오브젝트 시작 **주소 alignment**. 보통 `0`으로 두고 커널에 위임.
        
    - `flags` : 슬랩 동작 및 디버깅 플래그 (`SLAB_HWCACHE_ALIGN` 등).
        
    - `ctor` : 새 오브젝트가 처음 만들어질 때 한 번만 호출되는 constructor.
        
- `align`은 **구조체 내부 필드 정렬이 아니라, 슬랩에서 나오는 오브젝트 주소를 몇 바이트 경계에 맞출지 지정하는 값**이다.
    
- 캐시라인 정렬이 필요할 때는 `align` 값을 직접 주기보다는, 일반적으로  
    `align = 0` + `flags`에 `SLAB_HWCACHE_ALIGN`를 사용하는 패턴을 많이 쓴다.
    
- 슬랩 캐시에서 메모리를 쓸 때는:
    
    - `kmem_cache_alloc()` / `kmem_cache_zalloc()`으로 할당,
        
    - `kmem_cache_free()`로 해제,
        
    - 모듈 종료 시점 등에는 `kmem_cache_destroy()`로 **캐시 자체를 파괴**한다.
        

---

## 1. 개요

`kmem_cache_create()`는 커널 SLAB/SLUB allocator에서 **특정 크기의 오브젝트들을 위한 전용 캐시(slab cache)** 를 만드는 함수다.  
이 캐시를 만들어 두면, 같은 크기의 구조체를 반복적으로 `kmem_cache_alloc()` / `kmem_cache_free()`로 빠르게 할당/해제할 수 있다.

---

## 2. 함수 시그니처

일반적인 최신 커널 기준 시그니처는 다음과 같다:

```c
struct kmem_cache *kmem_cache_create(const char *name,
				     unsigned int size,
				     unsigned int align,
				     slab_flags_t flags,
				     void (*ctor)(void *));
```

---

## 3. 인자별 설명

### 3.1 `const char *name`

- 슬랩 캐시의 이름이다.
    
- `/proc/slabinfo` 등에 노출돼서 디버깅이나 모니터링할 때 어떤 캐시인지 식별하는 용도로 사용된다.
    
- 예: `"my_inode_cache"`, `"task_struct"` 등.
    

### 3.2 `unsigned int size`

- **캐시가 관리할 오브젝트 1개의 크기(바이트 단위)** 이다.
    
- `kmem_cache_alloc(cache, ...)`로 할당받는 객체의 크기가 이 값에 해당한다.
    
- 보통 이렇게 넘긴다:
    

```c
size = sizeof(struct my_obj);
```

### 3.3 `unsigned int align`

- 이 캐시에서 할당되는 **오브젝트 시작 주소의 alignment(정렬 단위)** 를 의미한다.
    
- 즉, “이 객체 주소가 몇 바이트 배수에 맞춰지게 할 것인지”를 정하는 값이다.
    
    - 예: `align = 64` → 오브젝트 시작 주소가 항상 64바이트 배수.
        
- 특별한 요구사항이 없으면 보통 `0`을 줘서 커널이 적당히 맞추게 둔다.
    
- 캐시라인 정렬이 필요하면 직접 숫자를 쓰기보다는 보통 `SLAB_HWCACHE_ALIGN` 플래그를 사용하는 패턴을 많이 쓴다.
    

정리하면,

> **align은 오브젝트가 놓이는 주소(address)의 alignment를 지정하는 인자**다.  
> 구조체 내부 특정 필드의 정렬이 아니라, “할당된 chunk 자체의 시작 주소”를 어떻게 정렬할지에 대한 설정이라고 보면 된다.

### 3.4 `slab_flags_t flags`

- 슬랩 캐시의 동작/디버깅 옵션을 제어하는 플래그들을 OR 해서 넘긴다.
    
- 자주 보는 플래그 예시:
    
    - `SLAB_HWCACHE_ALIGN`
        
        - 오브젝트를 CPU 캐시라인 경계에 정렬해서 캐시 효율을 올리려는 목적.
            
    - `SLAB_POISON`
        
        - 할당/해제 시 알려진 패턴으로 메모리를 채워서 use-after-free, 초기화 안 된 메모리 사용 같은 버그를 잡는 데 도움.
            
    - `SLAB_RED_ZONE`
        
        - 오브젝트 앞/뒤에 red zone을 둬서 버퍼 오버런 잡는 디버깅용.
            
- 커널 config에서 슬랩 디버깅 옵션을 켜면 이 플래그들이 자동으로 켜지는 경우도 있다.
    

### 3.5 `void (*ctor)(void *)`

- 슬랩 오브젝트 **constructor 콜백**이다.
    
- “새로운 페이지가 캐시에 추가되면서 새 오브젝트들이 처음 생성될 때” 한 번씩 호출되는 초기화 함수라고 보면 된다.
    
- 프로토타입:
    

```c
void my_ctor(void *obj);
```

- 주 사용처:
    
    - 구조체 안의 `spinlock_t`, `struct list_head` 같은 걸 **항상 초기 상태로 맞춰두고 싶을 때**.
        
    - 즉, “이 캐시에서 나오는 객체라면 기본적으로 이런 초기 상태를 가져야 한다”를 맞춰두는 용도.
        
- 포인트:
    
    - **매 alloc/free 때마다 도는 게 아니라**, 새로 준비된 오브젝트에 대해 한 번만 호출된다는 점을 주의해야 한다.
        
    - 실제 로직에서 요청마다 바뀌는 값(예: `id`, `data` 필드 등)은 보통 alloc 직후 코드에서 직접 채운다.
        

---

## 4. `align` 인자 상세

조금 더 `align`만 따로 정리하면:

1. **정의**
    
    - `align`은 슬랩 캐시에서 할당되는 **각 오브젝트의 시작 주소가 맞춰질 최소 정렬 단위**이다.
        
    - 즉, `align`은 곧 **address alignment 요구 사항**을 의미한다.
        
2. **align 값 선택 기준**
    
    - `0`
        
        - 커널이 오브젝트 크기와 타입에 따라 적당한 alignment를 잡아준다.
            
        - 가장 흔한 사용 방식.
            
    - N(예: 8, 16, 32, 64 등)
        
        - 특정 하드웨어 요구사항, DMA, SIMD, cacheline 등의 이유로 특정 경계에 맞춰야 할 때 사용.
            
3. **`SLAB_HWCACHE_ALIGN`와의 관계**
    
    - 캐시라인 정렬을 하고 싶을 때는 보통 `align`에 직접 캐시라인 크기를 넣기보다는,
        
        - `align = 0`으로 두고
            
        - `flags`에 `SLAB_HWCACHE_ALIGN`을 주는 식으로 많이 쓴다.
            
    - 예:
        

```c
cache = kmem_cache_create("my_obj_cache",
			  sizeof(struct my_obj),
			  0,                    // align은 0
			  SLAB_HWCACHE_ALIGN,   // 대신 캐시라인 정렬 플래그
			  my_obj_ctor);
```

---

## 5. 사용 예시

### 5.1 구조체 정의

```c
struct my_obj {
	spinlock_t lock;
	struct list_head list;
	int data;
};
```

### 5.2 constructor 정의

```c
static void my_obj_ctor(void *obj)
{
	struct my_obj *o = obj;

	spin_lock_init(&o->lock);
	INIT_LIST_HEAD(&o->list);
	/* data는 상황마다 값이 다르니까 여기서 굳이 채우지 않을 수도 있음 */
}
```

### 5.3 캐시 생성

```c
static struct kmem_cache *my_obj_cache;

static int __init my_init(void)
{
	my_obj_cache = kmem_cache_create("my_obj_cache",
					 sizeof(struct my_obj),
					 0,                    // align: 커널에 맡김
					 SLAB_HWCACHE_ALIGN,   // 캐시라인 정렬
					 my_obj_ctor);         // 기본 초기화
	if (!my_obj_cache)
		return -ENOMEM;

	return 0;
}
```

### 5.4 (간단) 할당 / 해제 예시

```c
struct my_obj *o;

o = kmem_cache_alloc(my_obj_cache, GFP_KERNEL);
if (!o)
	return -ENOMEM;

/* 필요 작업 수행 후 */

kmem_cache_free(my_obj_cache, o);
```

---

## 6. kmem_cache로부터 메모리 할당/해제

여기서는 **할당 함수/해제 함수의 시그니처와 사용 패턴**을 조금 더 자세히 정리한다.

### 6.1 `kmem_cache_alloc()`

```c
void *kmem_cache_alloc(struct kmem_cache *cachep, gfp_t flags);
```

- `cachep`
    
    - `kmem_cache_create()`로 만든 캐시에 대한 포인터.
        
- `flags`
    
    - `GFP_KERNEL`, `GFP_ATOMIC` 등 일반적인 GFP 플래그 사용.
        
    - 슬립 가능 여부, 컨텍스트에 따라 적절한 플래그를 선택해야 한다.
        
        - sleep 가능 컨텍스트: 보통 `GFP_KERNEL`.
            
        - interrupt context / bottom half 등: `GFP_ATOMIC`.
            
- 리턴값
    
    - 성공: 캐시에서 할당된 오브젝트 시작 주소.
        
    - 실패: `NULL`.
        
- 기본 사용 패턴:
    

```c
struct my_obj *o;

o = kmem_cache_alloc(my_obj_cache, GFP_KERNEL);
if (!o)
	return -ENOMEM;

/* 여기부터 o 사용 */
```

- 주의점
    
    - `ctor`가 설정돼 있다면, **새로 생성된 오브젝트에 대해서만** ctor가 호출되고,  
        이미 존재하던 오브젝트를 재사용할 때는 ctor가 다시 돌지 않는다.
        
    - 디버그 옵션이 없으면 `kmem_cache_alloc()`은 자동으로 zero-fill을 해주지 않는다.
        
        - 항상 0이 보장돼야 한다면:
            
            - 직접 `memset(o, 0, sizeof(*o));` 하거나,
                
            - `kmem_cache_zalloc()`(지원되는 커널 버전일 때)을 사용.
                

### 6.2 `kmem_cache_zalloc()` (있을 때)

```c
void *kmem_cache_zalloc(struct kmem_cache *cachep, gfp_t flags);
```

- `kmem_cache_alloc()` + `memset(obj, 0, size)`를 합쳐 놓은 형태다.
    
- 오브젝트 전체를 0으로 초기화한 상태로 받고 싶을 때 사용한다.
    
- ctor와 병행해서 쓸 경우:
    
    - ctor는 “항상 필요한 기본 초기화” (락 초기화, 리스트 헤드 등)
        
    - `zalloc`은 그 외 나머지 필드를 일단 0으로 만드는 용도로 역할이 분리된다.
        

### 6.3 `kmem_cache_free()`

```c
void kmem_cache_free(struct kmem_cache *cachep, void *objp);
```

- `cachep`
    
    - 이 오브젝트가 **원래 할당되었던** 캐시 포인터.
        
- `objp`
    
    - `kmem_cache_alloc()` (또는 `kmem_cache_zalloc()`)으로 받은 포인터.
        
- 사용 패턴:
    

```c
kmem_cache_free(my_obj_cache, o);
```

- 주의점
    
    - **반드시 같은 캐시로 되돌려야** 한다.
        
        - `kmem_cache_alloc(A)`로 받은 걸 `kmem_cache_free(B, obj)`로 넘기면 안 됨.
            
    - `kmem_cache_alloc()`으로 받은 포인터에 `kfree()`를 사용하면 안 됨.
        
    - 마찬가지로 `kmalloc()`으로 받은 포인터를 `kmem_cache_free()`에 넘기면 안 됨.
        
    - double free, use-after-free는 일반 메모리와 똑같이 위험하다.
        

### 6.4 에러 처리 및 lifetime 관리 예시

```c
struct my_obj *o;

o = kmem_cache_alloc(my_obj_cache, GFP_KERNEL);
if (!o)
	return -ENOMEM;

/* 초기화 (ctor에서 못 하는 per-instance 값 설정) */
o->data = some_value;

/* 리스트에 올리거나, 다른 구조에 연결 */
spin_lock(&global_lock);
list_add(&o->list, &global_list);
spin_unlock(&global_lock);

/* ... 나중에 더 이상 필요 없을 때 ... */
spin_lock(&global_lock);
list_del(&o->list);
spin_unlock(&global_lock);

kmem_cache_free(my_obj_cache, o);
```

- 포인트:
    
    - “소유 관계”를 명확히 해서 언제 `kmem_cache_free()`를 해야 하는지 결정해야 한다.
        
    - 리스트나 다른 자료구조에서 제거된 뒤에만 free 해야 한다.
        

---

## 7. `kmem_cache_destroy()` – 캐시 파괴

슬랩 캐시 사용을 끝낼 때는 `kmem_cache_destroy()`로 캐시 자체를 정리해야 한다.  
주로 **모듈 언로드 시점**이나 **초기화 실패 시 롤백 경로**에서 호출한다.

### 7.1 시그니처

```c
void kmem_cache_destroy(struct kmem_cache *cachep);
```

- `cachep`
    
    - `kmem_cache_create()`로 생성된 슬랩 캐시 포인터.
        

### 7.2 사용 조건

- **모든 오브젝트가 이미 해제된 상태여야 한다.**
    
    - 즉, 해당 캐시에서 `kmem_cache_alloc()`으로 할당된 것들은 모두 `kmem_cache_free()`로 반환된 뒤여야 한다.
        
- 코어 커널에서 전역적으로 사용하는 공용 캐시(예: `kmalloc-xx` 계열 등)에 대해서는 호출하면 안 되고,  
    **자기가 `kmem_cache_create()`로 직접 생성한 캐시**에 대해서만 `kmem_cache_destroy()`를 호출해야 한다.
    

이 조건이 깨진 상태에서 `kmem_cache_destroy()`를 호출하면:

- 슬랩 디버그 옵션이 있을 경우 warning / BUG가 날 수 있고,
    
- 아닌 경우 동작이 undefined에 가깝다 (메모리 누수, 크래시 등).
    

### 7.3 일반적인 사용 위치

1. **모듈 init 실패 경로**
    

```c
static int __init my_init(void)
{
	int ret;

	my_obj_cache = kmem_cache_create("my_obj_cache",
					 sizeof(struct my_obj),
					 0,
					 SLAB_HWCACHE_ALIGN,
					 my_obj_ctor);
	if (!my_obj_cache)
		return -ENOMEM;

	ret = my_subsystem_init();
	if (ret) {
		kmem_cache_destroy(my_obj_cache);
		return ret;
	}

	return 0;
}
```

2. **모듈 exit (언로드)**
    

```c
static void __exit my_exit(void)
{
	/* 이 시점에는 my_obj_cache에서 할당한 모든 객체가
	   이미 리스트에서 제거되고 kmem_cache_free() 되어 있어야 한다. */

	if (my_obj_cache)
		kmem_cache_destroy(my_obj_cache);
}
```

- 포인트:
    
    - exit 전에 전역 리스트, 해시 테이블 등에 남아 있는 오브젝트를 모두 정리하고 `kmem_cache_free()` 해야 한다.
        
    - 그 후에 `kmem_cache_destroy()`를 호출해 캐시를 완전히 반환한다.
        

### 7.4 `kmem_cache_shrink()`와의 차이 (간단히)

- `kmem_cache_shrink()`는 사용되지 않는 슬랩 페이지를 반납해 **메모리를 줄이는 역할**을 한다.
    
- `kmem_cache_destroy()`는 **캐시 자체를 없애는 것**이다.
    
- 보통 일반 모듈 코드에서는 `kmem_cache_shrink()`까지 직접 쓸 일은 드물고,  
    생성한 캐시는 그냥 `kmem_cache_destroy()`로 정리하는 정도면 충분한 경우가 많다.
    

---

## 8. 전체 흐름 요약

1. 모듈 초기화 시:
    
    - `kmem_cache_create()`로 전용 슬랩 캐시 생성.
        
2. 런타임 동안:
    
    - `kmem_cache_alloc()` / `kmem_cache_zalloc()`으로 오브젝트 할당.
        
    - 필요 없을 때마다 `kmem_cache_free()`로 반환.
        
3. 모듈 종료 또는 더 이상 캐시가 필요 없을 때:
    
    - 먼저 모든 오브젝트를 자료구조에서 제거하고 `kmem_cache_free()` 호출.
        
    - 마지막에 `kmem_cache_destroy()`로 캐시 자체를 파괴.
        

