---
title: 29주차 스터디 노트 (11.10)
date: 2018-11-11
---

<p>
제 29주차 2018년 11월 10일 (토)
</p><p>
| 모임장소 : 강남역 이지스터디<br>
| 모임시간 : 15:00 ~ 22:00<br>
| 참여인원 : 7명<br>
| 지난 진도 : free_area_init_nodes() 진행 중<br>
| 오늘 진도 : setup_arch() 내 bootmem_init()/free_area_init_nodes() ~ cpu_read_bootcpu_ops()<br>
서적 :  코드로 알아보는 ARM 리눅스 커널
</p><p>
2.스터디 내용<br>
5.1. 방법: 함께 한 줄씩 분석하며 논의한 내용을 바탕으로 주석을 남긴 후 git에 업데이트함<br>
5.2. 진행 사항:<br>
 - 위치: init/main.c <br>
 - 분석 함수:<br>
    setup_arch()<br>
        bootmem_init()  <br>
        kasan_init()<br>
        request_standard_resources()<br>
        early_ioremap_reset()<br>
        psci_dt_init()<br>
        cpu_read_bootcpu_ops()
</p>
