---
title: 16주차(2018-08-11) 스터디 노트
date: 2018-08-12
---

<p>
제 16주차 2018년 8월 11일 (토)
</p><p>
| 모임장소 : 강남역 스터디블룸<br>
| 모임시간 : 15:00 ~ 22:00<br>
| 참여인원 : 8명<br>
| 지난 진도 : start_kernel 내 cgroup 초기화<br>
| 오늘 진도 : start_kernel 내 setup_arch 일부<br>
1.진도, Time Table<br>
서적 :  코드로 알아보는 ARM 리눅스 커널<br>
TimeTable<br>
2.스터디 내용<br>
5.1. 방법: 함께 한 줄씩 분석하며 논의한 내용을 바탕으로 주석을 남긴 후 git에 업데이트함<br>
5.2. 진행 사항:<br>
 - 위치: init/main.c<br>
 - 분석 함수:<br>
    asmlinkage __visible void __init start_kernel() 함수 내, <br>
      local_irq_disable()<br>
      boot_cpu_init()<br>
      page_address_init()<br>
      setup_arch ()일부<br>
      4줄도 못 나간거 실화입니다.<br>
  - commit에 포함되지 않은 DTS 관련 내용 스터디<br>
   (boot_command_line의 초기화 코드 찾던 중 진행)<br>
 
</p>
