---
title: 30주차 스터디 노트 (11.17)
date: 2018-11-19
---

<p>
제 30주차 2018년 11월 17일 (토)
</p><p>
| 모임장소 : 여의도역 국제금융로 2길 25 ​<br>
| 모임시간 : 15:00 ~ 22:00<br>
| 참여인원 : 6명<br>
| 지난 진도 : setup_arch() 진행 중<br>
| 오늘 진도 : setup_arch() 마무리, 내 bootmem_init()/free_area_init_nodes() ~ cpu_read_bootcpu_ops()<br>
서적 :  코드로 알아보는 ARM 리눅스 커널
</p><p>
2.스터디 내용<br>
5.1. 방법: 함께 한 줄씩 분석하며 논의한 내용을 바탕으로 주석을 남긴 후 git에 업데이트함<br>
5.2. 진행 사항:<br>
 - 위치: init/main.c <br>
 - 분석 함수:<br>
    setup_arch() 끝<br>
    add_latent_entropy()<br>
    add_device_randomness()<br>
    boot_init_stack_canary()<br>
    mm_init_cpumask()<br>
    setup_command_line()<br>
    setup_nr_cpu_ids()<br>
    setup_per_cpu_areas() 관련 책 507p 읽다가 중단함 <br>
 
</p>
