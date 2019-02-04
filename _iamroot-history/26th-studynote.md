---
title: 26주차 2018년 10월 20일 (토) 스터디 노트
date: 2018-10-21
---

<p>
제 26주차 2018년 10월 20일 (토)
</p><p>
| 모임장소 : 강남역 이지스터디<br>
| 모임시간 : 15:00 ~ 22:00<br>
| 참여인원 : 3명<br>
| 지난 진도 : start_kernel 내 sparse_init() 일부<br>
| 오늘 진도 : start_kernel 내 sparse_init() ~ memblock_free_early()<br>
1.진도, Time Table<br>
서적 :  코드로 알아보는 ARM 리눅스 커널<br>
2.스터디 내용<br>
5.1. 방법: 함께 한 줄씩 분석하며 논의한 내용을 바탕으로 주석을 남긴 후 git에 업데이트함<br>
5.2. 진행 사항:<br>
 - 위치: init/main.c <br>
 - 분석 함수:<br>
    setup_arch()<br>
        bootmem_init()<br>
            sparse_init()<br>
                alloc_usemap_and_memmap()<br>
                sparse_early_mem_map_alloc()<br>
                sparse_init_one_section()<br>
                vmemmap_populate_print_last()<br>
                memblock_free_early()<br>
             zone_sizes_init() : 할 차례
</p>
