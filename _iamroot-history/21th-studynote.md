---
title: 21주차(2018-09-15) 스터디 노트
date: 2018-09-16
---

<p>
제 21주차 2018년 9월 15일 (토)
</p><p>
| 모임장소 : 강남역 이지스터디<br>
| 모임시간 : 15:00 ~ 22:00<br>
| 참여인원 : 8명<br>
| 지난 진도 : start_kernel 내 setup_machine_fd() 마무리, parse_early_param() ~ efi_init()<br>
| 오늘 진도 : start_kernel 내 setup_arch() 내 arm64_memblock_init() 처음부터 early_init_fdt_scan_reserved_mem()까지<br>
1.진도, Time Table<br>
서적 :  코드로 알아보는 ARM 리눅스 커널<br>
2.스터디 내용<br>
5.1. 방법: 함께 한 줄씩 분석하며 논의한 내용을 바탕으로 주석을 남긴 후 git에 업데이트함<br>
5.2. 진행 사항:<br>
 - 위치: init/main.c -> linux/setup.c<br>
 - 분석 함수:<br>
   arm64_memblock_init()내의<br>
       fdt_enforce_memory_region() // dump 뜨기 위한 초기화(?)들<br>
       memblock_remove() // memblock.memory 에서 start부터 end까지 삭제<br>
       round_down() // memstart_addr을 align<br>
       memblock_add() // memblock.memory 영역 설정<br>
       memblock_reserve() // memblock.reserved 영역 설정<br>
       early_init_fdt_scan_reserved_mem() // fdt에서 reserved가 필요한 영역을 memblock.reserved 영역에 추가
</p>
