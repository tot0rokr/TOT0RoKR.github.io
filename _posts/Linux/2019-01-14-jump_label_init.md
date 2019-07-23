---
title: "jump_label_init()"
classes: wide
excerpt: "jump label들에 대해 NOP과 JMP를 setting"
date: 2019-01-14T02:52:00-09:00
last_modified_at: 2019-02-14T03:08:00-09:00
tag:
- jump
- likely
- optimization
---

# jump_label_init()

일단, arm64 default config로는 jump label을 사용안함. 그러나 분석한 김에 작성함.
jump label은 cpu의 pipelining에서 branch 하자드를 없애주기 위함이며
unlikely와 likely 최적화에 사용된다. 

jump label이 붙은 코드를 통해 table을 만들고 branch할지 넘어갈지 설정하여
branch 예측을 강제로 넣어준다고 생각하면 될 것으로 보인다.


## 코드 설명

{% highlight c linenos %}
void __init jump_label_init(void)
{
	// TOT0Ro >> __init과 같은 매크로 태그를 이용에 컴파일 타임에 수집.
	// jump_table을 생성.
	struct jump_entry *iter_start = __start___jump_table;
	struct jump_entry *iter_stop = __stop___jump_table;
	struct static_key *key = NULL;
	struct jump_entry *iter;

	/*
	 * Since we are initializing the static_key.enabled field with
	 * with the 'raw' int values (to avoid pulling in atomic.h) in
	 * jump_label.h, let's make sure that is safe. There are only two
	 * cases to check since we initialize to 0 or 1.
	 */
	BUILD_BUG_ON((int)ATOMIC_INIT(0) != 0);
	BUILD_BUG_ON((int)ATOMIC_INIT(1) != 1);

	if (static_key_initialized)
		return;

	cpus_read_lock();
	jump_label_lock();
	// TOT0Ro >> Head 정렬을 수행한다.
	jump_label_sort_entries(iter_start, iter_stop);

	for (iter = iter_start; iter < iter_stop; iter++) {
		struct static_key *iterk;

		/* rewrite NOPs */
		// TOT0Ro >> jump label 주소에 NOP 명령에 대한 재정의. A64는 기본으로 NOP을 사용하고
		// 필요시 arch~~~transform 함수로 branch로 변경. (근데 여기서는 안하네?)
		if (jump_label_type(iter) == JUMP_LABEL_NOP)
			arch_jump_label_transform_static(iter, JUMP_LABEL_NOP);

		// TOT0Ro >> 최하위 비트는 0이면 nop, 1이면 branch를 의미. 날려버리고 key만 꺼냄.
		iterk = jump_entry_key(iter);
		if (iterk == key)
			continue;

		key = iterk;
		// TOT0Ro >> branch냐 nop이냐는 설정 했으니(언제?) key만 다시 iter에 저장.
		static_key_set_entries(key, iter);
	}
	static_key_initialized = true;
	jump_label_unlock();
	cpus_read_unlock();
}
{% endhighlight %}

> https://github.com/TOT0RoKR/linux/blob/freedom/kernel/jump_label.c#L383



## 동작 과정

{% include video id="a5kq0vbfmYQ" provider="youtube" %}


