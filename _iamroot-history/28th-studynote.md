---
title: 28주차 스터디 노트 (11.3)
date: 2018-11-07
---

<p>
제 28주차 2018년 11월 3일 (토)
</p><p>
| 모임장소 : 강남역 이지스터디<br>
| 모임시간 : 15:00 ~ 22:00<br>
| 참여인원 : 5명<br>
| 지난 진도 : free_area_init_nodes() 진행 중<br>
| 오늘 진도 : free_area_init_nodes() 여전히 진행 중​<br>
마지막 라인의 for_each_online_node에서, 각각의 node에 대해 free_area_init_node(), free_area_init_core()로 진입, 이어서 분석이 필요합니다.<br>
서적 :  코드로 알아보는 ARM 리눅스 커널
</p><p>
2.스터디 내용<br>
5.1. 방법: 함께 한 줄씩 분석하며 논의한 내용을 바탕으로 주석을 남긴 후 git에 업데이트함<br>
5.2. 진행 사항:<br>
 - 위치: init/main.c <br>
 - 분석 함수:<br>
    setup_arch()<br>
        bootmem_init()<br>
            sparse_init()<br>
            zone_sizes_init()<br>
                free_area_init_nodes() -> 27주차에 이어 계속 진행중입니다.<br>
​free_area_init_node()​<br>
​free_area_init_core()
</p>
