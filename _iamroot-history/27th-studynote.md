---
title: 27주차 2018년 10월 27일 (토) 스터디 노트
date: 2018-10-28
---

<p>
제 27주차 2018년 10월 27일 (토)
</p><p>
| 모임장소 : 강남역 이지스터디<br>
| 모임시간 : 15:00 ~ 22:00<br>
| 참여인원 : 4명<br>
| 지난 진도 : start_kernel 내 sparse_init() 끝<br>
| 오늘 진도 : start_kernel 내 zone_sizes_init() ~ find_zone_movable_pfns_for_nodes()<br>
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
            zone_sizes_init()<br>
                free_area_init_nodes()<br>
                    find_zone_movable_pfns_for_nodes()
</p>
