---
title: 19주차 2018년 9월 1일 (토) 스터디 노트
date: 2018-09-01
---

<p>
제 19주차 2018년 9월 1일 (토)
</p><p>
| 모임장소 : 사당역 더포도 스터디룸<br>
| 모임시간 : 15:00 ~ 22:00<br>
| 참여인원 : 5명<br>
| 지난 진도 : start_kernel 내 setup_machine_fdt 일부<br>
| 오늘 진도 : start_kernel 내 early_init_dt_add_memory_arch() 일부<br>
1.진도, Time Table<br>
서적 :  코드로 알아보는 ARM 리눅스 커널<br>
2.스터디 내용<br>
5.1. 방법: 함께 한 줄씩 분석하며 논의한 내용을 바탕으로 주석을 남긴 후 git에 업데이트함<br>
5.2. 진행 사항:<br>
 - 위치: init/main.c -> linux/setup.c<br>
 - 분석 함수:<br>
    early_init_dt_scan<br>
         early_init_dt_scan_memory()<br>
         early_init_dt_add_memory_arch()<br>
         memblock_add()<br>
         memblock_add_range() -> 진행중 (memblock_double_array() 부터 시작)
</p><p>
         
</p>
