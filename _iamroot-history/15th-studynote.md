---
title: 15주차(2018-08-04) 스터디 노트
date: 2018-08-06
---

<p>
제 15주차 2018년 8월 4일 (토)
</p><p>
| 모임장소 : 더포도 분점(관악구 남현3길 62 지하)<br>
| 모임시간 : 15:00 ~ 22:00<br>
| 참여인원 : 6명<br>
| 지난 진도 : 리눅스 커널 심층분석 개정 3판 ~ 584 page
</p><p>
| 오늘 진도<br>
1.진도, Time Table<br>
서적 :  코드로 알아보는 ARM 리눅스 커널<br>
TimeTable<br>
2.스터디 내용<br>
5.1. 방법: 함께 한 줄씩 분석하며 논의한 내용을 바탕으로 주석을 남긴 후 git에 업데이트함<br>
5.2. 진행 사항:<br>
 - 위치: init/main.c<br>
 - 분석 함수:<br>
    asmlinkage __visible void __init start_kernel() 함수 내, <br>
     (1) set_task_stack_end_magic(&init_task);<br>
     (2) smp_setup_processor_id();<br>
     (3) debug_objects_early_init();<br>
     (4) cgroup_init_early();<br>
     함수 분석 완료.<br>
     main.c 네줄 나간 거 실화입니다.<br>
 
</p>
