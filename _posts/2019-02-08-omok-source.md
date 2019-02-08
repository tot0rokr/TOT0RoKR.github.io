---
title: "Omok Source"
last_modified_at: 2019-02-08T12:07:00-09:00
categories:
- Clang
tags:
- clang
excerpt: "variable, loop, conditional을 사용하지 않고 오목만들기 소스코드"
---

## Intro

어릴 때, 변수, 반복문, 조건문 만으로 오목 만들기를 해보고 싶어 시도.
나는 이 사례를 통해 모든 프로그램은 변수, 반복문, 조건문 만으로 모든 프로그램을 만들 수 있다고 말하며,
그에 대한 뒷바침 근거로 사용하고 있다.

오로지 printf, scanf, if문, for문만을 사용하고 있다. 배열도 사용하지 않는다.
주석을 보면 어릴 때라 그런지 되게 즐거워 하면서 코딩한 것으로 보인다.
~~_나 자신이지만 귀엽다_~~


## 소스코드

``` c

#include <stdio.h>
int main()
{
    //이거슨 진정한 바둑판이다.
    int Pan0101, Pan0102, Pan0103, Pan0104, Pan0105, Pan0106, Pan0107, Pan0108, Pan0109, Pan0110, Pan0111, Pan0112, Pan0113, Pan0114, Pan0115, Pan0116, Pan0117, Pan0118, Pan0119;
    int Pan0201, Pan0202, Pan0203, Pan0204, Pan0205, Pan0206, Pan0207, Pan0208, Pan0209, Pan0210, Pan0211, Pan0212, Pan0213, Pan0214, Pan0215, Pan0216, Pan0217, Pan0218, Pan0219;
    int Pan0301, Pan0302, Pan0303, Pan0304, Pan0305, Pan0306, Pan0307, Pan0308, Pan0309, Pan0310, Pan0311, Pan0312, Pan0313, Pan0314, Pan0315, Pan0316, Pan0317, Pan0318, Pan0319;
    int Pan0401, Pan0402, Pan0403, Pan0404, Pan0405, Pan0406, Pan0407, Pan0408, Pan0409, Pan0410, Pan0411, Pan0412, Pan0413, Pan0414, Pan0415, Pan0416, Pan0417, Pan0418, Pan0419;
    int Pan0501, Pan0502, Pan0503, Pan0504, Pan0505, Pan0506, Pan0507, Pan0508, Pan0509, Pan0510, Pan0511, Pan0512, Pan0513, Pan0514, Pan0515, Pan0516, Pan0517, Pan0518, Pan0519;
    int Pan0601, Pan0602, Pan0603, Pan0604, Pan0605, Pan0606, Pan0607, Pan0608, Pan0609, Pan0610, Pan0611, Pan0612, Pan0613, Pan0614, Pan0615, Pan0616, Pan0617, Pan0618, Pan0619;
    int Pan0701, Pan0702, Pan0703, Pan0704, Pan0705, Pan0706, Pan0707, Pan0708, Pan0709, Pan0710, Pan0711, Pan0712, Pan0713, Pan0714, Pan0715, Pan0716, Pan0717, Pan0718, Pan0719;
    int Pan0801, Pan0802, Pan0803, Pan0804, Pan0805, Pan0806, Pan0807, Pan0808, Pan0809, Pan0810, Pan0811, Pan0812, Pan0813, Pan0814, Pan0815, Pan0816, Pan0817, Pan0818, Pan0819;
    int Pan0901, Pan0902, Pan0903, Pan0904, Pan0905, Pan0906, Pan0907, Pan0908, Pan0909, Pan0910, Pan0911, Pan0912, Pan0913, Pan0914, Pan0915, Pan0916, Pan0917, Pan0918, Pan0919;
    int Pan1001, Pan1002, Pan1003, Pan1004, Pan1005, Pan1006, Pan1007, Pan1008, Pan1009, Pan1010, Pan1011, Pan1012, Pan1013, Pan1014, Pan1015, Pan1016, Pan1017, Pan1018, Pan1019;
    int Pan1101, Pan1102, Pan1103, Pan1104, Pan1105, Pan1106, Pan1107, Pan1108, Pan1109, Pan1110, Pan1111, Pan1112, Pan1113, Pan1114, Pan1115, Pan1116, Pan1117, Pan1118, Pan1119;
    int Pan1201, Pan1202, Pan1203, Pan1204, Pan1205, Pan1206, Pan1207, Pan1208, Pan1209, Pan1210, Pan1211, Pan1212, Pan1213, Pan1214, Pan1215, Pan1216, Pan1217, Pan1218, Pan1219;
    int Pan1301, Pan1302, Pan1303, Pan1304, Pan1305, Pan1306, Pan1307, Pan1308, Pan1309, Pan1310, Pan1311, Pan1312, Pan1313, Pan1314, Pan1315, Pan1316, Pan1317, Pan1318, Pan1319;
    int Pan1401, Pan1402, Pan1403, Pan1404, Pan1405, Pan1406, Pan1407, Pan1408, Pan1409, Pan1410, Pan1411, Pan1412, Pan1413, Pan1414, Pan1415, Pan1416, Pan1417, Pan1418, Pan1419;
    int Pan1501, Pan1502, Pan1503, Pan1504, Pan1505, Pan1506, Pan1507, Pan1508, Pan1509, Pan1510, Pan1511, Pan1512, Pan1513, Pan1514, Pan1515, Pan1516, Pan1517, Pan1518, Pan1519;
    int Pan1601, Pan1602, Pan1603, Pan1604, Pan1605, Pan1606, Pan1607, Pan1608, Pan1609, Pan1610, Pan1611, Pan1612, Pan1613, Pan1614, Pan1615, Pan1616, Pan1617, Pan1618, Pan1619;
    int Pan1701, Pan1702, Pan1703, Pan1704, Pan1705, Pan1706, Pan1707, Pan1708, Pan1709, Pan1710, Pan1711, Pan1712, Pan1713, Pan1714, Pan1715, Pan1716, Pan1717, Pan1718, Pan1719;
    int Pan1801, Pan1802, Pan1803, Pan1804, Pan1805, Pan1806, Pan1807, Pan1808, Pan1809, Pan1810, Pan1811, Pan1812, Pan1813, Pan1814, Pan1815, Pan1816, Pan1817, Pan1818, Pan1819;
    int Pan1901, Pan1902, Pan1903, Pan1904, Pan1905, Pan1906, Pan1907, Pan1908, Pan1909, Pan1910, Pan1911, Pan1912, Pan1913, Pan1914, Pan1915, Pan1916, Pan1917, Pan1918, Pan1919;
    int sel=0, end=0; // 시작 할지 안 할지 선택하기 위한 변수
    int temp1; // 쓰레기 변수 (1과 2)
    int xy; // 좌표
    int turn=2; // 니턴 내턴 (초기값은 흑돌부터)
    int win; // 승리!
    int WWEB=0, BWEB=0; // 연승
    while(1)
    {
        /* 바둑판 초기화*/

        Pan0101=101, Pan0102=102, Pan0103=103, Pan0104=104, Pan0105=105, Pan0106=106, Pan0107=107, Pan0108=108, Pan0109=109, Pan0110=110, Pan0111=111, Pan0112=112, Pan0113=113, Pan0114=114, Pan0115=115, Pan0116=116, Pan0117=117, Pan0118=118, Pan0119=119;
        Pan0201=201, Pan0202=202, Pan0203=203, Pan0204=204, Pan0205=205, Pan0206=206, Pan0207=207, Pan0208=208, Pan0209=209, Pan0210=210, Pan0211=211, Pan0212=212, Pan0213=213, Pan0214=214, Pan0215=215, Pan0216=216, Pan0217=217, Pan0218=218, Pan0219=219;
        Pan0301=301, Pan0302=302, Pan0303=303, Pan0304=304, Pan0305=305, Pan0306=306, Pan0307=307, Pan0308=308, Pan0309=309, Pan0310=310, Pan0311=311, Pan0312=312, Pan0313=313, Pan0314=314, Pan0315=315, Pan0316=316, Pan0317=317, Pan0318=318, Pan0319=319;
        Pan0401=401, Pan0402=402, Pan0403=403, Pan0404=404, Pan0405=405, Pan0406=406, Pan0407=407, Pan0408=408, Pan0409=409, Pan0410=410, Pan0411=411, Pan0412=412, Pan0413=413, Pan0414=414, Pan0415=415, Pan0416=416, Pan0417=417, Pan0418=418, Pan0419=419;
        Pan0501=501, Pan0502=502, Pan0503=503, Pan0504=504, Pan0505=505, Pan0506=506, Pan0507=507, Pan0508=508, Pan0509=509, Pan0510=510, Pan0511=511, Pan0512=512, Pan0513=513, Pan0514=514, Pan0515=515, Pan0516=516, Pan0517=517, Pan0518=518, Pan0519=519;
        Pan0601=601, Pan0602=602, Pan0603=603, Pan0604=604, Pan0605=605, Pan0606=606, Pan0607=607, Pan0608=608, Pan0609=609, Pan0610=610, Pan0611=611, Pan0612=612, Pan0613=613, Pan0614=614, Pan0615=615, Pan0616=616, Pan0617=617, Pan0618=618, Pan0619=619;
        Pan0701=701, Pan0702=702, Pan0703=703, Pan0704=704, Pan0705=705, Pan0706=706, Pan0707=707, Pan0708=708, Pan0709=709, Pan0710=710, Pan0711=711, Pan0712=712, Pan0713=713, Pan0714=714, Pan0715=715, Pan0716=716, Pan0717=717, Pan0718=718, Pan0719=719;
        Pan0801=801, Pan0802=802, Pan0803=803, Pan0804=804, Pan0805=805, Pan0806=806, Pan0807=807, Pan0808=808, Pan0809=809, Pan0810=810, Pan0811=811, Pan0812=812, Pan0813=813, Pan0814=814, Pan0815=815, Pan0816=816, Pan0817=817, Pan0818=818, Pan0819=819;
        Pan0901=901, Pan0902=902, Pan0903=903, Pan0904=904, Pan0905=905, Pan0906=906, Pan0907=907, Pan0908=908, Pan0909=909, Pan0910=910, Pan0911=911, Pan0912=912, Pan0913=913, Pan0914=914, Pan0915=915, Pan0916=916, Pan0917=917, Pan0918=918, Pan0919=919;
        Pan1001=1001, Pan1002=1002, Pan1003=1003, Pan1004=1004, Pan1005=1005, Pan1006=1006, Pan1007=1007, Pan1008=1008, Pan1009=1009, Pan1010=1010, Pan1011=1011, Pan1012=1012, Pan1013=1013, Pan1014=1014, Pan1015=1015, Pan1016=1016, Pan1017=1017, Pan1018=1018, Pan1019=1019;
        Pan1101=1101, Pan1102=1102, Pan1103=1103, Pan1104=1104, Pan1105=1105, Pan1106=1106, Pan1107=1107, Pan1108=1108, Pan1109=1109, Pan1110=1110, Pan1111=1111, Pan1112=1112, Pan1113=1113, Pan1114=1114, Pan1115=1115, Pan1116=1116, Pan1117=1117, Pan1118=1118, Pan1119=1119;
        Pan1201=1201, Pan1202=1202, Pan1203=1203, Pan1204=1204, Pan1205=1205, Pan1206=1206, Pan1207=1207, Pan1208=1208, Pan1209=1209, Pan1210=1210, Pan1211=1211, Pan1212=1212, Pan1213=1213, Pan1214=1214, Pan1215=1215, Pan1216=1216, Pan1217=1217, Pan1218=1218, Pan1219=1219;
        Pan1301=1301, Pan1302=1302, Pan1303=1303, Pan1304=1304, Pan1305=1305, Pan1306=1306, Pan1307=1307, Pan1308=1308, Pan1309=1309, Pan1310=1310, Pan1311=1311, Pan1312=1312, Pan1313=1313, Pan1314=1314, Pan1315=1315, Pan1316=1316, Pan1317=1317, Pan1318=1318, Pan1319=1319;
        Pan1401=1401, Pan1402=1402, Pan1403=1403, Pan1404=1404, Pan1405=1405, Pan1406=1406, Pan1407=1407, Pan1408=1408, Pan1409=1409, Pan1410=1410, Pan1411=1411, Pan1412=1412, Pan1413=1413, Pan1414=1414, Pan1415=1415, Pan1416=1416, Pan1417=1417, Pan1418=1418, Pan1419=1419;
        Pan1501=1501, Pan1502=1502, Pan1503=1503, Pan1504=1504, Pan1505=1505, Pan1506=1506, Pan1507=1507, Pan1508=1508, Pan1509=1509, Pan1510=1510, Pan1511=1511, Pan1512=1512, Pan1513=1513, Pan1514=1514, Pan1515=1515, Pan1516=1516, Pan1517=1517, Pan1518=1518, Pan1519=1519;
        Pan1601=1601, Pan1602=1602, Pan1603=1603, Pan1604=1604, Pan1605=1605, Pan1606=1606, Pan1607=1607, Pan1608=1608, Pan1609=1609, Pan1610=1610, Pan1611=1611, Pan1612=1612, Pan1613=1613, Pan1614=1614, Pan1615=1615, Pan1616=1616, Pan1617=1617, Pan1618=1618, Pan1619=1619;
        Pan1701=1701, Pan1702=1702, Pan1703=1703, Pan1704=1704, Pan1705=1705, Pan1706=1706, Pan1707=1707, Pan1708=1708, Pan1709=1709, Pan1710=1710, Pan1711=1711, Pan1712=1712, Pan1713=1713, Pan1714=1714, Pan1715=1715, Pan1716=1716, Pan1717=1717, Pan1718=1718, Pan1719=1719;
        Pan1801=1801, Pan1802=1802, Pan1803=1803, Pan1804=1804, Pan1805=1805, Pan1806=1806, Pan1807=1807, Pan1808=1808, Pan1809=1809, Pan1810=1810, Pan1811=1811, Pan1812=1812, Pan1813=1813, Pan1814=1814, Pan1815=1815, Pan1816=1816, Pan1817=1817, Pan1818=1818, Pan1819=1819;
        Pan1901=1901, Pan1902=1902, Pan1903=1903, Pan1904=1904, Pan1905=1905, Pan1906=1906, Pan1907=1907, Pan1908=1908, Pan1909=1909, Pan1910=1910, Pan1911=1911, Pan1912=1912, Pan1913=1913, Pan1914=1914, Pan1915=1915, Pan1916=1916, Pan1917=1917, Pan1918=1918, Pan1919=1919;

        /* 변수 초기화 */
        xy=0;
        win=0;

        while(1)            //시작하시겠습니까? 예, 아니오
        {
            if(WWEB!=0)    // 연승 체크
            {
                printf("\n\n\n\t\t\t  백돌 : ");
                printf(" %d 연승 \n\n", WWEB);
            }
            else if(BWEB!=0)
            {
                printf("\n\n\n\t\t\t  흑돌 : ");
                printf(" %d 연승 \n\n", BWEB);
            }

            printf("\n\n\n\n게임하기 : 1 \t 끝내기 : 2\n 선택하세요 : "); // 메뉴
            fflush(stdin);
            scanf("%d", &sel);
            if(sel==1)
                break;
            else if(sel==2)
            {
                end=1;
                break;
            }
            else
                printf("\n\n\n다시입력하세요.\n\n\n");
        }
        if(end==1)
            break;

        /* 스타트 */
        printf("\n\n\n다음으로 가실려면 엔터를 눌러주세요.");
        fflush(stdin);
        scanf("%c", &temp1);
        printf("\n\n\n\n\n\n\n\n\n\n==================================필 독 규 칙=================================\n\n\n");
        printf("   게임은 아시다시피 오목입니다. 오목 방법은 일단 먼저 가로든 세로든\n\n");
        printf("   대각선이든 무조건 먼저 일렬로 5개 먼저 두면 이깁니다.\n\n");
        printf("   그게 중요한게 아니라 이 게임의 바둑 돌은 놓는 방법은 좌표를 입력하는\n\n");
        printf("   것입니다. 세로줄의 숫자를 먼저 쓰고 그 뒤에 가로줄의 숫자를 입력합니\n\n");
        printf("   다. 끝입니다.          항복은 좌표를 9999 입력하시면 됩니다.        \n\n\n");
        printf("   ex) 세로3,가로5 : 305  세로13,가로8 : 1308  세로6,가로11 : 611 \n\n");
        printf("===========================================================================\n\n");
        printf("\n\n\n다음으로 가실려면 엔터를 눌러주세요.");
        fflush(stdin);
        scanf("%c", &temp1);
        while(1)
        {                    //우어어 바둑판
            printf("\n\n");
            if( Pan0101==101 ) printf(" 1┌");
            else if( Pan0101==1 ) printf("●");
            else if( Pan0101==2 ) printf("○");
            if( Pan0102==102 ) printf("┬");
            else if( Pan0102==1 ) printf("●");
            else if( Pan0102==2 ) printf("○");
            if( Pan0103==103 ) printf("┬");
            else if( Pan0103==1 ) printf("●");
            else if( Pan0103==2 ) printf("○");
            if( Pan0104==104 ) printf("┬");
            else if( Pan0104==1 ) printf("●");
            else if( Pan0104==2 ) printf("○");
            if( Pan0105==105 ) printf("┬");
            else if( Pan0105==1 ) printf("●");
            else if( Pan0105==2 ) printf("○");
            if( Pan0106==106 ) printf("┬");
            else if( Pan0106==1 ) printf("●");
            else if( Pan0106==2 ) printf("○");
            if( Pan0107==107 ) printf("┬");
            else if( Pan0107==1 ) printf("●");
            else if( Pan0107==2 ) printf("○");
            if( Pan0108==108 ) printf("┬");
            else if( Pan0108==1 ) printf("●");
            else if( Pan0108==2 ) printf("○");
            if( Pan0109==109 ) printf("┬");
            else if( Pan0109==1 ) printf("●");
            else if( Pan0109==2 ) printf("○");
            if( Pan0110==110 ) printf("┬");
            else if( Pan0110==1 ) printf("●");
            else if( Pan0110==2 ) printf("○");
            if( Pan0111==111 ) printf("┬");
            else if( Pan0111==1 ) printf("●");
            else if( Pan0111==2 ) printf("○");
            if( Pan0112==112 ) printf("┬");
            else if( Pan0112==1 ) printf("●");
            else if( Pan0112==2 ) printf("○");
            if( Pan0113==113 ) printf("┬");
            else if( Pan0113==1 ) printf("●");
            else if( Pan0113==2 ) printf("○");
            if( Pan0114==114 ) printf("┬");
            else if( Pan0114==1 ) printf("●");
            else if( Pan0114==2 ) printf("○");
            if( Pan0115==115 ) printf("┬");
            else if( Pan0115==1 ) printf("●");
            else if( Pan0115==2 ) printf("○");
            if( Pan0116==116 ) printf("┬");
            else if( Pan0116==1 ) printf("●");
            else if( Pan0116==2 ) printf("○");
            if( Pan0117==117 ) printf("┬");
            else if( Pan0117==1 ) printf("●");
            else if( Pan0117==2 ) printf("○");
            if( Pan0118==118 ) printf("┬");
            else if( Pan0118==1 ) printf("●");
            else if( Pan0118==2 ) printf("○");
            if( Pan0119==119 ) printf("┐\n");
            else if( Pan0119==1 ) printf("●\n");
            else if( Pan0119==2 ) printf("○\n");
            if( Pan0201==201 ) printf(" 2├");
            else if( Pan0201==1 ) printf("●");
            else if( Pan0201==2 ) printf("○");
            if( Pan0202==202 ) printf("┼");
            else if( Pan0202==1 ) printf("●");
            else if( Pan0202==2 ) printf("○");
            if( Pan0203==203 ) printf("┼");
            else if( Pan0203==1 ) printf("●");
            else if( Pan0203==2 ) printf("○");
            if( Pan0204==204 ) printf("┼");
            else if( Pan0204==1 ) printf("●");
            else if( Pan0204==2 ) printf("○");
            if( Pan0205==205 ) printf("┼");
            else if( Pan0205==1 ) printf("●");
            else if( Pan0205==2 ) printf("○");
            if( Pan0206==206 ) printf("┼");
            else if( Pan0206==1 ) printf("●");
            else if( Pan0206==2 ) printf("○");
            if( Pan0207==207 ) printf("┼");
            else if( Pan0207==1 ) printf("●");
            else if( Pan0207==2 ) printf("○");
            if( Pan0208==208 ) printf("┼");
            else if( Pan0208==1 ) printf("●");
            else if( Pan0208==2 ) printf("○");
            if( Pan0209==209 ) printf("┼");
            else if( Pan0209==1 ) printf("●");
            else if( Pan0209==2 ) printf("○");
            if( Pan0210==210 ) printf("┼");
            else if( Pan0210==1 ) printf("●");
            else if( Pan0210==2 ) printf("○");
            if( Pan0211==211 ) printf("┼");
            else if( Pan0211==1 ) printf("●");
            else if( Pan0211==2 ) printf("○");
            if( Pan0212==212 ) printf("┼");
            else if( Pan0212==1 ) printf("●");
            else if( Pan0212==2 ) printf("○");
            if( Pan0213==213 ) printf("┼");
            else if( Pan0213==1 ) printf("●");
            else if( Pan0213==2 ) printf("○");
            if( Pan0214==214 ) printf("┼");
            else if( Pan0214==1 ) printf("●");
            else if( Pan0214==2 ) printf("○");
            if( Pan0215==215 ) printf("┼");
            else if( Pan0215==1 ) printf("●");
            else if( Pan0215==2 ) printf("○");
            if( Pan0216==216 ) printf("┼");
            else if( Pan0216==1 ) printf("●");
            else if( Pan0216==2 ) printf("○");
            if( Pan0217==217 ) printf("┼");
            else if( Pan0217==1 ) printf("●");
            else if( Pan0217==2 ) printf("○");
            if( Pan0218==218 ) printf("┼");
            else if( Pan0218==1 ) printf("●");
            else if( Pan0218==2 ) printf("○");
            if( Pan0219==219 ) printf("┤\n");
            else if( Pan0219==1 ) printf("●\n");
            else if( Pan0219==2 ) printf("○\n");
            if( Pan0301==301 ) printf(" 3├");
            else if( Pan0301==1 ) printf("●");
            else if( Pan0301==2 ) printf("○");
            if( Pan0302==302 ) printf("┼");
            else if( Pan0302==1 ) printf("●");
            else if( Pan0302==2 ) printf("○");
            if( Pan0303==303 ) printf("┼");
            else if( Pan0303==1 ) printf("●");
            else if( Pan0303==2 ) printf("○");
            if( Pan0304==304 ) printf("┼");
            else if( Pan0304==1 ) printf("●");
            else if( Pan0304==2 ) printf("○");
            if( Pan0305==305 ) printf("┼");
            else if( Pan0305==1 ) printf("●");
            else if( Pan0305==2 ) printf("○");
            if( Pan0306==306 ) printf("┼");
            else if( Pan0306==1 ) printf("●");
            else if( Pan0306==2 ) printf("○");
            if( Pan0307==307 ) printf("┼");
            else if( Pan0307==1 ) printf("●");
            else if( Pan0307==2 ) printf("○");
            if( Pan0308==308 ) printf("┼");
            else if( Pan0308==1 ) printf("●");
            else if( Pan0308==2 ) printf("○");
            if( Pan0309==309 ) printf("┼");
            else if( Pan0309==1 ) printf("●");
            else if( Pan0309==2 ) printf("○");
            if( Pan0310==310 ) printf("┼");
            else if( Pan0310==1 ) printf("●");
            else if( Pan0310==2 ) printf("○");
            if( Pan0311==311 ) printf("┼");
            else if( Pan0311==1 ) printf("●");
            else if( Pan0311==2 ) printf("○");
            if( Pan0312==312 ) printf("┼");
            else if( Pan0312==1 ) printf("●");
            else if( Pan0312==2 ) printf("○");
            if( Pan0313==313 ) printf("┼");
            else if( Pan0313==1 ) printf("●");
            else if( Pan0313==2 ) printf("○");
            if( Pan0314==314 ) printf("┼");
            else if( Pan0314==1 ) printf("●");
            else if( Pan0314==2 ) printf("○");
            if( Pan0315==315 ) printf("┼");
            else if( Pan0315==1 ) printf("●");
            else if( Pan0315==2 ) printf("○");
            if( Pan0316==316 ) printf("┼");
            else if( Pan0316==1 ) printf("●");
            else if( Pan0316==2 ) printf("○");
            if( Pan0317==317 ) printf("┼");
            else if( Pan0317==1 ) printf("●");
            else if( Pan0317==2 ) printf("○");
            if( Pan0318==318 ) printf("┼");
            else if( Pan0318==1 ) printf("●");
            else if( Pan0318==2 ) printf("○");
            if( Pan0319==319 ) printf("┤\n");
            else if( Pan0319==1 ) printf("●\n");
            else if( Pan0319==2 ) printf("○\n");
            if( Pan0401==401 ) printf(" 4├");
            else if( Pan0401==1 ) printf("●");
            else if( Pan0401==2 ) printf("○");
            if( Pan0402==402 ) printf("┼");
            else if( Pan0402==1 ) printf("●");
            else if( Pan0402==2 ) printf("○");
            if( Pan0403==403 ) printf("┼");
            else if( Pan0403==1 ) printf("●");
            else if( Pan0403==2 ) printf("○");
            if( Pan0404==404 ) printf("┼");
            else if( Pan0404==1 ) printf("●");
            else if( Pan0404==2 ) printf("○");
            if( Pan0405==405 ) printf("┼");
            else if( Pan0405==1 ) printf("●");
            else if( Pan0405==2 ) printf("○");
            if( Pan0406==406 ) printf("┼");
            else if( Pan0406==1 ) printf("●");
            else if( Pan0406==2 ) printf("○");
            if( Pan0407==407 ) printf("┼");
            else if( Pan0407==1 ) printf("●");
            else if( Pan0407==2 ) printf("○");
            if( Pan0408==408 ) printf("┼");
            else if( Pan0408==1 ) printf("●");
            else if( Pan0408==2 ) printf("○");
            if( Pan0409==409 ) printf("┼");
            else if( Pan0409==1 ) printf("●");
            else if( Pan0409==2 ) printf("○");
            if( Pan0410==410 ) printf("┼");
            else if( Pan0410==1 ) printf("●");
            else if( Pan0410==2 ) printf("○");
            if( Pan0411==411 ) printf("┼");
            else if( Pan0411==1 ) printf("●");
            else if( Pan0411==2 ) printf("○");
            if( Pan0412==412 ) printf("┼");
            else if( Pan0412==1 ) printf("●");
            else if( Pan0412==2 ) printf("○");
            if( Pan0413==413 ) printf("┼");
            else if( Pan0413==1 ) printf("●");
            else if( Pan0413==2 ) printf("○");
            if( Pan0414==414 ) printf("┼");
            else if( Pan0414==1 ) printf("●");
            else if( Pan0414==2 ) printf("○");
            if( Pan0415==415 ) printf("┼");
            else if( Pan0415==1 ) printf("●");
            else if( Pan0415==2 ) printf("○");
            if( Pan0416==416 ) printf("┼");
            else if( Pan0416==1 ) printf("●");
            else if( Pan0416==2 ) printf("○");
            if( Pan0417==417 ) printf("┼");
            else if( Pan0417==1 ) printf("●");
            else if( Pan0417==2 ) printf("○");
            if( Pan0418==418 ) printf("┼");
            else if( Pan0418==1 ) printf("●");
            else if( Pan0418==2 ) printf("○");
            if( Pan0419==419 ) printf("┤\n");
            else if( Pan0419==1 ) printf("●\n");
            else if( Pan0419==2 ) printf("○\n");
            if( Pan0501==501 ) printf(" 5├");
            else if( Pan0501==1 ) printf("●");
            else if( Pan0501==2 ) printf("○");
            if( Pan0502==502 ) printf("┼");
            else if( Pan0502==1 ) printf("●");
            else if( Pan0502==2 ) printf("○");
            if( Pan0503==503 ) printf("┼");
            else if( Pan0503==1 ) printf("●");
            else if( Pan0503==2 ) printf("○");
            if( Pan0504==504 ) printf("┼");
            else if( Pan0504==1 ) printf("●");
            else if( Pan0504==2 ) printf("○");
            if( Pan0505==505 ) printf("┼");
            else if( Pan0505==1 ) printf("●");
            else if( Pan0505==2 ) printf("○");
            if( Pan0506==506 ) printf("┼");
            else if( Pan0506==1 ) printf("●");
            else if( Pan0506==2 ) printf("○");
            if( Pan0507==507 ) printf("┼");
            else if( Pan0507==1 ) printf("●");
            else if( Pan0507==2 ) printf("○");
            if( Pan0508==508 ) printf("┼");
            else if( Pan0508==1 ) printf("●");
            else if( Pan0508==2 ) printf("○");
            if( Pan0509==509 ) printf("┼");
            else if( Pan0509==1 ) printf("●");
            else if( Pan0509==2 ) printf("○");
            if( Pan0510==510 ) printf("┼");
            else if( Pan0510==1 ) printf("●");
            else if( Pan0510==2 ) printf("○");
            if( Pan0511==511 ) printf("┼");
            else if( Pan0511==1 ) printf("●");
            else if( Pan0511==2 ) printf("○");
            if( Pan0512==512 ) printf("┼");
            else if( Pan0512==1 ) printf("●");
            else if( Pan0512==2 ) printf("○");
            if( Pan0513==513 ) printf("┼");
            else if( Pan0513==1 ) printf("●");
            else if( Pan0513==2 ) printf("○");
            if( Pan0514==514 ) printf("┼");
            else if( Pan0514==1 ) printf("●");
            else if( Pan0514==2 ) printf("○");
            if( Pan0515==515 ) printf("┼");
            else if( Pan0515==1 ) printf("●");
            else if( Pan0515==2 ) printf("○");
            if( Pan0516==516 ) printf("┼");
            else if( Pan0516==1 ) printf("●");
            else if( Pan0516==2 ) printf("○");
            if( Pan0517==517 ) printf("┼");
            else if( Pan0517==1 ) printf("●");
            else if( Pan0517==2 ) printf("○");
            if( Pan0518==518 ) printf("┼");
            else if( Pan0518==1 ) printf("●");
            else if( Pan0518==2 ) printf("○");
            if( Pan0519==519 ) printf("┤\n");
            else if( Pan0519==1 ) printf("●\n");
            else if( Pan0519==2 ) printf("○\n");
            if( Pan0601==601 ) printf(" 6├");
            else if( Pan0601==1 ) printf("●");
            else if( Pan0601==2 ) printf("○");
            if( Pan0602==602 ) printf("┼");
            else if( Pan0602==1 ) printf("●");
            else if( Pan0602==2 ) printf("○");
            if( Pan0603==603 ) printf("┼");
            else if( Pan0603==1 ) printf("●");
            else if( Pan0603==2 ) printf("○");
            if( Pan0604==604 ) printf("┼");
            else if( Pan0604==1 ) printf("●");
            else if( Pan0604==2 ) printf("○");
            if( Pan0605==605 ) printf("┼");
            else if( Pan0605==1 ) printf("●");
            else if( Pan0605==2 ) printf("○");
            if( Pan0606==606 ) printf("┼");
            else if( Pan0606==1 ) printf("●");
            else if( Pan0606==2 ) printf("○");
            if( Pan0607==607 ) printf("┼");
            else if( Pan0607==1 ) printf("●");
            else if( Pan0607==2 ) printf("○");
            if( Pan0608==608 ) printf("┼");
            else if( Pan0608==1 ) printf("●");
            else if( Pan0608==2 ) printf("○");
            if( Pan0609==609 ) printf("┼");
            else if( Pan0609==1 ) printf("●");
            else if( Pan0609==2 ) printf("○");
            if( Pan0610==610 ) printf("┼");
            else if( Pan0610==1 ) printf("●");
            else if( Pan0610==2 ) printf("○");
            if( Pan0611==611 ) printf("┼");
            else if( Pan0611==1 ) printf("●");
            else if( Pan0611==2 ) printf("○");
            if( Pan0612==612 ) printf("┼");
            else if( Pan0612==1 ) printf("●");
            else if( Pan0612==2 ) printf("○");
            if( Pan0613==613 ) printf("┼");
            else if( Pan0613==1 ) printf("●");
            else if( Pan0613==2 ) printf("○");
            if( Pan0614==614 ) printf("┼");
            else if( Pan0614==1 ) printf("●");
            else if( Pan0614==2 ) printf("○");
            if( Pan0615==615 ) printf("┼");
            else if( Pan0615==1 ) printf("●");
            else if( Pan0615==2 ) printf("○");
            if( Pan0616==616 ) printf("┼");
            else if( Pan0616==1 ) printf("●");
            else if( Pan0616==2 ) printf("○");
            if( Pan0617==617 ) printf("┼");
            else if( Pan0617==1 ) printf("●");
            else if( Pan0617==2 ) printf("○");
            if( Pan0618==618 ) printf("┼");
            else if( Pan0618==1 ) printf("●");
            else if( Pan0618==2 ) printf("○");
            if( Pan0619==619 ) printf("┤\n");
            else if( Pan0619==1 ) printf("●\n");
            else if( Pan0619==2 ) printf("○\n");
            if( Pan0701==701 ) printf(" 7├");
            else if( Pan0701==1 ) printf("●");
            else if( Pan0701==2 ) printf("○");
            if( Pan0702==702 ) printf("┼");
            else if( Pan0702==1 ) printf("●");
            else if( Pan0702==2 ) printf("○");
            if( Pan0703==703 ) printf("┼");
            else if( Pan0703==1 ) printf("●");
            else if( Pan0703==2 ) printf("○");
            if( Pan0704==704 ) printf("┼");
            else if( Pan0704==1 ) printf("●");
            else if( Pan0704==2 ) printf("○");
            if( Pan0705==705 ) printf("┼");
            else if( Pan0705==1 ) printf("●");
            else if( Pan0705==2 ) printf("○");
            if( Pan0706==706 ) printf("┼");
            else if( Pan0706==1 ) printf("●");
            else if( Pan0706==2 ) printf("○");
            if( Pan0707==707 ) printf("┼");
            else if( Pan0707==1 ) printf("●");
            else if( Pan0707==2 ) printf("○");
            if( Pan0708==708 ) printf("┼");
            else if( Pan0708==1 ) printf("●");
            else if( Pan0708==2 ) printf("○");
            if( Pan0709==709 ) printf("┼");
            else if( Pan0709==1 ) printf("●");
            else if( Pan0709==2 ) printf("○");
            if( Pan0710==710 ) printf("┼");
            else if( Pan0710==1 ) printf("●");
            else if( Pan0710==2 ) printf("○");
            if( Pan0711==711 ) printf("┼");
            else if( Pan0711==1 ) printf("●");
            else if( Pan0711==2 ) printf("○");
            if( Pan0712==712 ) printf("┼");
            else if( Pan0712==1 ) printf("●");
            else if( Pan0712==2 ) printf("○");
            if( Pan0713==713 ) printf("┼");
            else if( Pan0713==1 ) printf("●");
            else if( Pan0713==2 ) printf("○");
            if( Pan0714==714 ) printf("┼");
            else if( Pan0714==1 ) printf("●");
            else if( Pan0714==2 ) printf("○");
            if( Pan0715==715 ) printf("┼");
            else if( Pan0715==1 ) printf("●");
            else if( Pan0715==2 ) printf("○");
            if( Pan0716==716 ) printf("┼");
            else if( Pan0716==1 ) printf("●");
            else if( Pan0716==2 ) printf("○");
            if( Pan0717==717 ) printf("┼");
            else if( Pan0717==1 ) printf("●");
            else if( Pan0717==2 ) printf("○");
            if( Pan0718==718 ) printf("┼");
            else if( Pan0718==1 ) printf("●");
            else if( Pan0718==2 ) printf("○");
            if( Pan0719==719 ) printf("┤\n");
            else if( Pan0719==1 ) printf("●\n");
            else if( Pan0719==2 ) printf("○\n");
            if( Pan0801==801 ) printf(" 8├");
            else if( Pan0801==1 ) printf("●");
            else if( Pan0801==2 ) printf("○");
            if( Pan0802==802 ) printf("┼");
            else if( Pan0802==1 ) printf("●");
            else if( Pan0802==2 ) printf("○");
            if( Pan0803==803 ) printf("┼");
            else if( Pan0803==1 ) printf("●");
            else if( Pan0803==2 ) printf("○");
            if( Pan0804==804 ) printf("┼");
            else if( Pan0804==1 ) printf("●");
            else if( Pan0804==2 ) printf("○");
            if( Pan0805==805 ) printf("┼");
            else if( Pan0805==1 ) printf("●");
            else if( Pan0805==2 ) printf("○");
            if( Pan0806==806 ) printf("┼");
            else if( Pan0806==1 ) printf("●");
            else if( Pan0806==2 ) printf("○");
            if( Pan0807==807 ) printf("┼");
            else if( Pan0807==1 ) printf("●");
            else if( Pan0807==2 ) printf("○");
            if( Pan0808==808 ) printf("┼");
            else if( Pan0808==1 ) printf("●");
            else if( Pan0808==2 ) printf("○");
            if( Pan0809==809 ) printf("┼");
            else if( Pan0809==1 ) printf("●");
            else if( Pan0809==2 ) printf("○");
            if( Pan0810==810 ) printf("┼");
            else if( Pan0810==1 ) printf("●");
            else if( Pan0810==2 ) printf("○");
            if( Pan0811==811 ) printf("┼");
            else if( Pan0811==1 ) printf("●");
            else if( Pan0811==2 ) printf("○");
            if( Pan0812==812 ) printf("┼");
            else if( Pan0812==1 ) printf("●");
            else if( Pan0812==2 ) printf("○");
            if( Pan0813==813 ) printf("┼");
            else if( Pan0813==1 ) printf("●");
            else if( Pan0813==2 ) printf("○");
            if( Pan0814==814 ) printf("┼");
            else if( Pan0814==1 ) printf("●");
            else if( Pan0814==2 ) printf("○");
            if( Pan0815==815 ) printf("┼");
            else if( Pan0815==1 ) printf("●");
            else if( Pan0815==2 ) printf("○");
            if( Pan0816==816 ) printf("┼");
            else if( Pan0816==1 ) printf("●");
            else if( Pan0816==2 ) printf("○");
            if( Pan0817==817 ) printf("┼");
            else if( Pan0817==1 ) printf("●");
            else if( Pan0817==2 ) printf("○");
            if( Pan0818==818 ) printf("┼");
            else if( Pan0818==1 ) printf("●");
            else if( Pan0818==2 ) printf("○");
            if( Pan0819==819 ) printf("┤\n");
            else if( Pan0819==1 ) printf("●\n");
            else if( Pan0819==2 ) printf("○\n");
            if( Pan0901==901 ) printf(" 9├");
            else if( Pan0901==1 ) printf("●");
            else if( Pan0901==2 ) printf("○");
            if( Pan0902==902 ) printf("┼");
            else if( Pan0902==1 ) printf("●");
            else if( Pan0902==2 ) printf("○");
            if( Pan0903==903 ) printf("┼");
            else if( Pan0903==1 ) printf("●");
            else if( Pan0903==2 ) printf("○");
            if( Pan0904==904 ) printf("┼");
            else if( Pan0904==1 ) printf("●");
            else if( Pan0904==2 ) printf("○");
            if( Pan0905==905 ) printf("┼");
            else if( Pan0905==1 ) printf("●");
            else if( Pan0905==2 ) printf("○");
            if( Pan0906==906 ) printf("┼");
            else if( Pan0906==1 ) printf("●");
            else if( Pan0906==2 ) printf("○");
            if( Pan0907==907 ) printf("┼");
            else if( Pan0907==1 ) printf("●");
            else if( Pan0907==2 ) printf("○");
            if( Pan0908==908 ) printf("┼");
            else if( Pan0908==1 ) printf("●");
            else if( Pan0908==2 ) printf("○");
            if( Pan0909==909 ) printf("┼");
            else if( Pan0909==1 ) printf("●");
            else if( Pan0909==2 ) printf("○");
            if( Pan0910==910 ) printf("┼");
            else if( Pan0910==1 ) printf("●");
            else if( Pan0910==2 ) printf("○");
            if( Pan0911==911 ) printf("┼");
            else if( Pan0911==1 ) printf("●");
            else if( Pan0911==2 ) printf("○");
            if( Pan0912==912 ) printf("┼");
            else if( Pan0912==1 ) printf("●");
            else if( Pan0912==2 ) printf("○");
            if( Pan0913==913 ) printf("┼");
            else if( Pan0913==1 ) printf("●");
            else if( Pan0913==2 ) printf("○");
            if( Pan0914==914 ) printf("┼");
            else if( Pan0914==1 ) printf("●");
            else if( Pan0914==2 ) printf("○");
            if( Pan0915==915 ) printf("┼");
            else if( Pan0915==1 ) printf("●");
            else if( Pan0915==2 ) printf("○");
            if( Pan0916==916 ) printf("┼");
            else if( Pan0916==1 ) printf("●");
            else if( Pan0916==2 ) printf("○");
            if( Pan0917==917 ) printf("┼");
            else if( Pan0917==1 ) printf("●");
            else if( Pan0917==2 ) printf("○");
            if( Pan0918==918 ) printf("┼");
            else if( Pan0918==1 ) printf("●");
            else if( Pan0918==2 ) printf("○");
            if( Pan0919==919 ) printf("┤\n");
            else if( Pan0919==1 ) printf("●\n");
            else if( Pan0919==2 ) printf("○\n");
            if( Pan1001==1001 ) printf("10├");
            else if( Pan1001==1 ) printf("●");
            else if( Pan1001==2 ) printf("○");
            if( Pan1002==1002 ) printf("┼");
            else if( Pan1002==1 ) printf("●");
            else if( Pan1002==2 ) printf("○");
            if( Pan1003==1003 ) printf("┼");
            else if( Pan1003==1 ) printf("●");
            else if( Pan1003==2 ) printf("○");
            if( Pan1004==1004 ) printf("┼");
            else if( Pan1004==1 ) printf("●");
            else if( Pan1004==2 ) printf("○");
            if( Pan1005==1005 ) printf("┼");
            else if( Pan1005==1 ) printf("●");
            else if( Pan1005==2 ) printf("○");
            if( Pan1006==1006 ) printf("┼");
            else if( Pan1006==1 ) printf("●");
            else if( Pan1006==2 ) printf("○");
            if( Pan1007==1007 ) printf("┼");
            else if( Pan1007==1 ) printf("●");
            else if( Pan1007==2 ) printf("○");
            if( Pan1008==1008 ) printf("┼");
            else if( Pan1008==1 ) printf("●");
            else if( Pan1008==2 ) printf("○");
            if( Pan1009==1009 ) printf("┼");
            else if( Pan1009==1 ) printf("●");
            else if( Pan1009==2 ) printf("○");
            if( Pan1010==1010 ) printf("┼");
            else if( Pan1010==1 ) printf("●");
            else if( Pan1010==2 ) printf("○");
            if( Pan1011==1011 ) printf("┼");
            else if( Pan1011==1 ) printf("●");
            else if( Pan1011==2 ) printf("○");
            if( Pan1012==1012 ) printf("┼");
            else if( Pan1012==1 ) printf("●");
            else if( Pan1012==2 ) printf("○");
            if( Pan1013==1013 ) printf("┼");
            else if( Pan1013==1 ) printf("●");
            else if( Pan1013==2 ) printf("○");
            if( Pan1014==1014 ) printf("┼");
            else if( Pan1014==1 ) printf("●");
            else if( Pan1014==2 ) printf("○");
            if( Pan1015==1015 ) printf("┼");
            else if( Pan1015==1 ) printf("●");
            else if( Pan1015==2 ) printf("○");
            if( Pan1016==1016 ) printf("┼");
            else if( Pan1016==1 ) printf("●");
            else if( Pan1016==2 ) printf("○");
            if( Pan1017==1017 ) printf("┼");
            else if( Pan1017==1 ) printf("●");
            else if( Pan1017==2 ) printf("○");
            if( Pan1018==1018 ) printf("┼");
            else if( Pan1018==1 ) printf("●");
            else if( Pan1018==2 ) printf("○");
            if( Pan1019==1019 ) printf("┤\n");
            else if( Pan1019==1 ) printf("●\n");
            else if( Pan1019==2 ) printf("○\n");
            if( Pan1101==1101 ) printf("11├");
            else if( Pan1101==1 ) printf("●");
            else if( Pan1101==2 ) printf("○");
            if( Pan1102==1102 ) printf("┼");
            else if( Pan1102==1 ) printf("●");
            else if( Pan1102==2 ) printf("○");
            if( Pan1103==1103 ) printf("┼");
            else if( Pan1103==1 ) printf("●");
            else if( Pan1103==2 ) printf("○");
            if( Pan1104==1104 ) printf("┼");
            else if( Pan1104==1 ) printf("●");
            else if( Pan1104==2 ) printf("○");
            if( Pan1105==1105 ) printf("┼");
            else if( Pan1105==1 ) printf("●");
            else if( Pan1105==2 ) printf("○");
            if( Pan1106==1106 ) printf("┼");
            else if( Pan1106==1 ) printf("●");
            else if( Pan1106==2 ) printf("○");
            if( Pan1107==1107 ) printf("┼");
            else if( Pan1107==1 ) printf("●");
            else if( Pan1107==2 ) printf("○");
            if( Pan1108==1108 ) printf("┼");
            else if( Pan1108==1 ) printf("●");
            else if( Pan1108==2 ) printf("○");
            if( Pan1109==1109 ) printf("┼");
            else if( Pan1109==1 ) printf("●");
            else if( Pan1109==2 ) printf("○");
            if( Pan1110==1110 ) printf("┼");
            else if( Pan1110==1 ) printf("●");
            else if( Pan1110==2 ) printf("○");
            if( Pan1111==1111 ) printf("┼");
            else if( Pan1111==1 ) printf("●");
            else if( Pan1111==2 ) printf("○");
            if( Pan1112==1112 ) printf("┼");
            else if( Pan1112==1 ) printf("●");
            else if( Pan1112==2 ) printf("○");
            if( Pan1113==1113 ) printf("┼");
            else if( Pan1113==1 ) printf("●");
            else if( Pan1113==2 ) printf("○");
            if( Pan1114==1114 ) printf("┼");
            else if( Pan1114==1 ) printf("●");
            else if( Pan1114==2 ) printf("○");
            if( Pan1115==1115 ) printf("┼");
            else if( Pan1115==1 ) printf("●");
            else if( Pan1115==2 ) printf("○");
            if( Pan1116==1116 ) printf("┼");
            else if( Pan1116==1 ) printf("●");
            else if( Pan1116==2 ) printf("○");
            if( Pan1117==1117 ) printf("┼");
            else if( Pan1117==1 ) printf("●");
            else if( Pan1117==2 ) printf("○");
            if( Pan1118==1118 ) printf("┼");
            else if( Pan1118==1 ) printf("●");
            else if( Pan1118==2 ) printf("○");
            if( Pan1119==1119 ) printf("┤\n");
            else if( Pan1119==1 ) printf("●\n");
            else if( Pan1119==2 ) printf("○\n");
            if( Pan1201==1201 ) printf("12├");
            else if( Pan1201==1 ) printf("●");
            else if( Pan1201==2 ) printf("○");
            if( Pan1202==1202 ) printf("┼");
            else if( Pan1202==1 ) printf("●");
            else if( Pan1202==2 ) printf("○");
            if( Pan1203==1203 ) printf("┼");
            else if( Pan1203==1 ) printf("●");
            else if( Pan1203==2 ) printf("○");
            if( Pan1204==1204 ) printf("┼");
            else if( Pan1204==1 ) printf("●");
            else if( Pan1204==2 ) printf("○");
            if( Pan1205==1205 ) printf("┼");
            else if( Pan1205==1 ) printf("●");
            else if( Pan1205==2 ) printf("○");
            if( Pan1206==1206 ) printf("┼");
            else if( Pan1206==1 ) printf("●");
            else if( Pan1206==2 ) printf("○");
            if( Pan1207==1207 ) printf("┼");
            else if( Pan1207==1 ) printf("●");
            else if( Pan1207==2 ) printf("○");
            if( Pan1208==1208 ) printf("┼");
            else if( Pan1208==1 ) printf("●");
            else if( Pan1208==2 ) printf("○");
            if( Pan1209==1209 ) printf("┼");
            else if( Pan1209==1 ) printf("●");
            else if( Pan1209==2 ) printf("○");
            if( Pan1210==1210 ) printf("┼");
            else if( Pan1210==1 ) printf("●");
            else if( Pan1210==2 ) printf("○");
            if( Pan1211==1211 ) printf("┼");
            else if( Pan1211==1 ) printf("●");
            else if( Pan1211==2 ) printf("○");
            if( Pan1212==1212 ) printf("┼");
            else if( Pan1212==1 ) printf("●");
            else if( Pan1212==2 ) printf("○");
            if( Pan1213==1213 ) printf("┼");
            else if( Pan1213==1 ) printf("●");
            else if( Pan1213==2 ) printf("○");
            if( Pan1214==1214 ) printf("┼");
            else if( Pan1214==1 ) printf("●");
            else if( Pan1214==2 ) printf("○");
            if( Pan1215==1215 ) printf("┼");
            else if( Pan1215==1 ) printf("●");
            else if( Pan1215==2 ) printf("○");
            if( Pan1216==1216 ) printf("┼");
            else if( Pan1216==1 ) printf("●");
            else if( Pan1216==2 ) printf("○");
            if( Pan1217==1217 ) printf("┼");
            else if( Pan1217==1 ) printf("●");
            else if( Pan1217==2 ) printf("○");
            if( Pan1218==1218 ) printf("┼");
            else if( Pan1218==1 ) printf("●");
            else if( Pan1218==2 ) printf("○");
            if( Pan1219==1219 ) printf("┤\n");
            else if( Pan1219==1 ) printf("●\n");
            else if( Pan1219==2 ) printf("○\n");
            if( Pan1301==1301 ) printf("13├");
            else if( Pan1301==1 ) printf("●");
            else if( Pan1301==2 ) printf("○");
            if( Pan1302==1302 ) printf("┼");
            else if( Pan1302==1 ) printf("●");
            else if( Pan1302==2 ) printf("○");
            if( Pan1303==1303 ) printf("┼");
            else if( Pan1303==1 ) printf("●");
            else if( Pan1303==2 ) printf("○");
            if( Pan1304==1304 ) printf("┼");
            else if( Pan1304==1 ) printf("●");
            else if( Pan1304==2 ) printf("○");
            if( Pan1305==1305 ) printf("┼");
            else if( Pan1305==1 ) printf("●");
            else if( Pan1305==2 ) printf("○");
            if( Pan1306==1306 ) printf("┼");
            else if( Pan1306==1 ) printf("●");
            else if( Pan1306==2 ) printf("○");
            if( Pan1307==1307 ) printf("┼");
            else if( Pan1307==1 ) printf("●");
            else if( Pan1307==2 ) printf("○");
            if( Pan1308==1308 ) printf("┼");
            else if( Pan1308==1 ) printf("●");
            else if( Pan1308==2 ) printf("○");
            if( Pan1309==1309 ) printf("┼");
            else if( Pan1309==1 ) printf("●");
            else if( Pan1309==2 ) printf("○");
            if( Pan1310==1310 ) printf("┼");
            else if( Pan1310==1 ) printf("●");
            else if( Pan1310==2 ) printf("○");
            if( Pan1311==1311 ) printf("┼");
            else if( Pan1311==1 ) printf("●");
            else if( Pan1311==2 ) printf("○");
            if( Pan1312==1312 ) printf("┼");
            else if( Pan1312==1 ) printf("●");
            else if( Pan1312==2 ) printf("○");
            if( Pan1313==1313 ) printf("┼");
            else if( Pan1313==1 ) printf("●");
            else if( Pan1313==2 ) printf("○");
            if( Pan1314==1314 ) printf("┼");
            else if( Pan1314==1 ) printf("●");
            else if( Pan1314==2 ) printf("○");
            if( Pan1315==1315 ) printf("┼");
            else if( Pan1315==1 ) printf("●");
            else if( Pan1315==2 ) printf("○");
            if( Pan1316==1316 ) printf("┼");
            else if( Pan1316==1 ) printf("●");
            else if( Pan1316==2 ) printf("○");
            if( Pan1317==1317 ) printf("┼");
            else if( Pan1317==1 ) printf("●");
            else if( Pan1317==2 ) printf("○");
            if( Pan1318==1318 ) printf("┼");
            else if( Pan1318==1 ) printf("●");
            else if( Pan1318==2 ) printf("○");
            if( Pan1319==1319 ) printf("┤\n");
            else if( Pan1319==1 ) printf("●\n");
            else if( Pan1319==2 ) printf("○\n");
            if( Pan1401==1401 ) printf("14├");
            else if( Pan1401==1 ) printf("●");
            else if( Pan1401==2 ) printf("○");
            if( Pan1402==1402 ) printf("┼");
            else if( Pan1402==1 ) printf("●");
            else if( Pan1402==2 ) printf("○");
            if( Pan1403==1403 ) printf("┼");
            else if( Pan1403==1 ) printf("●");
            else if( Pan1403==2 ) printf("○");
            if( Pan1404==1404 ) printf("┼");
            else if( Pan1404==1 ) printf("●");
            else if( Pan1404==2 ) printf("○");
            if( Pan1405==1405 ) printf("┼");
            else if( Pan1405==1 ) printf("●");
            else if( Pan1405==2 ) printf("○");
            if( Pan1406==1406 ) printf("┼");
            else if( Pan1406==1 ) printf("●");
            else if( Pan1406==2 ) printf("○");
            if( Pan1407==1407 ) printf("┼");
            else if( Pan1407==1 ) printf("●");
            else if( Pan1407==2 ) printf("○");
            if( Pan1408==1408 ) printf("┼");
            else if( Pan1408==1 ) printf("●");
            else if( Pan1408==2 ) printf("○");
            if( Pan1409==1409 ) printf("┼");
            else if( Pan1409==1 ) printf("●");
            else if( Pan1409==2 ) printf("○");
            if( Pan1410==1410 ) printf("┼");
            else if( Pan1410==1 ) printf("●");
            else if( Pan1410==2 ) printf("○");
            if( Pan1411==1411 ) printf("┼");
            else if( Pan1411==1 ) printf("●");
            else if( Pan1411==2 ) printf("○");
            if( Pan1412==1412 ) printf("┼");
            else if( Pan1412==1 ) printf("●");
            else if( Pan1412==2 ) printf("○");
            if( Pan1413==1413 ) printf("┼");
            else if( Pan1413==1 ) printf("●");
            else if( Pan1413==2 ) printf("○");
            if( Pan1414==1414 ) printf("┼");
            else if( Pan1414==1 ) printf("●");
            else if( Pan1414==2 ) printf("○");
            if( Pan1415==1415 ) printf("┼");
            else if( Pan1415==1 ) printf("●");
            else if( Pan1415==2 ) printf("○");
            if( Pan1416==1416 ) printf("┼");
            else if( Pan1416==1 ) printf("●");
            else if( Pan1416==2 ) printf("○");
            if( Pan1417==1417 ) printf("┼");
            else if( Pan1417==1 ) printf("●");
            else if( Pan1417==2 ) printf("○");
            if( Pan1418==1418 ) printf("┼");
            else if( Pan1418==1 ) printf("●");
            else if( Pan1418==2 ) printf("○");
            if( Pan1419==1419 ) printf("┤\n");
            else if( Pan1419==1 ) printf("●\n");
            else if( Pan1419==2 ) printf("○\n");
            if( Pan1501==1501 ) printf("15├");
            else if( Pan1501==1 ) printf("●");
            else if( Pan1501==2 ) printf("○");
            if( Pan1502==1502 ) printf("┼");
            else if( Pan1502==1 ) printf("●");
            else if( Pan1502==2 ) printf("○");
            if( Pan1503==1503 ) printf("┼");
            else if( Pan1503==1 ) printf("●");
            else if( Pan1503==2 ) printf("○");
            if( Pan1504==1504 ) printf("┼");
            else if( Pan1504==1 ) printf("●");
            else if( Pan1504==2 ) printf("○");
            if( Pan1505==1505 ) printf("┼");
            else if( Pan1505==1 ) printf("●");
            else if( Pan1505==2 ) printf("○");
            if( Pan1506==1506 ) printf("┼");
            else if( Pan1506==1 ) printf("●");
            else if( Pan1506==2 ) printf("○");
            if( Pan1507==1507 ) printf("┼");
            else if( Pan1507==1 ) printf("●");
            else if( Pan1507==2 ) printf("○");
            if( Pan1508==1508 ) printf("┼");
            else if( Pan1508==1 ) printf("●");
            else if( Pan1508==2 ) printf("○");
            if( Pan1509==1509 ) printf("┼");
            else if( Pan1509==1 ) printf("●");
            else if( Pan1509==2 ) printf("○");
            if( Pan1510==1510 ) printf("┼");
            else if( Pan1510==1 ) printf("●");
            else if( Pan1510==2 ) printf("○");
            if( Pan1511==1511 ) printf("┼");
            else if( Pan1511==1 ) printf("●");
            else if( Pan1511==2 ) printf("○");
            if( Pan1512==1512 ) printf("┼");
            else if( Pan1512==1 ) printf("●");
            else if( Pan1512==2 ) printf("○");
            if( Pan1513==1513 ) printf("┼");
            else if( Pan1513==1 ) printf("●");
            else if( Pan1513==2 ) printf("○");
            if( Pan1514==1514 ) printf("┼");
            else if( Pan1514==1 ) printf("●");
            else if( Pan1514==2 ) printf("○");
            if( Pan1515==1515 ) printf("┼");
            else if( Pan1515==1 ) printf("●");
            else if( Pan1515==2 ) printf("○");
            if( Pan1516==1516 ) printf("┼");
            else if( Pan1516==1 ) printf("●");
            else if( Pan1516==2 ) printf("○");
            if( Pan1517==1517 ) printf("┼");
            else if( Pan1517==1 ) printf("●");
            else if( Pan1517==2 ) printf("○");
            if( Pan1518==1518 ) printf("┼");
            else if( Pan1518==1 ) printf("●");
            else if( Pan1518==2 ) printf("○");
            if( Pan1519==1519 ) printf("┤\n");
            else if( Pan1519==1 ) printf("●\n");
            else if( Pan1519==2 ) printf("○\n");
            if( Pan1601==1601 ) printf("16├");
            else if( Pan1601==1 ) printf("●");
            else if( Pan1601==2 ) printf("○");
            if( Pan1602==1602 ) printf("┼");
            else if( Pan1602==1 ) printf("●");
            else if( Pan1602==2 ) printf("○");
            if( Pan1603==1603 ) printf("┼");
            else if( Pan1603==1 ) printf("●");
            else if( Pan1603==2 ) printf("○");
            if( Pan1604==1604 ) printf("┼");
            else if( Pan1604==1 ) printf("●");
            else if( Pan1604==2 ) printf("○");
            if( Pan1605==1605 ) printf("┼");
            else if( Pan1605==1 ) printf("●");
            else if( Pan1605==2 ) printf("○");
            if( Pan1606==1606 ) printf("┼");
            else if( Pan1606==1 ) printf("●");
            else if( Pan1606==2 ) printf("○");
            if( Pan1607==1607 ) printf("┼");
            else if( Pan1607==1 ) printf("●");
            else if( Pan1607==2 ) printf("○");
            if( Pan1608==1608 ) printf("┼");
            else if( Pan1608==1 ) printf("●");
            else if( Pan1608==2 ) printf("○");
            if( Pan1609==1609 ) printf("┼");
            else if( Pan1609==1 ) printf("●");
            else if( Pan1609==2 ) printf("○");
            if( Pan1610==1610 ) printf("┼");
            else if( Pan1610==1 ) printf("●");
            else if( Pan1610==2 ) printf("○");
            if( Pan1611==1611 ) printf("┼");
            else if( Pan1611==1 ) printf("●");
            else if( Pan1611==2 ) printf("○");
            if( Pan1612==1612 ) printf("┼");
            else if( Pan1612==1 ) printf("●");
            else if( Pan1612==2 ) printf("○");
            if( Pan1613==1613 ) printf("┼");
            else if( Pan1613==1 ) printf("●");
            else if( Pan1613==2 ) printf("○");
            if( Pan1614==1614 ) printf("┼");
            else if( Pan1614==1 ) printf("●");
            else if( Pan1614==2 ) printf("○");
            if( Pan1615==1615 ) printf("┼");
            else if( Pan1615==1 ) printf("●");
            else if( Pan1615==2 ) printf("○");
            if( Pan1616==1616 ) printf("┼");
            else if( Pan1616==1 ) printf("●");
            else if( Pan1616==2 ) printf("○");
            if( Pan1617==1617 ) printf("┼");
            else if( Pan1617==1 ) printf("●");
            else if( Pan1617==2 ) printf("○");
            if( Pan1618==1618 ) printf("┼");
            else if( Pan1618==1 ) printf("●");
            else if( Pan1618==2 ) printf("○");
            if( Pan1619==1619 ) printf("┤\n");
            else if( Pan1619==1 ) printf("●\n");
            else if( Pan1619==2 ) printf("○\n");
            if( Pan1701==1701 ) printf("17├");
            else if( Pan1701==1 ) printf("●");
            else if( Pan1701==2 ) printf("○");
            if( Pan1702==1702 ) printf("┼");
            else if( Pan1702==1 ) printf("●");
            else if( Pan1702==2 ) printf("○");
            if( Pan1703==1703 ) printf("┼");
            else if( Pan1703==1 ) printf("●");
            else if( Pan1703==2 ) printf("○");
            if( Pan1704==1704 ) printf("┼");
            else if( Pan1704==1 ) printf("●");
            else if( Pan1704==2 ) printf("○");
            if( Pan1705==1705 ) printf("┼");
            else if( Pan1705==1 ) printf("●");
            else if( Pan1705==2 ) printf("○");
            if( Pan1706==1706 ) printf("┼");
            else if( Pan1706==1 ) printf("●");
            else if( Pan1706==2 ) printf("○");
            if( Pan1707==1707 ) printf("┼");
            else if( Pan1707==1 ) printf("●");
            else if( Pan1707==2 ) printf("○");
            if( Pan1708==1708 ) printf("┼");
            else if( Pan1708==1 ) printf("●");
            else if( Pan1708==2 ) printf("○");
            if( Pan1709==1709 ) printf("┼");
            else if( Pan1709==1 ) printf("●");
            else if( Pan1709==2 ) printf("○");
            if( Pan1710==1710 ) printf("┼");
            else if( Pan1710==1 ) printf("●");
            else if( Pan1710==2 ) printf("○");
            if( Pan1711==1711 ) printf("┼");
            else if( Pan1711==1 ) printf("●");
            else if( Pan1711==2 ) printf("○");
            if( Pan1712==1712 ) printf("┼");
            else if( Pan1712==1 ) printf("●");
            else if( Pan1712==2 ) printf("○");
            if( Pan1713==1713 ) printf("┼");
            else if( Pan1713==1 ) printf("●");
            else if( Pan1713==2 ) printf("○");
            if( Pan1714==1714 ) printf("┼");
            else if( Pan1714==1 ) printf("●");
            else if( Pan1714==2 ) printf("○");
            if( Pan1715==1715 ) printf("┼");
            else if( Pan1715==1 ) printf("●");
            else if( Pan1715==2 ) printf("○");
            if( Pan1716==1716 ) printf("┼");
            else if( Pan1716==1 ) printf("●");
            else if( Pan1716==2 ) printf("○");
            if( Pan1717==1717 ) printf("┼");
            else if( Pan1717==1 ) printf("●");
            else if( Pan1717==2 ) printf("○");
            if( Pan1718==1718 ) printf("┼");
            else if( Pan1718==1 ) printf("●");
            else if( Pan1718==2 ) printf("○");
            if( Pan1719==1719 ) printf("┤\n");
            else if( Pan1719==1 ) printf("●\n");
            else if( Pan1719==2 ) printf("○\n");
            if( Pan1801==1801 ) printf("18├");
            else if( Pan1801==1 ) printf("●");
            else if( Pan1801==2 ) printf("○");
            if( Pan1802==1802 ) printf("┼");
            else if( Pan1802==1 ) printf("●");
            else if( Pan1802==2 ) printf("○");
            if( Pan1803==1803 ) printf("┼");
            else if( Pan1803==1 ) printf("●");
            else if( Pan1803==2 ) printf("○");
            if( Pan1804==1804 ) printf("┼");
            else if( Pan1804==1 ) printf("●");
            else if( Pan1804==2 ) printf("○");
            if( Pan1805==1805 ) printf("┼");
            else if( Pan1805==1 ) printf("●");
            else if( Pan1805==2 ) printf("○");
            if( Pan1806==1806 ) printf("┼");
            else if( Pan1806==1 ) printf("●");
            else if( Pan1806==2 ) printf("○");
            if( Pan1807==1807 ) printf("┼");
            else if( Pan1807==1 ) printf("●");
            else if( Pan1807==2 ) printf("○");
            if( Pan1808==1808 ) printf("┼");
            else if( Pan1808==1 ) printf("●");
            else if( Pan1808==2 ) printf("○");
            if( Pan1809==1809 ) printf("┼");
            else if( Pan1809==1 ) printf("●");
            else if( Pan1809==2 ) printf("○");
            if( Pan1810==1810 ) printf("┼");
            else if( Pan1810==1 ) printf("●");
            else if( Pan1810==2 ) printf("○");
            if( Pan1811==1811 ) printf("┼");
            else if( Pan1811==1 ) printf("●");
            else if( Pan1811==2 ) printf("○");
            if( Pan1812==1812 ) printf("┼");
            else if( Pan1812==1 ) printf("●");
            else if( Pan1812==2 ) printf("○");
            if( Pan1813==1813 ) printf("┼");
            else if( Pan1813==1 ) printf("●");
            else if( Pan1813==2 ) printf("○");
            if( Pan1814==1814 ) printf("┼");
            else if( Pan1814==1 ) printf("●");
            else if( Pan1814==2 ) printf("○");
            if( Pan1815==1815 ) printf("┼");
            else if( Pan1815==1 ) printf("●");
            else if( Pan1815==2 ) printf("○");
            if( Pan1816==1816 ) printf("┼");
            else if( Pan1816==1 ) printf("●");
            else if( Pan1816==2 ) printf("○");
            if( Pan1817==1817 ) printf("┼");
            else if( Pan1817==1 ) printf("●");
            else if( Pan1817==2 ) printf("○");
            if( Pan1818==1818 ) printf("┼");
            else if( Pan1818==1 ) printf("●");
            else if( Pan1818==2 ) printf("○");
            if( Pan1819==1819 ) printf("┤\n");
            else if( Pan1819==1 ) printf("●\n");
            else if( Pan1819==2 ) printf("○\n");
            if( Pan1901==1901 ) printf("19└");
            else if( Pan1901==1 ) printf("●");
            else if( Pan1901==2 ) printf("○");
            if( Pan1902==1902 ) printf("┴");
            else if( Pan1902==1 ) printf("●");
            else if( Pan1902==2 ) printf("○");
            if( Pan1903==1903 ) printf("┴");
            else if( Pan1903==1 ) printf("●");
            else if( Pan1903==2 ) printf("○");
            if( Pan1904==1904 ) printf("┴");
            else if( Pan1904==1 ) printf("●");
            else if( Pan1904==2 ) printf("○");
            if( Pan1905==1905 ) printf("┴");
            else if( Pan1905==1 ) printf("●");
            else if( Pan1905==2 ) printf("○");
            if( Pan1906==1906 ) printf("┴");
            else if( Pan1906==1 ) printf("●");
            else if( Pan1906==2 ) printf("○");
            if( Pan1907==1907 ) printf("┴");
            else if( Pan1907==1 ) printf("●");
            else if( Pan1907==2 ) printf("○");
            if( Pan1908==1908 ) printf("┴");
            else if( Pan1908==1 ) printf("●");
            else if( Pan1908==2 ) printf("○");
            if( Pan1909==1909 ) printf("┴");
            else if( Pan1909==1 ) printf("●");
            else if( Pan1909==2 ) printf("○");
            if( Pan1910==1910 ) printf("┴");
            else if( Pan1910==1 ) printf("●");
            else if( Pan1910==2 ) printf("○");
            if( Pan1911==1911 ) printf("┴");
            else if( Pan1911==1 ) printf("●");
            else if( Pan1911==2 ) printf("○");
            if( Pan1912==1912 ) printf("┴");
            else if( Pan1912==1 ) printf("●");
            else if( Pan1912==2 ) printf("○");
            if( Pan1913==1913 ) printf("┴");
            else if( Pan1913==1 ) printf("●");
            else if( Pan1913==2 ) printf("○");
            if( Pan1914==1914 ) printf("┴");
            else if( Pan1914==1 ) printf("●");
            else if( Pan1914==2 ) printf("○");
            if( Pan1915==1915 ) printf("┴");
            else if( Pan1915==1 ) printf("●");
            else if( Pan1915==2 ) printf("○");
            if( Pan1916==1916 ) printf("┴");
            else if( Pan1916==1 ) printf("●");
            else if( Pan1916==2 ) printf("○");
            if( Pan1917==1917 ) printf("┴");
            else if( Pan1917==1 ) printf("●");
            else if( Pan1917==2 ) printf("○");
            if( Pan1918==1918 ) printf("┴");
            else if( Pan1918==1 ) printf("●");
            else if( Pan1918==2 ) printf("○");
            if( Pan1919==1919 ) printf("┘\n");
            else if( Pan1919==1 ) printf("●\n");
            else if( Pan1919==2 ) printf("○\n");
            printf("   1 2 3 4 5 6 7 8 910111213141516171819\n");
            printf("\n");

            if(win==1)                        // 승리
            {
                printf("\n\n\n다음으로 가실려면 엔터를 눌러주세요.");
                fflush(stdin);
                scanf("%c", &temp1);
                if(turn==1)
                    turn=2;
                else
                    turn=1;
                if(turn==1)
                {
                    BWEB=0;
                    WWEB++;        
                    printf("\n\n\n\t\t\t승리 :  백돌 ,   %d 연승 \n\n\n\n\n\n\n\n\n\n\n", WWEB);
                }
                else
                {
                    WWEB=0;
                    BWEB++;
                    printf("\n\n\n\t\t\t승리 :  흑돌 ,   %d 연승 \n\n\n\n\n\n\n\n\n\n\n", BWEB);
                }
                printf("\n\n\n다음으로 가실려면 엔터를 눌러주세요.");
                fflush(stdin);
                scanf("%c", &temp1);
                printf("\n\n\n\n\n\n");
                break;
            }
            fflush(stdin);
            printf("좌표를 입력해 주세요. : ");
            scanf("%d", &xy);    //좌표를 입력 받는다. (단. xy값을 붙여서)
            printf("\n");

            if(!(xy==9999) && (xy<101 || (xy>119 && xy<201) || (xy>219 && xy<301) || (xy>319 && xy<401) || (xy>419 && xy<501) || (xy>519 && xy<601) || (xy>619 && xy<701) || (xy>719 && xy<801) || (xy>819 && xy<901) || (xy>919 && xy<1001) || (xy>1019 && xy<1101) || (xy>1119 && xy<1201) || (xy>1219 && xy<1301) || (xy>1319 && xy<1401) || (xy>1419 && xy<1501) || (xy>1519 && xy<1601) || (xy>1619 && xy<1701) || (xy>1719 && xy<1801) || (xy>1819 && xy<1901) || xy>1919))
                printf("입력할 수 있는 좌표값을 넘었습니다.");

            else
            {        // 바둑판에 돌을 둔다.
                if( Pan0101==xy )
                    Pan0101=turn;
                else if( Pan0102==xy )
                    Pan0102=turn;
                else if( Pan0103==xy )
                    Pan0103=turn;
                else if( Pan0104==xy )
                    Pan0104=turn;
                else if( Pan0105==xy )
                    Pan0105=turn;
                else if( Pan0106==xy )
                    Pan0106=turn;
                else if( Pan0107==xy )
                    Pan0107=turn;
                else if( Pan0108==xy )
                    Pan0108=turn;
                else if( Pan0109==xy )
                    Pan0109=turn;
                else if( Pan0110==xy )
                    Pan0110=turn;
                else if( Pan0111==xy )
                    Pan0111=turn;
                else if( Pan0112==xy )
                    Pan0112=turn;
                else if( Pan0113==xy )
                    Pan0113=turn;
                else if( Pan0114==xy )
                    Pan0114=turn;
                else if( Pan0115==xy )
                    Pan0115=turn;
                else if( Pan0116==xy )
                    Pan0116=turn;
                else if( Pan0117==xy )
                    Pan0117=turn;
                else if( Pan0118==xy )
                    Pan0118=turn;
                else if( Pan0119==xy )
                    Pan0119=turn;
                else if( Pan0201==xy )
                    Pan0201=turn;
                else if( Pan0202==xy )
                    Pan0202=turn;
                else if( Pan0203==xy )
                    Pan0203=turn;
                else if( Pan0204==xy )
                    Pan0204=turn;
                else if( Pan0205==xy )
                    Pan0205=turn;
                else if( Pan0206==xy )
                    Pan0206=turn;
                else if( Pan0207==xy )
                    Pan0207=turn;
                else if( Pan0208==xy )
                    Pan0208=turn;
                else if( Pan0209==xy )
                    Pan0209=turn;
                else if( Pan0210==xy )
                    Pan0210=turn;
                else if( Pan0211==xy )
                    Pan0211=turn;
                else if( Pan0212==xy )
                    Pan0212=turn;
                else if( Pan0213==xy )
                    Pan0213=turn;
                else if( Pan0214==xy )
                    Pan0214=turn;
                else if( Pan0215==xy )
                    Pan0215=turn;
                else if( Pan0216==xy )
                    Pan0216=turn;
                else if( Pan0217==xy )
                    Pan0217=turn;
                else if( Pan0218==xy )
                    Pan0218=turn;
                else if( Pan0219==xy )
                    Pan0219=turn;
                else if( Pan0301==xy )
                    Pan0301=turn;
                else if( Pan0302==xy )
                    Pan0302=turn;
                else if( Pan0303==xy )
                    Pan0303=turn;
                else if( Pan0304==xy )
                    Pan0304=turn;
                else if( Pan0305==xy )
                    Pan0305=turn;
                else if( Pan0306==xy )
                    Pan0306=turn;
                else if( Pan0307==xy )
                    Pan0307=turn;
                else if( Pan0308==xy )
                    Pan0308=turn;
                else if( Pan0309==xy )
                    Pan0309=turn;
                else if( Pan0310==xy )
                    Pan0310=turn;
                else if( Pan0311==xy )
                    Pan0311=turn;
                else if( Pan0312==xy )
                    Pan0312=turn;
                else if( Pan0313==xy )
                    Pan0313=turn;
                else if( Pan0314==xy )
                    Pan0314=turn;
                else if( Pan0315==xy )
                    Pan0315=turn;
                else if( Pan0316==xy )
                    Pan0316=turn;
                else if( Pan0317==xy )
                    Pan0317=turn;
                else if( Pan0318==xy )
                    Pan0318=turn;
                else if( Pan0319==xy )
                    Pan0319=turn;
                else if( Pan0401==xy )
                    Pan0401=turn;
                else if( Pan0402==xy )
                    Pan0402=turn;
                else if( Pan0403==xy )
                    Pan0403=turn;
                else if( Pan0404==xy )
                    Pan0404=turn;
                else if( Pan0405==xy )
                    Pan0405=turn;
                else if( Pan0406==xy )
                    Pan0406=turn;
                else if( Pan0407==xy )
                    Pan0407=turn;
                else if( Pan0408==xy )
                    Pan0408=turn;
                else if( Pan0409==xy )
                    Pan0409=turn;
                else if( Pan0410==xy )
                    Pan0410=turn;
                else if( Pan0411==xy )
                    Pan0411=turn;
                else if( Pan0412==xy )
                    Pan0412=turn;
                else if( Pan0413==xy )
                    Pan0413=turn;
                else if( Pan0414==xy )
                    Pan0414=turn;
                else if( Pan0415==xy )
                    Pan0415=turn;
                else if( Pan0416==xy )
                    Pan0416=turn;
                else if( Pan0417==xy )
                    Pan0417=turn;
                else if( Pan0418==xy )
                    Pan0418=turn;
                else if( Pan0419==xy )
                    Pan0419=turn;
                else if( Pan0501==xy )
                    Pan0501=turn;
                else if( Pan0502==xy )
                    Pan0502=turn;
                else if( Pan0503==xy )
                    Pan0503=turn;
                else if( Pan0504==xy )
                    Pan0504=turn;
                else if( Pan0505==xy )
                    Pan0505=turn;
                else if( Pan0506==xy )
                    Pan0506=turn;
                else if( Pan0507==xy )
                    Pan0507=turn;
                else if( Pan0508==xy )
                    Pan0508=turn;
                else if( Pan0509==xy )
                    Pan0509=turn;
                else if( Pan0510==xy )
                    Pan0510=turn;
                else if( Pan0511==xy )
                    Pan0511=turn;
                else if( Pan0512==xy )
                    Pan0512=turn;
                else if( Pan0513==xy )
                    Pan0513=turn;
                else if( Pan0514==xy )
                    Pan0514=turn;
                else if( Pan0515==xy )
                    Pan0515=turn;
                else if( Pan0516==xy )
                    Pan0516=turn;
                else if( Pan0517==xy )
                    Pan0517=turn;
                else if( Pan0518==xy )
                    Pan0518=turn;
                else if( Pan0519==xy )
                    Pan0519=turn;
                else if( Pan0601==xy )
                    Pan0601=turn;
                else if( Pan0602==xy )
                    Pan0602=turn;
                else if( Pan0603==xy )
                    Pan0603=turn;
                else if( Pan0604==xy )
                    Pan0604=turn;
                else if( Pan0605==xy )
                    Pan0605=turn;
                else if( Pan0606==xy )
                    Pan0606=turn;
                else if( Pan0607==xy )
                    Pan0607=turn;
                else if( Pan0608==xy )
                    Pan0608=turn;
                else if( Pan0609==xy )
                    Pan0609=turn;
                else if( Pan0610==xy )
                    Pan0610=turn;
                else if( Pan0611==xy )
                    Pan0611=turn;
                else if( Pan0612==xy )
                    Pan0612=turn;
                else if( Pan0613==xy )
                    Pan0613=turn;
                else if( Pan0614==xy )
                    Pan0614=turn;
                else if( Pan0615==xy )
                    Pan0615=turn;
                else if( Pan0616==xy )
                    Pan0616=turn;
                else if( Pan0617==xy )
                    Pan0617=turn;
                else if( Pan0618==xy )
                    Pan0618=turn;
                else if( Pan0619==xy )
                    Pan0619=turn;
                else if( Pan0701==xy )
                    Pan0701=turn;
                else if( Pan0702==xy )
                    Pan0702=turn;
                else if( Pan0703==xy )
                    Pan0703=turn;
                else if( Pan0704==xy )
                    Pan0704=turn;
                else if( Pan0705==xy )
                    Pan0705=turn;
                else if( Pan0706==xy )
                    Pan0706=turn;
                else if( Pan0707==xy )
                    Pan0707=turn;
                else if( Pan0708==xy )
                    Pan0708=turn;
                else if( Pan0709==xy )
                    Pan0709=turn;
                else if( Pan0710==xy )
                    Pan0710=turn;
                else if( Pan0711==xy )
                    Pan0711=turn;
                else if( Pan0712==xy )
                    Pan0712=turn;
                else if( Pan0713==xy )
                    Pan0713=turn;
                else if( Pan0714==xy )
                    Pan0714=turn;
                else if( Pan0715==xy )
                    Pan0715=turn;
                else if( Pan0716==xy )
                    Pan0716=turn;
                else if( Pan0717==xy )
                    Pan0717=turn;
                else if( Pan0718==xy )
                    Pan0718=turn;
                else if( Pan0719==xy )
                    Pan0719=turn;
                else if( Pan0801==xy )
                    Pan0801=turn;
                else if( Pan0802==xy )
                    Pan0802=turn;
                else if( Pan0803==xy )
                    Pan0803=turn;
                else if( Pan0804==xy )
                    Pan0804=turn;
                else if( Pan0805==xy )
                    Pan0805=turn;
                else if( Pan0806==xy )
                    Pan0806=turn;
                else if( Pan0807==xy )
                    Pan0807=turn;
                else if( Pan0808==xy )
                    Pan0808=turn;
                else if( Pan0809==xy )
                    Pan0809=turn;
                else if( Pan0810==xy )
                    Pan0810=turn;
                else if( Pan0811==xy )
                    Pan0811=turn;
                else if( Pan0812==xy )
                    Pan0812=turn;
                else if( Pan0813==xy )
                    Pan0813=turn;
                else if( Pan0814==xy )
                    Pan0814=turn;
                else if( Pan0815==xy )
                    Pan0815=turn;
                else if( Pan0816==xy )
                    Pan0816=turn;
                else if( Pan0817==xy )
                    Pan0817=turn;
                else if( Pan0818==xy )
                    Pan0818=turn;
                else if( Pan0819==xy )
                    Pan0819=turn;
                else if( Pan0901==xy )
                    Pan0901=turn;
                else if( Pan0902==xy )
                    Pan0902=turn;
                else if( Pan0903==xy )
                    Pan0903=turn;
                else if( Pan0904==xy )
                    Pan0904=turn;
                else if( Pan0905==xy )
                    Pan0905=turn;
                else if( Pan0906==xy )
                    Pan0906=turn;
                else if( Pan0907==xy )
                    Pan0907=turn;
                else if( Pan0908==xy )
                    Pan0908=turn;
                else if( Pan0909==xy )
                    Pan0909=turn;
                else if( Pan0910==xy )
                    Pan0910=turn;
                else if( Pan0911==xy )
                    Pan0911=turn;
                else if( Pan0912==xy )
                    Pan0912=turn;
                else if( Pan0913==xy )
                    Pan0913=turn;
                else if( Pan0914==xy )
                    Pan0914=turn;
                else if( Pan0915==xy )
                    Pan0915=turn;
                else if( Pan0916==xy )
                    Pan0916=turn;
                else if( Pan0917==xy )
                    Pan0917=turn;
                else if( Pan0918==xy )
                    Pan0918=turn;
                else if( Pan0919==xy )
                    Pan0919=turn;
                else if( Pan1001==xy )
                    Pan1001=turn;
                else if( Pan1002==xy )
                    Pan1002=turn;
                else if( Pan1003==xy )
                    Pan1003=turn;
                else if( Pan1004==xy )
                    Pan1004=turn;
                else if( Pan1005==xy )
                    Pan1005=turn;
                else if( Pan1006==xy )
                    Pan1006=turn;
                else if( Pan1007==xy )
                    Pan1007=turn;
                else if( Pan1008==xy )
                    Pan1008=turn;
                else if( Pan1009==xy )
                    Pan1009=turn;
                else if( Pan1010==xy )
                    Pan1010=turn;
                else if( Pan1011==xy )
                    Pan1011=turn;
                else if( Pan1012==xy )
                    Pan1012=turn;
                else if( Pan1013==xy )
                    Pan1013=turn;
                else if( Pan1014==xy )
                    Pan1014=turn;
                else if( Pan1015==xy )
                    Pan1015=turn;
                else if( Pan1016==xy )
                    Pan1016=turn;
                else if( Pan1017==xy )
                    Pan1017=turn;
                else if( Pan1018==xy )
                    Pan1018=turn;
                else if( Pan1019==xy )
                    Pan1019=turn;
                else if( Pan1101==xy )
                    Pan1101=turn;
                else if( Pan1102==xy )
                    Pan1102=turn;
                else if( Pan1103==xy )
                    Pan1103=turn;
                else if( Pan1104==xy )
                    Pan1104=turn;
                else if( Pan1105==xy )
                    Pan1105=turn;
                else if( Pan1106==xy )
                    Pan1106=turn;
                else if( Pan1107==xy )
                    Pan1107=turn;
                else if( Pan1108==xy )
                    Pan1108=turn;
                else if( Pan1109==xy )
                    Pan1109=turn;
                else if( Pan1110==xy )
                    Pan1110=turn;
                else if( Pan1111==xy )
                    Pan1111=turn;
                else if( Pan1112==xy )
                    Pan1112=turn;
                else if( Pan1113==xy )
                    Pan1113=turn;
                else if( Pan1114==xy )
                    Pan1114=turn;
                else if( Pan1115==xy )
                    Pan1115=turn;
                else if( Pan1116==xy )
                    Pan1116=turn;
                else if( Pan1117==xy )
                    Pan1117=turn;
                else if( Pan1118==xy )
                    Pan1118=turn;
                else if( Pan1119==xy )
                    Pan1119=turn;
                else if( Pan1201==xy )
                    Pan1201=turn;
                else if( Pan1202==xy )
                    Pan1202=turn;
                else if( Pan1203==xy )
                    Pan1203=turn;
                else if( Pan1204==xy )
                    Pan1204=turn;
                else if( Pan1205==xy )
                    Pan1205=turn;
                else if( Pan1206==xy )
                    Pan1206=turn;
                else if( Pan1207==xy )
                    Pan1207=turn;
                else if( Pan1208==xy )
                    Pan1208=turn;
                else if( Pan1209==xy )
                    Pan1209=turn;
                else if( Pan1210==xy )
                    Pan1210=turn;
                else if( Pan1211==xy )
                    Pan1211=turn;
                else if( Pan1212==xy )
                    Pan1212=turn;
                else if( Pan1213==xy )
                    Pan1213=turn;
                else if( Pan1214==xy )
                    Pan1214=turn;
                else if( Pan1215==xy )
                    Pan1215=turn;
                else if( Pan1216==xy )
                    Pan1216=turn;
                else if( Pan1217==xy )
                    Pan1217=turn;
                else if( Pan1218==xy )
                    Pan1218=turn;
                else if( Pan1219==xy )
                    Pan1219=turn;
                else if( Pan1301==xy )
                    Pan1301=turn;
                else if( Pan1302==xy )
                    Pan1302=turn;
                else if( Pan1303==xy )
                    Pan1303=turn;
                else if( Pan1304==xy )
                    Pan1304=turn;
                else if( Pan1305==xy )
                    Pan1305=turn;
                else if( Pan1306==xy )
                    Pan1306=turn;
                else if( Pan1307==xy )
                    Pan1307=turn;
                else if( Pan1308==xy )
                    Pan1308=turn;
                else if( Pan1309==xy )
                    Pan1309=turn;
                else if( Pan1310==xy )
                    Pan1310=turn;
                else if( Pan1311==xy )
                    Pan1311=turn;
                else if( Pan1312==xy )
                    Pan1312=turn;
                else if( Pan1313==xy )
                    Pan1313=turn;
                else if( Pan1314==xy )
                    Pan1314=turn;
                else if( Pan1315==xy )
                    Pan1315=turn;
                else if( Pan1316==xy )
                    Pan1316=turn;
                else if( Pan1317==xy )
                    Pan1317=turn;
                else if( Pan1318==xy )
                    Pan1318=turn;
                else if( Pan1319==xy )
                    Pan1319=turn;
                else if( Pan1401==xy )
                    Pan1401=turn;
                else if( Pan1402==xy )
                    Pan1402=turn;
                else if( Pan1403==xy )
                    Pan1403=turn;
                else if( Pan1404==xy )
                    Pan1404=turn;
                else if( Pan1405==xy )
                    Pan1405=turn;
                else if( Pan1406==xy )
                    Pan1406=turn;
                else if( Pan1407==xy )
                    Pan1407=turn;
                else if( Pan1408==xy )
                    Pan1408=turn;
                else if( Pan1409==xy )
                    Pan1409=turn;
                else if( Pan1410==xy )
                    Pan1410=turn;
                else if( Pan1411==xy )
                    Pan1411=turn;
                else if( Pan1412==xy )
                    Pan1412=turn;
                else if( Pan1413==xy )
                    Pan1413=turn;
                else if( Pan1414==xy )
                    Pan1414=turn;
                else if( Pan1415==xy )
                    Pan1415=turn;
                else if( Pan1416==xy )
                    Pan1416=turn;
                else if( Pan1417==xy )
                    Pan1417=turn;
                else if( Pan1418==xy )
                    Pan1418=turn;
                else if( Pan1419==xy )
                    Pan1419=turn;
                else if( Pan1501==xy )
                    Pan1501=turn;
                else if( Pan1502==xy )
                    Pan1502=turn;
                else if( Pan1503==xy )
                    Pan1503=turn;
                else if( Pan1504==xy )
                    Pan1504=turn;
                else if( Pan1505==xy )
                    Pan1505=turn;
                else if( Pan1506==xy )
                    Pan1506=turn;
                else if( Pan1507==xy )
                    Pan1507=turn;
                else if( Pan1508==xy )
                    Pan1508=turn;
                else if( Pan1509==xy )
                    Pan1509=turn;
                else if( Pan1510==xy )
                    Pan1510=turn;
                else if( Pan1511==xy )
                    Pan1511=turn;
                else if( Pan1512==xy )
                    Pan1512=turn;
                else if( Pan1513==xy )
                    Pan1513=turn;
                else if( Pan1514==xy )
                    Pan1514=turn;
                else if( Pan1515==xy )
                    Pan1515=turn;
                else if( Pan1516==xy )
                    Pan1516=turn;
                else if( Pan1517==xy )
                    Pan1517=turn;
                else if( Pan1518==xy )
                    Pan1518=turn;
                else if( Pan1519==xy )
                    Pan1519=turn;
                else if( Pan1601==xy )
                    Pan1601=turn;
                else if( Pan1602==xy )
                    Pan1602=turn;
                else if( Pan1603==xy )
                    Pan1603=turn;
                else if( Pan1604==xy )
                    Pan1604=turn;
                else if( Pan1605==xy )
                    Pan1605=turn;
                else if( Pan1606==xy )
                    Pan1606=turn;
                else if( Pan1607==xy )
                    Pan1607=turn;
                else if( Pan1608==xy )
                    Pan1608=turn;
                else if( Pan1609==xy )
                    Pan1609=turn;
                else if( Pan1610==xy )
                    Pan1610=turn;
                else if( Pan1611==xy )
                    Pan1611=turn;
                else if( Pan1612==xy )
                    Pan1612=turn;
                else if( Pan1613==xy )
                    Pan1613=turn;
                else if( Pan1614==xy )
                    Pan1614=turn;
                else if( Pan1615==xy )
                    Pan1615=turn;
                else if( Pan1616==xy )
                    Pan1616=turn;
                else if( Pan1617==xy )
                    Pan1617=turn;
                else if( Pan1618==xy )
                    Pan1618=turn;
                else if( Pan1619==xy )
                    Pan1619=turn;
                else if( Pan1701==xy )
                    Pan1701=turn;
                else if( Pan1702==xy )
                    Pan1702=turn;
                else if( Pan1703==xy )
                    Pan1703=turn;
                else if( Pan1704==xy )
                    Pan1704=turn;
                else if( Pan1705==xy )
                    Pan1705=turn;
                else if( Pan1706==xy )
                    Pan1706=turn;
                else if( Pan1707==xy )
                    Pan1707=turn;
                else if( Pan1708==xy )
                    Pan1708=turn;
                else if( Pan1709==xy )
                    Pan1709=turn;
                else if( Pan1710==xy )
                    Pan1710=turn;
                else if( Pan1711==xy )
                    Pan1711=turn;
                else if( Pan1712==xy )
                    Pan1712=turn;
                else if( Pan1713==xy )
                    Pan1713=turn;
                else if( Pan1714==xy )
                    Pan1714=turn;
                else if( Pan1715==xy )
                    Pan1715=turn;
                else if( Pan1716==xy )
                    Pan1716=turn;
                else if( Pan1717==xy )
                    Pan1717=turn;
                else if( Pan1718==xy )
                    Pan1718=turn;
                else if( Pan1719==xy )
                    Pan1719=turn;
                else if( Pan1801==xy )
                    Pan1801=turn;
                else if( Pan1802==xy )
                    Pan1802=turn;
                else if( Pan1803==xy )
                    Pan1803=turn;
                else if( Pan1804==xy )
                    Pan1804=turn;
                else if( Pan1805==xy )
                    Pan1805=turn;
                else if( Pan1806==xy )
                    Pan1806=turn;
                else if( Pan1807==xy )
                    Pan1807=turn;
                else if( Pan1808==xy )
                    Pan1808=turn;
                else if( Pan1809==xy )
                    Pan1809=turn;
                else if( Pan1810==xy )
                    Pan1810=turn;
                else if( Pan1811==xy )
                    Pan1811=turn;
                else if( Pan1812==xy )
                    Pan1812=turn;
                else if( Pan1813==xy )
                    Pan1813=turn;
                else if( Pan1814==xy )
                    Pan1814=turn;
                else if( Pan1815==xy )
                    Pan1815=turn;
                else if( Pan1816==xy )
                    Pan1816=turn;
                else if( Pan1817==xy )
                    Pan1817=turn;
                else if( Pan1818==xy )
                    Pan1818=turn;
                else if( Pan1819==xy )
                    Pan1819=turn;
                else if( Pan1901==xy )
                    Pan1901=turn;
                else if( Pan1902==xy )
                    Pan1902=turn;
                else if( Pan1903==xy )
                    Pan1903=turn;
                else if( Pan1904==xy )
                    Pan1904=turn;
                else if( Pan1905==xy )
                    Pan1905=turn;
                else if( Pan1906==xy )
                    Pan1906=turn;
                else if( Pan1907==xy )
                    Pan1907=turn;
                else if( Pan1908==xy )
                    Pan1908=turn;
                else if( Pan1909==xy )
                    Pan1909=turn;
                else if( Pan1910==xy )
                    Pan1910=turn;
                else if( Pan1911==xy )
                    Pan1911=turn;
                else if( Pan1912==xy )
                    Pan1912=turn;
                else if( Pan1913==xy )
                    Pan1913=turn;
                else if( Pan1914==xy )
                    Pan1914=turn;
                else if( Pan1915==xy )
                    Pan1915=turn;
                else if( Pan1916==xy )
                    Pan1916=turn;
                else if( Pan1917==xy )
                    Pan1917=turn;
                else if( Pan1918==xy )
                    Pan1918=turn;
                else if( Pan1919==xy )
                    Pan1919=turn;
                else
                {
                    if(xy==9999)                        // 승리
                    {
                        if(turn==1)
                        {
                            turn=2;
                            BWEB=0;
                            WWEB++;        
                            printf("\n\n\n\t\t\t승리 :  백돌 ,   %d 연승 \n\n\n\n\n\n\n\n\n\n\n", WWEB);
                        }
                        else
                        {
                            turn=1;
                            WWEB=0;
                            BWEB++;
                            printf("\n\n\n\t\t\t승리 :  흑돌 ,   %d 연승 \n\n\n\n\n\n\n\n\n\n\n", BWEB);
                        }
                        printf("\n\n\n다음으로 가실려면 엔터를 눌러주세요.");
                        fflush(stdin);
                        scanf("%c", &temp1);
                        printf("\n\n\n\n\n\n");
                        break;
                    }
                    else
                    {
                        printf("이미 돌이 놓여있는 자리 입니다.");
                        continue;
                    }
                }



                /* 승리를 검사한다. */

                ////////////////////// 가로 검사 ///////////////////////////////////
                if(Pan0101==turn) 
                { if(Pan0102==turn) 
                { if(Pan0103==turn) 
                { if(Pan0104==turn) 
                { if(Pan0105==turn) 
                { win++; } } } } }
                if(Pan0102==turn) 
                { if(Pan0103==turn) 
                { if(Pan0104==turn) 
                { if(Pan0105==turn) 
                { if(Pan0106==turn) 
                { win++; } } } } }
                if(Pan0103==turn) 
                { if(Pan0104==turn) 
                { if(Pan0105==turn) 
                { if(Pan0106==turn) 
                { if(Pan0107==turn) 
                { win++; } } } } }
                if(Pan0104==turn) 
                { if(Pan0105==turn) 
                { if(Pan0106==turn) 
                { if(Pan0107==turn) 
                { if(Pan0108==turn) 
                { win++; } } } } }
                if(Pan0105==turn) 
                { if(Pan0106==turn) 
                { if(Pan0107==turn) 
                { if(Pan0108==turn) 
                { if(Pan0109==turn) 
                { win++; } } } } }
                if(Pan0106==turn) 
                { if(Pan0107==turn) 
                { if(Pan0108==turn) 
                { if(Pan0109==turn) 
                { if(Pan0110==turn) 
                { win++; } } } } }
                if(Pan0107==turn) 
                { if(Pan0108==turn) 
                { if(Pan0109==turn) 
                { if(Pan0110==turn) 
                { if(Pan0111==turn) 
                { win++; } } } } }
                if(Pan0108==turn) 
                { if(Pan0109==turn) 
                { if(Pan0110==turn) 
                { if(Pan0111==turn) 
                { if(Pan0112==turn) 
                { win++; } } } } }
                if(Pan0109==turn) 
                { if(Pan0110==turn) 
                { if(Pan0111==turn) 
                { if(Pan0112==turn) 
                { if(Pan0113==turn) 
                { win++; } } } } }
                if(Pan0110==turn) 
                { if(Pan0111==turn) 
                { if(Pan0112==turn) 
                { if(Pan0113==turn) 
                { if(Pan0114==turn) 
                { win++; } } } } }
                if(Pan0111==turn) 
                { if(Pan0112==turn) 
                { if(Pan0113==turn) 
                { if(Pan0114==turn) 
                { if(Pan0115==turn) 
                { win++; } } } } }
                if(Pan0112==turn) 
                { if(Pan0113==turn) 
                { if(Pan0114==turn) 
                { if(Pan0115==turn) 
                { if(Pan0116==turn) 
                { win++; } } } } }
                if(Pan0113==turn) 
                { if(Pan0114==turn) 
                { if(Pan0115==turn) 
                { if(Pan0116==turn) 
                { if(Pan0117==turn) 
                { win++; } } } } }
                if(Pan0114==turn) 
                { if(Pan0115==turn) 
                { if(Pan0116==turn) 
                { if(Pan0117==turn) 
                { if(Pan0118==turn) 
                { win++; } } } } }
                if(Pan0115==turn) 
                { if(Pan0116==turn) 
                { if(Pan0117==turn) 
                { if(Pan0118==turn) 
                { if(Pan0119==turn) 
                { win++; } } } } }
                if(Pan0201==turn) 
                { if(Pan0202==turn) 
                { if(Pan0203==turn) 
                { if(Pan0204==turn) 
                { if(Pan0205==turn) 
                { win++; } } } } }
                if(Pan0202==turn) 
                { if(Pan0203==turn) 
                { if(Pan0204==turn) 
                { if(Pan0205==turn) 
                { if(Pan0206==turn) 
                { win++; } } } } }
                if(Pan0203==turn) 
                { if(Pan0204==turn) 
                { if(Pan0205==turn) 
                { if(Pan0206==turn) 
                { if(Pan0207==turn) 
                { win++; } } } } }
                if(Pan0204==turn) 
                { if(Pan0205==turn) 
                { if(Pan0206==turn) 
                { if(Pan0207==turn) 
                { if(Pan0208==turn) 
                { win++; } } } } }
                if(Pan0205==turn) 
                { if(Pan0206==turn) 
                { if(Pan0207==turn) 
                { if(Pan0208==turn) 
                { if(Pan0209==turn) 
                { win++; } } } } }
                if(Pan0206==turn) 
                { if(Pan0207==turn) 
                { if(Pan0208==turn) 
                { if(Pan0209==turn) 
                { if(Pan0210==turn) 
                { win++; } } } } }
                if(Pan0207==turn) 
                { if(Pan0208==turn) 
                { if(Pan0209==turn) 
                { if(Pan0210==turn) 
                { if(Pan0211==turn) 
                { win++; } } } } }
                if(Pan0208==turn) 
                { if(Pan0209==turn) 
                { if(Pan0210==turn) 
                { if(Pan0211==turn) 
                { if(Pan0212==turn) 
                { win++; } } } } }
                if(Pan0209==turn) 
                { if(Pan0210==turn) 
                { if(Pan0211==turn) 
                { if(Pan0212==turn) 
                { if(Pan0213==turn) 
                { win++; } } } } }
                if(Pan0210==turn) 
                { if(Pan0211==turn) 
                { if(Pan0212==turn) 
                { if(Pan0213==turn) 
                { if(Pan0214==turn) 
                { win++; } } } } }
                if(Pan0211==turn) 
                { if(Pan0212==turn) 
                { if(Pan0213==turn) 
                { if(Pan0214==turn) 
                { if(Pan0215==turn) 
                { win++; } } } } }
                if(Pan0212==turn) 
                { if(Pan0213==turn) 
                { if(Pan0214==turn) 
                { if(Pan0215==turn) 
                { if(Pan0216==turn) 
                { win++; } } } } }
                if(Pan0213==turn) 
                { if(Pan0214==turn) 
                { if(Pan0215==turn) 
                { if(Pan0216==turn) 
                { if(Pan0217==turn) 
                { win++; } } } } }
                if(Pan0214==turn) 
                { if(Pan0215==turn) 
                { if(Pan0216==turn) 
                { if(Pan0217==turn) 
                { if(Pan0218==turn) 
                { win++; } } } } }
                if(Pan0215==turn) 
                { if(Pan0216==turn) 
                { if(Pan0217==turn) 
                { if(Pan0218==turn) 
                { if(Pan0219==turn) 
                { win++; } } } } }
                if(Pan0301==turn) 
                { if(Pan0302==turn) 
                { if(Pan0303==turn) 
                { if(Pan0304==turn) 
                { if(Pan0305==turn) 
                { win++; } } } } }
                if(Pan0302==turn) 
                { if(Pan0303==turn) 
                { if(Pan0304==turn) 
                { if(Pan0305==turn) 
                { if(Pan0306==turn) 
                { win++; } } } } }
                if(Pan0303==turn) 
                { if(Pan0304==turn) 
                { if(Pan0305==turn) 
                { if(Pan0306==turn) 
                { if(Pan0307==turn) 
                { win++; } } } } }
                if(Pan0304==turn) 
                { if(Pan0305==turn) 
                { if(Pan0306==turn) 
                { if(Pan0307==turn) 
                { if(Pan0308==turn) 
                { win++; } } } } }
                if(Pan0305==turn) 
                { if(Pan0306==turn) 
                { if(Pan0307==turn) 
                { if(Pan0308==turn) 
                { if(Pan0309==turn) 
                { win++; } } } } }
                if(Pan0306==turn) 
                { if(Pan0307==turn) 
                { if(Pan0308==turn) 
                { if(Pan0309==turn) 
                { if(Pan0310==turn) 
                { win++; } } } } }
                if(Pan0307==turn) 
                { if(Pan0308==turn) 
                { if(Pan0309==turn) 
                { if(Pan0310==turn) 
                { if(Pan0311==turn) 
                { win++; } } } } }
                if(Pan0308==turn) 
                { if(Pan0309==turn) 
                { if(Pan0310==turn) 
                { if(Pan0311==turn) 
                { if(Pan0312==turn) 
                { win++; } } } } }
                if(Pan0309==turn) 
                { if(Pan0310==turn) 
                { if(Pan0311==turn) 
                { if(Pan0312==turn) 
                { if(Pan0313==turn) 
                { win++; } } } } }
                if(Pan0310==turn) 
                { if(Pan0311==turn) 
                { if(Pan0312==turn) 
                { if(Pan0313==turn) 
                { if(Pan0314==turn) 
                { win++; } } } } }
                if(Pan0311==turn) 
                { if(Pan0312==turn) 
                { if(Pan0313==turn) 
                { if(Pan0314==turn) 
                { if(Pan0315==turn) 
                { win++; } } } } }
                if(Pan0312==turn) 
                { if(Pan0313==turn) 
                { if(Pan0314==turn) 
                { if(Pan0315==turn) 
                { if(Pan0316==turn) 
                { win++; } } } } }
                if(Pan0313==turn) 
                { if(Pan0314==turn) 
                { if(Pan0315==turn) 
                { if(Pan0316==turn) 
                { if(Pan0317==turn) 
                { win++; } } } } }
                if(Pan0314==turn) 
                { if(Pan0315==turn) 
                { if(Pan0316==turn) 
                { if(Pan0317==turn) 
                { if(Pan0318==turn) 
                { win++; } } } } }
                if(Pan0315==turn) 
                { if(Pan0316==turn) 
                { if(Pan0317==turn) 
                { if(Pan0318==turn) 
                { if(Pan0319==turn) 
                { win++; } } } } }
                if(Pan0401==turn) 
                { if(Pan0402==turn) 
                { if(Pan0403==turn) 
                { if(Pan0404==turn) 
                { if(Pan0405==turn) 
                { win++; } } } } }
                if(Pan0402==turn) 
                { if(Pan0403==turn) 
                { if(Pan0404==turn) 
                { if(Pan0405==turn) 
                { if(Pan0406==turn) 
                { win++; } } } } }
                if(Pan0403==turn) 
                { if(Pan0404==turn) 
                { if(Pan0405==turn) 
                { if(Pan0406==turn) 
                { if(Pan0407==turn) 
                { win++; } } } } }
                if(Pan0404==turn) 
                { if(Pan0405==turn) 
                { if(Pan0406==turn) 
                { if(Pan0407==turn) 
                { if(Pan0408==turn) 
                { win++; } } } } }
                if(Pan0405==turn) 
                { if(Pan0406==turn) 
                { if(Pan0407==turn) 
                { if(Pan0408==turn) 
                { if(Pan0409==turn) 
                { win++; } } } } }
                if(Pan0406==turn) 
                { if(Pan0407==turn) 
                { if(Pan0408==turn) 
                { if(Pan0409==turn) 
                { if(Pan0410==turn) 
                { win++; } } } } }
                if(Pan0407==turn) 
                { if(Pan0408==turn) 
                { if(Pan0409==turn) 
                { if(Pan0410==turn) 
                { if(Pan0411==turn) 
                { win++; } } } } }
                if(Pan0408==turn) 
                { if(Pan0409==turn) 
                { if(Pan0410==turn) 
                { if(Pan0411==turn) 
                { if(Pan0412==turn) 
                { win++; } } } } }
                if(Pan0409==turn) 
                { if(Pan0410==turn) 
                { if(Pan0411==turn) 
                { if(Pan0412==turn) 
                { if(Pan0413==turn) 
                { win++; } } } } }
                if(Pan0410==turn) 
                { if(Pan0411==turn) 
                { if(Pan0412==turn) 
                { if(Pan0413==turn) 
                { if(Pan0414==turn) 
                { win++; } } } } }
                if(Pan0411==turn) 
                { if(Pan0412==turn) 
                { if(Pan0413==turn) 
                { if(Pan0414==turn) 
                { if(Pan0415==turn) 
                { win++; } } } } }
                if(Pan0412==turn) 
                { if(Pan0413==turn) 
                { if(Pan0414==turn) 
                { if(Pan0415==turn) 
                { if(Pan0416==turn) 
                { win++; } } } } }
                if(Pan0413==turn) 
                { if(Pan0414==turn) 
                { if(Pan0415==turn) 
                { if(Pan0416==turn) 
                { if(Pan0417==turn) 
                { win++; } } } } }
                if(Pan0414==turn) 
                { if(Pan0415==turn) 
                { if(Pan0416==turn) 
                { if(Pan0417==turn) 
                { if(Pan0418==turn) 
                { win++; } } } } }
                if(Pan0415==turn) 
                { if(Pan0416==turn) 
                { if(Pan0417==turn) 
                { if(Pan0418==turn) 
                { if(Pan0419==turn) 
                { win++; } } } } }
                if(Pan0501==turn) 
                { if(Pan0502==turn) 
                { if(Pan0503==turn) 
                { if(Pan0504==turn) 
                { if(Pan0505==turn) 
                { win++; } } } } }
                if(Pan0502==turn) 
                { if(Pan0503==turn) 
                { if(Pan0504==turn) 
                { if(Pan0505==turn) 
                { if(Pan0506==turn) 
                { win++; } } } } }
                if(Pan0503==turn) 
                { if(Pan0504==turn) 
                { if(Pan0505==turn) 
                { if(Pan0506==turn) 
                { if(Pan0507==turn) 
                { win++; } } } } }
                if(Pan0504==turn) 
                { if(Pan0505==turn) 
                { if(Pan0506==turn) 
                { if(Pan0507==turn) 
                { if(Pan0508==turn) 
                { win++; } } } } }
                if(Pan0505==turn) 
                { if(Pan0506==turn) 
                { if(Pan0507==turn) 
                { if(Pan0508==turn) 
                { if(Pan0509==turn) 
                { win++; } } } } }
                if(Pan0506==turn) 
                { if(Pan0507==turn) 
                { if(Pan0508==turn) 
                { if(Pan0509==turn) 
                { if(Pan0510==turn) 
                { win++; } } } } }
                if(Pan0507==turn) 
                { if(Pan0508==turn) 
                { if(Pan0509==turn) 
                { if(Pan0510==turn) 
                { if(Pan0511==turn) 
                { win++; } } } } }
                if(Pan0508==turn) 
                { if(Pan0509==turn) 
                { if(Pan0510==turn) 
                { if(Pan0511==turn) 
                { if(Pan0512==turn) 
                { win++; } } } } }
                if(Pan0509==turn) 
                { if(Pan0510==turn) 
                { if(Pan0511==turn) 
                { if(Pan0512==turn) 
                { if(Pan0513==turn) 
                { win++; } } } } }
                if(Pan0510==turn) 
                { if(Pan0511==turn) 
                { if(Pan0512==turn) 
                { if(Pan0513==turn) 
                { if(Pan0514==turn) 
                { win++; } } } } }
                if(Pan0511==turn) 
                { if(Pan0512==turn) 
                { if(Pan0513==turn) 
                { if(Pan0514==turn) 
                { if(Pan0515==turn) 
                { win++; } } } } }
                if(Pan0512==turn) 
                { if(Pan0513==turn) 
                { if(Pan0514==turn) 
                { if(Pan0515==turn) 
                { if(Pan0516==turn) 
                { win++; } } } } }
                if(Pan0513==turn) 
                { if(Pan0514==turn) 
                { if(Pan0515==turn) 
                { if(Pan0516==turn) 
                { if(Pan0517==turn) 
                { win++; } } } } }
                if(Pan0514==turn) 
                { if(Pan0515==turn) 
                { if(Pan0516==turn) 
                { if(Pan0517==turn) 
                { if(Pan0518==turn) 
                { win++; } } } } }
                if(Pan0515==turn) 
                { if(Pan0516==turn) 
                { if(Pan0517==turn) 
                { if(Pan0518==turn) 
                { if(Pan0519==turn) 
                { win++; } } } } }
                if(Pan0601==turn) 
                { if(Pan0602==turn) 
                { if(Pan0603==turn) 
                { if(Pan0604==turn) 
                { if(Pan0605==turn) 
                { win++; } } } } }
                if(Pan0602==turn) 
                { if(Pan0603==turn) 
                { if(Pan0604==turn) 
                { if(Pan0605==turn) 
                { if(Pan0606==turn) 
                { win++; } } } } }
                if(Pan0603==turn) 
                { if(Pan0604==turn) 
                { if(Pan0605==turn) 
                { if(Pan0606==turn) 
                { if(Pan0607==turn) 
                { win++; } } } } }
                if(Pan0604==turn) 
                { if(Pan0605==turn) 
                { if(Pan0606==turn) 
                { if(Pan0607==turn) 
                { if(Pan0608==turn) 
                { win++; } } } } }
                if(Pan0605==turn) 
                { if(Pan0606==turn) 
                { if(Pan0607==turn) 
                { if(Pan0608==turn) 
                { if(Pan0609==turn) 
                { win++; } } } } }
                if(Pan0606==turn) 
                { if(Pan0607==turn) 
                { if(Pan0608==turn) 
                { if(Pan0609==turn) 
                { if(Pan0610==turn) 
                { win++; } } } } }
                if(Pan0607==turn) 
                { if(Pan0608==turn) 
                { if(Pan0609==turn) 
                { if(Pan0610==turn) 
                { if(Pan0611==turn) 
                { win++; } } } } }
                if(Pan0608==turn) 
                { if(Pan0609==turn) 
                { if(Pan0610==turn) 
                { if(Pan0611==turn) 
                { if(Pan0612==turn) 
                { win++; } } } } }
                if(Pan0609==turn) 
                { if(Pan0610==turn) 
                { if(Pan0611==turn) 
                { if(Pan0612==turn) 
                { if(Pan0613==turn) 
                { win++; } } } } }
                if(Pan0610==turn) 
                { if(Pan0611==turn) 
                { if(Pan0612==turn) 
                { if(Pan0613==turn) 
                { if(Pan0614==turn) 
                { win++; } } } } }
                if(Pan0611==turn) 
                { if(Pan0612==turn) 
                { if(Pan0613==turn) 
                { if(Pan0614==turn) 
                { if(Pan0615==turn) 
                { win++; } } } } }
                if(Pan0612==turn) 
                { if(Pan0613==turn) 
                { if(Pan0614==turn) 
                { if(Pan0615==turn) 
                { if(Pan0616==turn) 
                { win++; } } } } }
                if(Pan0613==turn) 
                { if(Pan0614==turn) 
                { if(Pan0615==turn) 
                { if(Pan0616==turn) 
                { if(Pan0617==turn) 
                { win++; } } } } }
                if(Pan0614==turn) 
                { if(Pan0615==turn) 
                { if(Pan0616==turn) 
                { if(Pan0617==turn) 
                { if(Pan0618==turn) 
                { win++; } } } } }
                if(Pan0615==turn) 
                { if(Pan0616==turn) 
                { if(Pan0617==turn) 
                { if(Pan0618==turn) 
                { if(Pan0619==turn) 
                { win++; } } } } }
                if(Pan0701==turn) 
                { if(Pan0702==turn) 
                { if(Pan0703==turn) 
                { if(Pan0704==turn) 
                { if(Pan0705==turn) 
                { win++; } } } } }
                if(Pan0702==turn) 
                { if(Pan0703==turn) 
                { if(Pan0704==turn) 
                { if(Pan0705==turn) 
                { if(Pan0706==turn) 
                { win++; } } } } }
                if(Pan0703==turn) 
                { if(Pan0704==turn) 
                { if(Pan0705==turn) 
                { if(Pan0706==turn) 
                { if(Pan0707==turn) 
                { win++; } } } } }
                if(Pan0704==turn) 
                { if(Pan0705==turn) 
                { if(Pan0706==turn) 
                { if(Pan0707==turn) 
                { if(Pan0708==turn) 
                { win++; } } } } }
                if(Pan0705==turn) 
                { if(Pan0706==turn) 
                { if(Pan0707==turn) 
                { if(Pan0708==turn) 
                { if(Pan0709==turn) 
                { win++; } } } } }
                if(Pan0706==turn) 
                { if(Pan0707==turn) 
                { if(Pan0708==turn) 
                { if(Pan0709==turn) 
                { if(Pan0710==turn) 
                { win++; } } } } }
                if(Pan0707==turn) 
                { if(Pan0708==turn) 
                { if(Pan0709==turn) 
                { if(Pan0710==turn) 
                { if(Pan0711==turn) 
                { win++; } } } } }
                if(Pan0708==turn) 
                { if(Pan0709==turn) 
                { if(Pan0710==turn) 
                { if(Pan0711==turn) 
                { if(Pan0712==turn) 
                { win++; } } } } }
                if(Pan0709==turn) 
                { if(Pan0710==turn) 
                { if(Pan0711==turn) 
                { if(Pan0712==turn) 
                { if(Pan0713==turn) 
                { win++; } } } } }
                if(Pan0710==turn) 
                { if(Pan0711==turn) 
                { if(Pan0712==turn) 
                { if(Pan0713==turn) 
                { if(Pan0714==turn) 
                { win++; } } } } }
                if(Pan0711==turn) 
                { if(Pan0712==turn) 
                { if(Pan0713==turn) 
                { if(Pan0714==turn) 
                { if(Pan0715==turn) 
                { win++; } } } } }
                if(Pan0712==turn) 
                { if(Pan0713==turn) 
                { if(Pan0714==turn) 
                { if(Pan0715==turn) 
                { if(Pan0716==turn) 
                { win++; } } } } }
                if(Pan0713==turn) 
                { if(Pan0714==turn) 
                { if(Pan0715==turn) 
                { if(Pan0716==turn) 
                { if(Pan0717==turn) 
                { win++; } } } } }
                if(Pan0714==turn) 
                { if(Pan0715==turn) 
                { if(Pan0716==turn) 
                { if(Pan0717==turn) 
                { if(Pan0718==turn) 
                { win++; } } } } }
                if(Pan0715==turn) 
                { if(Pan0716==turn) 
                { if(Pan0717==turn) 
                { if(Pan0718==turn) 
                { if(Pan0719==turn) 
                { win++; } } } } }
                if(Pan0801==turn) 
                { if(Pan0802==turn) 
                { if(Pan0803==turn) 
                { if(Pan0804==turn) 
                { if(Pan0805==turn) 
                { win++; } } } } }
                if(Pan0802==turn) 
                { if(Pan0803==turn) 
                { if(Pan0804==turn) 
                { if(Pan0805==turn) 
                { if(Pan0806==turn) 
                { win++; } } } } }
                if(Pan0803==turn) 
                { if(Pan0804==turn) 
                { if(Pan0805==turn) 
                { if(Pan0806==turn) 
                { if(Pan0807==turn) 
                { win++; } } } } }
                if(Pan0804==turn) 
                { if(Pan0805==turn) 
                { if(Pan0806==turn) 
                { if(Pan0807==turn) 
                { if(Pan0808==turn) 
                { win++; } } } } }
                if(Pan0805==turn) 
                { if(Pan0806==turn) 
                { if(Pan0807==turn) 
                { if(Pan0808==turn) 
                { if(Pan0809==turn) 
                { win++; } } } } }
                if(Pan0806==turn) 
                { if(Pan0807==turn) 
                { if(Pan0808==turn) 
                { if(Pan0809==turn) 
                { if(Pan0810==turn) 
                { win++; } } } } }
                if(Pan0807==turn) 
                { if(Pan0808==turn) 
                { if(Pan0809==turn) 
                { if(Pan0810==turn) 
                { if(Pan0811==turn) 
                { win++; } } } } }
                if(Pan0808==turn) 
                { if(Pan0809==turn) 
                { if(Pan0810==turn) 
                { if(Pan0811==turn) 
                { if(Pan0812==turn) 
                { win++; } } } } }
                if(Pan0809==turn) 
                { if(Pan0810==turn) 
                { if(Pan0811==turn) 
                { if(Pan0812==turn) 
                { if(Pan0813==turn) 
                { win++; } } } } }
                if(Pan0810==turn) 
                { if(Pan0811==turn) 
                { if(Pan0812==turn) 
                { if(Pan0813==turn) 
                { if(Pan0814==turn) 
                { win++; } } } } }
                if(Pan0811==turn) 
                { if(Pan0812==turn) 
                { if(Pan0813==turn) 
                { if(Pan0814==turn) 
                { if(Pan0815==turn) 
                { win++; } } } } }
                if(Pan0812==turn) 
                { if(Pan0813==turn) 
                { if(Pan0814==turn) 
                { if(Pan0815==turn) 
                { if(Pan0816==turn) 
                { win++; } } } } }
                if(Pan0813==turn) 
                { if(Pan0814==turn) 
                { if(Pan0815==turn) 
                { if(Pan0816==turn) 
                { if(Pan0817==turn) 
                { win++; } } } } }
                if(Pan0814==turn) 
                { if(Pan0815==turn) 
                { if(Pan0816==turn) 
                { if(Pan0817==turn) 
                { if(Pan0818==turn) 
                { win++; } } } } }
                if(Pan0815==turn) 
                { if(Pan0816==turn) 
                { if(Pan0817==turn) 
                { if(Pan0818==turn) 
                { if(Pan0819==turn) 
                { win++; } } } } }
                if(Pan0901==turn) 
                { if(Pan0902==turn) 
                { if(Pan0903==turn) 
                { if(Pan0904==turn) 
                { if(Pan0905==turn) 
                { win++; } } } } }
                if(Pan0902==turn) 
                { if(Pan0903==turn) 
                { if(Pan0904==turn) 
                { if(Pan0905==turn) 
                { if(Pan0906==turn) 
                { win++; } } } } }
                if(Pan0903==turn) 
                { if(Pan0904==turn) 
                { if(Pan0905==turn) 
                { if(Pan0906==turn) 
                { if(Pan0907==turn) 
                { win++; } } } } }
                if(Pan0904==turn) 
                { if(Pan0905==turn) 
                { if(Pan0906==turn) 
                { if(Pan0907==turn) 
                { if(Pan0908==turn) 
                { win++; } } } } }
                if(Pan0905==turn) 
                { if(Pan0906==turn) 
                { if(Pan0907==turn) 
                { if(Pan0908==turn) 
                { if(Pan0909==turn) 
                { win++; } } } } }
                if(Pan0906==turn) 
                { if(Pan0907==turn) 
                { if(Pan0908==turn) 
                { if(Pan0909==turn) 
                { if(Pan0910==turn) 
                { win++; } } } } }
                if(Pan0907==turn) 
                { if(Pan0908==turn) 
                { if(Pan0909==turn) 
                { if(Pan0910==turn) 
                { if(Pan0911==turn) 
                { win++; } } } } }
                if(Pan0908==turn) 
                { if(Pan0909==turn) 
                { if(Pan0910==turn) 
                { if(Pan0911==turn) 
                { if(Pan0912==turn) 
                { win++; } } } } }
                if(Pan0909==turn) 
                { if(Pan0910==turn) 
                { if(Pan0911==turn) 
                { if(Pan0912==turn) 
                { if(Pan0913==turn) 
                { win++; } } } } }
                if(Pan0910==turn) 
                { if(Pan0911==turn) 
                { if(Pan0912==turn) 
                { if(Pan0913==turn) 
                { if(Pan0914==turn) 
                { win++; } } } } }
                if(Pan0911==turn) 
                { if(Pan0912==turn) 
                { if(Pan0913==turn) 
                { if(Pan0914==turn) 
                { if(Pan0915==turn) 
                { win++; } } } } }
                if(Pan0912==turn) 
                { if(Pan0913==turn) 
                { if(Pan0914==turn) 
                { if(Pan0915==turn) 
                { if(Pan0916==turn) 
                { win++; } } } } }
                if(Pan0913==turn) 
                { if(Pan0914==turn) 
                { if(Pan0915==turn) 
                { if(Pan0916==turn) 
                { if(Pan0917==turn) 
                { win++; } } } } }
                if(Pan0914==turn) 
                { if(Pan0915==turn) 
                { if(Pan0916==turn) 
                { if(Pan0917==turn) 
                { if(Pan0918==turn) 
                { win++; } } } } }
                if(Pan0915==turn) 
                { if(Pan0916==turn) 
                { if(Pan0917==turn) 
                { if(Pan0918==turn) 
                { if(Pan0919==turn) 
                { win++; } } } } }
                if(Pan1001==turn) 
                { if(Pan1002==turn) 
                { if(Pan1003==turn) 
                { if(Pan1004==turn) 
                { if(Pan1005==turn) 
                { win++; } } } } }
                if(Pan1002==turn) 
                { if(Pan1003==turn) 
                { if(Pan1004==turn) 
                { if(Pan1005==turn) 
                { if(Pan1006==turn) 
                { win++; } } } } }
                if(Pan1003==turn) 
                { if(Pan1004==turn) 
                { if(Pan1005==turn) 
                { if(Pan1006==turn) 
                { if(Pan1007==turn) 
                { win++; } } } } }
                if(Pan1004==turn) 
                { if(Pan1005==turn) 
                { if(Pan1006==turn) 
                { if(Pan1007==turn) 
                { if(Pan1008==turn) 
                { win++; } } } } }
                if(Pan1005==turn) 
                { if(Pan1006==turn) 
                { if(Pan1007==turn) 
                { if(Pan1008==turn) 
                { if(Pan1009==turn) 
                { win++; } } } } }
                if(Pan1006==turn) 
                { if(Pan1007==turn) 
                { if(Pan1008==turn) 
                { if(Pan1009==turn) 
                { if(Pan1010==turn) 
                { win++; } } } } }
                if(Pan1007==turn) 
                { if(Pan1008==turn) 
                { if(Pan1009==turn) 
                { if(Pan1010==turn) 
                { if(Pan1011==turn) 
                { win++; } } } } }
                if(Pan1008==turn) 
                { if(Pan1009==turn) 
                { if(Pan1010==turn) 
                { if(Pan1011==turn) 
                { if(Pan1012==turn) 
                { win++; } } } } }
                if(Pan1009==turn) 
                { if(Pan1010==turn) 
                { if(Pan1011==turn) 
                { if(Pan1012==turn) 
                { if(Pan1013==turn) 
                { win++; } } } } }
                if(Pan1010==turn) 
                { if(Pan1011==turn) 
                { if(Pan1012==turn) 
                { if(Pan1013==turn) 
                { if(Pan1014==turn) 
                { win++; } } } } }
                if(Pan1011==turn) 
                { if(Pan1012==turn) 
                { if(Pan1013==turn) 
                { if(Pan1014==turn) 
                { if(Pan1015==turn) 
                { win++; } } } } }
                if(Pan1012==turn) 
                { if(Pan1013==turn) 
                { if(Pan1014==turn) 
                { if(Pan1015==turn) 
                { if(Pan1016==turn) 
                { win++; } } } } }
                if(Pan1013==turn) 
                { if(Pan1014==turn) 
                { if(Pan1015==turn) 
                { if(Pan1016==turn) 
                { if(Pan1017==turn) 
                { win++; } } } } }
                if(Pan1014==turn) 
                { if(Pan1015==turn) 
                { if(Pan1016==turn) 
                { if(Pan1017==turn) 
                { if(Pan1018==turn) 
                { win++; } } } } }
                if(Pan1015==turn) 
                { if(Pan1016==turn) 
                { if(Pan1017==turn) 
                { if(Pan1018==turn) 
                { if(Pan1019==turn) 
                { win++; } } } } }
                if(Pan1101==turn) 
                { if(Pan1102==turn) 
                { if(Pan1103==turn) 
                { if(Pan1104==turn) 
                { if(Pan1105==turn) 
                { win++; } } } } }
                if(Pan1102==turn) 
                { if(Pan1103==turn) 
                { if(Pan1104==turn) 
                { if(Pan1105==turn) 
                { if(Pan1106==turn) 
                { win++; } } } } }
                if(Pan1103==turn) 
                { if(Pan1104==turn) 
                { if(Pan1105==turn) 
                { if(Pan1106==turn) 
                { if(Pan1107==turn) 
                { win++; } } } } }
                if(Pan1104==turn) 
                { if(Pan1105==turn) 
                { if(Pan1106==turn) 
                { if(Pan1107==turn) 
                { if(Pan1108==turn) 
                { win++; } } } } }
                if(Pan1105==turn) 
                { if(Pan1106==turn) 
                { if(Pan1107==turn) 
                { if(Pan1108==turn) 
                { if(Pan1109==turn) 
                { win++; } } } } }
                if(Pan1106==turn) 
                { if(Pan1107==turn) 
                { if(Pan1108==turn) 
                { if(Pan1109==turn) 
                { if(Pan1110==turn) 
                { win++; } } } } }
                if(Pan1107==turn) 
                { if(Pan1108==turn) 
                { if(Pan1109==turn) 
                { if(Pan1110==turn) 
                { if(Pan1111==turn) 
                { win++; } } } } }
                if(Pan1108==turn) 
                { if(Pan1109==turn) 
                { if(Pan1110==turn) 
                { if(Pan1111==turn) 
                { if(Pan1112==turn) 
                { win++; } } } } }
                if(Pan1109==turn) 
                { if(Pan1110==turn) 
                { if(Pan1111==turn) 
                { if(Pan1112==turn) 
                { if(Pan1113==turn) 
                { win++; } } } } }
                if(Pan1110==turn) 
                { if(Pan1111==turn) 
                { if(Pan1112==turn) 
                { if(Pan1113==turn) 
                { if(Pan1114==turn) 
                { win++; } } } } }
                if(Pan1111==turn) 
                { if(Pan1112==turn) 
                { if(Pan1113==turn) 
                { if(Pan1114==turn) 
                { if(Pan1115==turn) 
                { win++; } } } } }
                if(Pan1112==turn) 
                { if(Pan1113==turn) 
                { if(Pan1114==turn) 
                { if(Pan1115==turn) 
                { if(Pan1116==turn) 
                { win++; } } } } }
                if(Pan1113==turn) 
                { if(Pan1114==turn) 
                { if(Pan1115==turn) 
                { if(Pan1116==turn) 
                { if(Pan1117==turn) 
                { win++; } } } } }
                if(Pan1114==turn) 
                { if(Pan1115==turn) 
                { if(Pan1116==turn) 
                { if(Pan1117==turn) 
                { if(Pan1118==turn) 
                { win++; } } } } }
                if(Pan1115==turn) 
                { if(Pan1116==turn) 
                { if(Pan1117==turn) 
                { if(Pan1118==turn) 
                { if(Pan1119==turn) 
                { win++; } } } } }
                if(Pan1201==turn) 
                { if(Pan1202==turn) 
                { if(Pan1203==turn) 
                { if(Pan1204==turn) 
                { if(Pan1205==turn) 
                { win++; } } } } }
                if(Pan1202==turn) 
                { if(Pan1203==turn) 
                { if(Pan1204==turn) 
                { if(Pan1205==turn) 
                { if(Pan1206==turn) 
                { win++; } } } } }
                if(Pan1203==turn) 
                { if(Pan1204==turn) 
                { if(Pan1205==turn) 
                { if(Pan1206==turn) 
                { if(Pan1207==turn) 
                { win++; } } } } }
                if(Pan1204==turn) 
                { if(Pan1205==turn) 
                { if(Pan1206==turn) 
                { if(Pan1207==turn) 
                { if(Pan1208==turn) 
                { win++; } } } } }
                if(Pan1205==turn) 
                { if(Pan1206==turn) 
                { if(Pan1207==turn) 
                { if(Pan1208==turn) 
                { if(Pan1209==turn) 
                { win++; } } } } }
                if(Pan1206==turn) 
                { if(Pan1207==turn) 
                { if(Pan1208==turn) 
                { if(Pan1209==turn) 
                { if(Pan1210==turn) 
                { win++; } } } } }
                if(Pan1207==turn) 
                { if(Pan1208==turn) 
                { if(Pan1209==turn) 
                { if(Pan1210==turn) 
                { if(Pan1211==turn) 
                { win++; } } } } }
                if(Pan1208==turn) 
                { if(Pan1209==turn) 
                { if(Pan1210==turn) 
                { if(Pan1211==turn) 
                { if(Pan1212==turn) 
                { win++; } } } } }
                if(Pan1209==turn) 
                { if(Pan1210==turn) 
                { if(Pan1211==turn) 
                { if(Pan1212==turn) 
                { if(Pan1213==turn) 
                { win++; } } } } }
                if(Pan1210==turn) 
                { if(Pan1211==turn) 
                { if(Pan1212==turn) 
                { if(Pan1213==turn) 
                { if(Pan1214==turn) 
                { win++; } } } } }
                if(Pan1211==turn) 
                { if(Pan1212==turn) 
                { if(Pan1213==turn) 
                { if(Pan1214==turn) 
                { if(Pan1215==turn) 
                { win++; } } } } }
                if(Pan1212==turn) 
                { if(Pan1213==turn) 
                { if(Pan1214==turn) 
                { if(Pan1215==turn) 
                { if(Pan1216==turn) 
                { win++; } } } } }
                if(Pan1213==turn) 
                { if(Pan1214==turn) 
                { if(Pan1215==turn) 
                { if(Pan1216==turn) 
                { if(Pan1217==turn) 
                { win++; } } } } }
                if(Pan1214==turn) 
                { if(Pan1215==turn) 
                { if(Pan1216==turn) 
                { if(Pan1217==turn) 
                { if(Pan1218==turn) 
                { win++; } } } } }
                if(Pan1215==turn) 
                { if(Pan1216==turn) 
                { if(Pan1217==turn) 
                { if(Pan1218==turn) 
                { if(Pan1219==turn) 
                { win++; } } } } }
                if(Pan1301==turn) 
                { if(Pan1302==turn) 
                { if(Pan1303==turn) 
                { if(Pan1304==turn) 
                { if(Pan1305==turn) 
                { win++; } } } } }
                if(Pan1302==turn) 
                { if(Pan1303==turn) 
                { if(Pan1304==turn) 
                { if(Pan1305==turn) 
                { if(Pan1306==turn) 
                { win++; } } } } }
                if(Pan1303==turn) 
                { if(Pan1304==turn) 
                { if(Pan1305==turn) 
                { if(Pan1306==turn) 
                { if(Pan1307==turn) 
                { win++; } } } } }
                if(Pan1304==turn) 
                { if(Pan1305==turn) 
                { if(Pan1306==turn) 
                { if(Pan1307==turn) 
                { if(Pan1308==turn) 
                { win++; } } } } }
                if(Pan1305==turn) 
                { if(Pan1306==turn) 
                { if(Pan1307==turn) 
                { if(Pan1308==turn) 
                { if(Pan1309==turn) 
                { win++; } } } } }
                if(Pan1306==turn) 
                { if(Pan1307==turn) 
                { if(Pan1308==turn) 
                { if(Pan1309==turn) 
                { if(Pan1310==turn) 
                { win++; } } } } }
                if(Pan1307==turn) 
                { if(Pan1308==turn) 
                { if(Pan1309==turn) 
                { if(Pan1310==turn) 
                { if(Pan1311==turn) 
                { win++; } } } } }
                if(Pan1308==turn) 
                { if(Pan1309==turn) 
                { if(Pan1310==turn) 
                { if(Pan1311==turn) 
                { if(Pan1312==turn) 
                { win++; } } } } }
                if(Pan1309==turn) 
                { if(Pan1310==turn) 
                { if(Pan1311==turn) 
                { if(Pan1312==turn) 
                { if(Pan1313==turn) 
                { win++; } } } } }
                if(Pan1310==turn) 
                { if(Pan1311==turn) 
                { if(Pan1312==turn) 
                { if(Pan1313==turn) 
                { if(Pan1314==turn) 
                { win++; } } } } }
                if(Pan1311==turn) 
                { if(Pan1312==turn) 
                { if(Pan1313==turn) 
                { if(Pan1314==turn) 
                { if(Pan1315==turn) 
                { win++; } } } } }
                if(Pan1312==turn) 
                { if(Pan1313==turn) 
                { if(Pan1314==turn) 
                { if(Pan1315==turn) 
                { if(Pan1316==turn) 
                { win++; } } } } }
                if(Pan1313==turn) 
                { if(Pan1314==turn) 
                { if(Pan1315==turn) 
                { if(Pan1316==turn) 
                { if(Pan1317==turn) 
                { win++; } } } } }
                if(Pan1314==turn) 
                { if(Pan1315==turn) 
                { if(Pan1316==turn) 
                { if(Pan1317==turn) 
                { if(Pan1318==turn) 
                { win++; } } } } }
                if(Pan1315==turn) 
                { if(Pan1316==turn) 
                { if(Pan1317==turn) 
                { if(Pan1318==turn) 
                { if(Pan1319==turn) 
                { win++; } } } } }
                if(Pan1401==turn) 
                { if(Pan1402==turn) 
                { if(Pan1403==turn) 
                { if(Pan1404==turn) 
                { if(Pan1405==turn) 
                { win++; } } } } }
                if(Pan1402==turn) 
                { if(Pan1403==turn) 
                { if(Pan1404==turn) 
                { if(Pan1405==turn) 
                { if(Pan1406==turn) 
                { win++; } } } } }
                if(Pan1403==turn) 
                { if(Pan1404==turn) 
                { if(Pan1405==turn) 
                { if(Pan1406==turn) 
                { if(Pan1407==turn) 
                { win++; } } } } }
                if(Pan1404==turn) 
                { if(Pan1405==turn) 
                { if(Pan1406==turn) 
                { if(Pan1407==turn) 
                { if(Pan1408==turn) 
                { win++; } } } } }
                if(Pan1405==turn) 
                { if(Pan1406==turn) 
                { if(Pan1407==turn) 
                { if(Pan1408==turn) 
                { if(Pan1409==turn) 
                { win++; } } } } }
                if(Pan1406==turn) 
                { if(Pan1407==turn) 
                { if(Pan1408==turn) 
                { if(Pan1409==turn) 
                { if(Pan1410==turn) 
                { win++; } } } } }
                if(Pan1407==turn) 
                { if(Pan1408==turn) 
                { if(Pan1409==turn) 
                { if(Pan1410==turn) 
                { if(Pan1411==turn) 
                { win++; } } } } }
                if(Pan1408==turn) 
                { if(Pan1409==turn) 
                { if(Pan1410==turn) 
                { if(Pan1411==turn) 
                { if(Pan1412==turn) 
                { win++; } } } } }
                if(Pan1409==turn) 
                { if(Pan1410==turn) 
                { if(Pan1411==turn) 
                { if(Pan1412==turn) 
                { if(Pan1413==turn) 
                { win++; } } } } }
                if(Pan1410==turn) 
                { if(Pan1411==turn) 
                { if(Pan1412==turn) 
                { if(Pan1413==turn) 
                { if(Pan1414==turn) 
                { win++; } } } } }
                if(Pan1411==turn) 
                { if(Pan1412==turn) 
                { if(Pan1413==turn) 
                { if(Pan1414==turn) 
                { if(Pan1415==turn) 
                { win++; } } } } }
                if(Pan1412==turn) 
                { if(Pan1413==turn) 
                { if(Pan1414==turn) 
                { if(Pan1415==turn) 
                { if(Pan1416==turn) 
                { win++; } } } } }
                if(Pan1413==turn) 
                { if(Pan1414==turn) 
                { if(Pan1415==turn) 
                { if(Pan1416==turn) 
                { if(Pan1417==turn) 
                { win++; } } } } }
                if(Pan1414==turn) 
                { if(Pan1415==turn) 
                { if(Pan1416==turn) 
                { if(Pan1417==turn) 
                { if(Pan1418==turn) 
                { win++; } } } } }
                if(Pan1415==turn) 
                { if(Pan1416==turn) 
                { if(Pan1417==turn) 
                { if(Pan1418==turn) 
                { if(Pan1419==turn) 
                { win++; } } } } }
                if(Pan1501==turn) 
                { if(Pan1502==turn) 
                { if(Pan1503==turn) 
                { if(Pan1504==turn) 
                { if(Pan1505==turn) 
                { win++; } } } } }
                if(Pan1502==turn) 
                { if(Pan1503==turn) 
                { if(Pan1504==turn) 
                { if(Pan1505==turn) 
                { if(Pan1506==turn) 
                { win++; } } } } }
                if(Pan1503==turn) 
                { if(Pan1504==turn) 
                { if(Pan1505==turn) 
                { if(Pan1506==turn) 
                { if(Pan1507==turn) 
                { win++; } } } } }
                if(Pan1504==turn) 
                { if(Pan1505==turn) 
                { if(Pan1506==turn) 
                { if(Pan1507==turn) 
                { if(Pan1508==turn) 
                { win++; } } } } }
                if(Pan1505==turn) 
                { if(Pan1506==turn) 
                { if(Pan1507==turn) 
                { if(Pan1508==turn) 
                { if(Pan1509==turn) 
                { win++; } } } } }
                if(Pan1506==turn) 
                { if(Pan1507==turn) 
                { if(Pan1508==turn) 
                { if(Pan1509==turn) 
                { if(Pan1510==turn) 
                { win++; } } } } }
                if(Pan1507==turn) 
                { if(Pan1508==turn) 
                { if(Pan1509==turn) 
                { if(Pan1510==turn) 
                { if(Pan1511==turn) 
                { win++; } } } } }
                if(Pan1508==turn) 
                { if(Pan1509==turn) 
                { if(Pan1510==turn) 
                { if(Pan1511==turn) 
                { if(Pan1512==turn) 
                { win++; } } } } }
                if(Pan1509==turn) 
                { if(Pan1510==turn) 
                { if(Pan1511==turn) 
                { if(Pan1512==turn) 
                { if(Pan1513==turn) 
                { win++; } } } } }
                if(Pan1510==turn) 
                { if(Pan1511==turn) 
                { if(Pan1512==turn) 
                { if(Pan1513==turn) 
                { if(Pan1514==turn) 
                { win++; } } } } }
                if(Pan1511==turn) 
                { if(Pan1512==turn) 
                { if(Pan1513==turn) 
                { if(Pan1514==turn) 
                { if(Pan1515==turn) 
                { win++; } } } } }
                if(Pan1512==turn) 
                { if(Pan1513==turn) 
                { if(Pan1514==turn) 
                { if(Pan1515==turn) 
                { if(Pan1516==turn) 
                { win++; } } } } }
                if(Pan1513==turn) 
                { if(Pan1514==turn) 
                { if(Pan1515==turn) 
                { if(Pan1516==turn) 
                { if(Pan1517==turn) 
                { win++; } } } } }
                if(Pan1514==turn) 
                { if(Pan1515==turn) 
                { if(Pan1516==turn) 
                { if(Pan1517==turn) 
                { if(Pan1518==turn) 
                { win++; } } } } }
                if(Pan1515==turn) 
                { if(Pan1516==turn) 
                { if(Pan1517==turn) 
                { if(Pan1518==turn) 
                { if(Pan1519==turn) 
                { win++; } } } } }
                if(Pan1601==turn) 
                { if(Pan1602==turn) 
                { if(Pan1603==turn) 
                { if(Pan1604==turn) 
                { if(Pan1605==turn) 
                { win++; } } } } }
                if(Pan1602==turn) 
                { if(Pan1603==turn) 
                { if(Pan1604==turn) 
                { if(Pan1605==turn) 
                { if(Pan1606==turn) 
                { win++; } } } } }
                if(Pan1603==turn) 
                { if(Pan1604==turn) 
                { if(Pan1605==turn) 
                { if(Pan1606==turn) 
                { if(Pan1607==turn) 
                { win++; } } } } }
                if(Pan1604==turn) 
                { if(Pan1605==turn) 
                { if(Pan1606==turn) 
                { if(Pan1607==turn) 
                { if(Pan1608==turn) 
                { win++; } } } } }
                if(Pan1605==turn) 
                { if(Pan1606==turn) 
                { if(Pan1607==turn) 
                { if(Pan1608==turn) 
                { if(Pan1609==turn) 
                { win++; } } } } }
                if(Pan1606==turn) 
                { if(Pan1607==turn) 
                { if(Pan1608==turn) 
                { if(Pan1609==turn) 
                { if(Pan1610==turn) 
                { win++; } } } } }
                if(Pan1607==turn) 
                { if(Pan1608==turn) 
                { if(Pan1609==turn) 
                { if(Pan1610==turn) 
                { if(Pan1611==turn) 
                { win++; } } } } }
                if(Pan1608==turn) 
                { if(Pan1609==turn) 
                { if(Pan1610==turn) 
                { if(Pan1611==turn) 
                { if(Pan1612==turn) 
                { win++; } } } } }
                if(Pan1609==turn) 
                { if(Pan1610==turn) 
                { if(Pan1611==turn) 
                { if(Pan1612==turn) 
                { if(Pan1613==turn) 
                { win++; } } } } }
                if(Pan1610==turn) 
                { if(Pan1611==turn) 
                { if(Pan1612==turn) 
                { if(Pan1613==turn) 
                { if(Pan1614==turn) 
                { win++; } } } } }
                if(Pan1611==turn) 
                { if(Pan1612==turn) 
                { if(Pan1613==turn) 
                { if(Pan1614==turn) 
                { if(Pan1615==turn) 
                { win++; } } } } }
                if(Pan1612==turn) 
                { if(Pan1613==turn) 
                { if(Pan1614==turn) 
                { if(Pan1615==turn) 
                { if(Pan1616==turn) 
                { win++; } } } } }
                if(Pan1613==turn) 
                { if(Pan1614==turn) 
                { if(Pan1615==turn) 
                { if(Pan1616==turn) 
                { if(Pan1617==turn) 
                { win++; } } } } }
                if(Pan1614==turn) 
                { if(Pan1615==turn) 
                { if(Pan1616==turn) 
                { if(Pan1617==turn) 
                { if(Pan1618==turn) 
                { win++; } } } } }
                if(Pan1615==turn) 
                { if(Pan1616==turn) 
                { if(Pan1617==turn) 
                { if(Pan1618==turn) 
                { if(Pan1619==turn) 
                { win++; } } } } }
                if(Pan1701==turn) 
                { if(Pan1702==turn) 
                { if(Pan1703==turn) 
                { if(Pan1704==turn) 
                { if(Pan1705==turn) 
                { win++; } } } } }
                if(Pan1702==turn) 
                { if(Pan1703==turn) 
                { if(Pan1704==turn) 
                { if(Pan1705==turn) 
                { if(Pan1706==turn) 
                { win++; } } } } }
                if(Pan1703==turn) 
                { if(Pan1704==turn) 
                { if(Pan1705==turn) 
                { if(Pan1706==turn) 
                { if(Pan1707==turn) 
                { win++; } } } } }
                if(Pan1704==turn) 
                { if(Pan1705==turn) 
                { if(Pan1706==turn) 
                { if(Pan1707==turn) 
                { if(Pan1708==turn) 
                { win++; } } } } }
                if(Pan1705==turn) 
                { if(Pan1706==turn) 
                { if(Pan1707==turn) 
                { if(Pan1708==turn) 
                { if(Pan1709==turn) 
                { win++; } } } } }
                if(Pan1706==turn) 
                { if(Pan1707==turn) 
                { if(Pan1708==turn) 
                { if(Pan1709==turn) 
                { if(Pan1710==turn) 
                { win++; } } } } }
                if(Pan1707==turn) 
                { if(Pan1708==turn) 
                { if(Pan1709==turn) 
                { if(Pan1710==turn) 
                { if(Pan1711==turn) 
                { win++; } } } } }
                if(Pan1708==turn) 
                { if(Pan1709==turn) 
                { if(Pan1710==turn) 
                { if(Pan1711==turn) 
                { if(Pan1712==turn) 
                { win++; } } } } }
                if(Pan1709==turn) 
                { if(Pan1710==turn) 
                { if(Pan1711==turn) 
                { if(Pan1712==turn) 
                { if(Pan1713==turn) 
                { win++; } } } } }
                if(Pan1710==turn) 
                { if(Pan1711==turn) 
                { if(Pan1712==turn) 
                { if(Pan1713==turn) 
                { if(Pan1714==turn) 
                { win++; } } } } }
                if(Pan1711==turn) 
                { if(Pan1712==turn) 
                { if(Pan1713==turn) 
                { if(Pan1714==turn) 
                { if(Pan1715==turn) 
                { win++; } } } } }
                if(Pan1712==turn) 
                { if(Pan1713==turn) 
                { if(Pan1714==turn) 
                { if(Pan1715==turn) 
                { if(Pan1716==turn) 
                { win++; } } } } }
                if(Pan1713==turn) 
                { if(Pan1714==turn) 
                { if(Pan1715==turn) 
                { if(Pan1716==turn) 
                { if(Pan1717==turn) 
                { win++; } } } } }
                if(Pan1714==turn) 
                { if(Pan1715==turn) 
                { if(Pan1716==turn) 
                { if(Pan1717==turn) 
                { if(Pan1718==turn) 
                { win++; } } } } }
                if(Pan1715==turn) 
                { if(Pan1716==turn) 
                { if(Pan1717==turn) 
                { if(Pan1718==turn) 
                { if(Pan1719==turn) 
                { win++; } } } } }
                if(Pan1801==turn) 
                { if(Pan1802==turn) 
                { if(Pan1803==turn) 
                { if(Pan1804==turn) 
                { if(Pan1805==turn) 
                { win++; } } } } }
                if(Pan1802==turn) 
                { if(Pan1803==turn) 
                { if(Pan1804==turn) 
                { if(Pan1805==turn) 
                { if(Pan1806==turn) 
                { win++; } } } } }
                if(Pan1803==turn) 
                { if(Pan1804==turn) 
                { if(Pan1805==turn) 
                { if(Pan1806==turn) 
                { if(Pan1807==turn) 
                { win++; } } } } }
                if(Pan1804==turn) 
                { if(Pan1805==turn) 
                { if(Pan1806==turn) 
                { if(Pan1807==turn) 
                { if(Pan1808==turn) 
                { win++; } } } } }
                if(Pan1805==turn) 
                { if(Pan1806==turn) 
                { if(Pan1807==turn) 
                { if(Pan1808==turn) 
                { if(Pan1809==turn) 
                { win++; } } } } }
                if(Pan1806==turn) 
                { if(Pan1807==turn) 
                { if(Pan1808==turn) 
                { if(Pan1809==turn) 
                { if(Pan1810==turn) 
                { win++; } } } } }
                if(Pan1807==turn) 
                { if(Pan1808==turn) 
                { if(Pan1809==turn) 
                { if(Pan1810==turn) 
                { if(Pan1811==turn) 
                { win++; } } } } }
                if(Pan1808==turn) 
                { if(Pan1809==turn) 
                { if(Pan1810==turn) 
                { if(Pan1811==turn) 
                { if(Pan1812==turn) 
                { win++; } } } } }
                if(Pan1809==turn) 
                { if(Pan1810==turn) 
                { if(Pan1811==turn) 
                { if(Pan1812==turn) 
                { if(Pan1813==turn) 
                { win++; } } } } }
                if(Pan1810==turn) 
                { if(Pan1811==turn) 
                { if(Pan1812==turn) 
                { if(Pan1813==turn) 
                { if(Pan1814==turn) 
                { win++; } } } } }
                if(Pan1811==turn) 
                { if(Pan1812==turn) 
                { if(Pan1813==turn) 
                { if(Pan1814==turn) 
                { if(Pan1815==turn) 
                { win++; } } } } }
                if(Pan1812==turn) 
                { if(Pan1813==turn) 
                { if(Pan1814==turn) 
                { if(Pan1815==turn) 
                { if(Pan1816==turn) 
                { win++; } } } } }
                if(Pan1813==turn) 
                { if(Pan1814==turn) 
                { if(Pan1815==turn) 
                { if(Pan1816==turn) 
                { if(Pan1817==turn) 
                { win++; } } } } }
                if(Pan1814==turn) 
                { if(Pan1815==turn) 
                { if(Pan1816==turn) 
                { if(Pan1817==turn) 
                { if(Pan1818==turn) 
                { win++; } } } } }
                if(Pan1815==turn) 
                { if(Pan1816==turn) 
                { if(Pan1817==turn) 
                { if(Pan1818==turn) 
                { if(Pan1819==turn) 
                { win++; } } } } }
                if(Pan1901==turn) 
                { if(Pan1902==turn) 
                { if(Pan1903==turn) 
                { if(Pan1904==turn) 
                { if(Pan1905==turn) 
                { win++; } } } } }
                if(Pan1902==turn) 
                { if(Pan1903==turn) 
                { if(Pan1904==turn) 
                { if(Pan1905==turn) 
                { if(Pan1906==turn) 
                { win++; } } } } }
                if(Pan1903==turn) 
                { if(Pan1904==turn) 
                { if(Pan1905==turn) 
                { if(Pan1906==turn) 
                { if(Pan1907==turn) 
                { win++; } } } } }
                if(Pan1904==turn) 
                { if(Pan1905==turn) 
                { if(Pan1906==turn) 
                { if(Pan1907==turn) 
                { if(Pan1908==turn) 
                { win++; } } } } }
                if(Pan1905==turn) 
                { if(Pan1906==turn) 
                { if(Pan1907==turn) 
                { if(Pan1908==turn) 
                { if(Pan1909==turn) 
                { win++; } } } } }
                if(Pan1906==turn) 
                { if(Pan1907==turn) 
                { if(Pan1908==turn) 
                { if(Pan1909==turn) 
                { if(Pan1910==turn) 
                { win++; } } } } }
                if(Pan1907==turn) 
                { if(Pan1908==turn) 
                { if(Pan1909==turn) 
                { if(Pan1910==turn) 
                { if(Pan1911==turn) 
                { win++; } } } } }
                if(Pan1908==turn) 
                { if(Pan1909==turn) 
                { if(Pan1910==turn) 
                { if(Pan1911==turn) 
                { if(Pan1912==turn) 
                { win++; } } } } }
                if(Pan1909==turn) 
                { if(Pan1910==turn) 
                { if(Pan1911==turn) 
                { if(Pan1912==turn) 
                { if(Pan1913==turn) 
                { win++; } } } } }
                if(Pan1910==turn) 
                { if(Pan1911==turn) 
                { if(Pan1912==turn) 
                { if(Pan1913==turn) 
                { if(Pan1914==turn) 
                { win++; } } } } }
                if(Pan1911==turn) 
                { if(Pan1912==turn) 
                { if(Pan1913==turn) 
                { if(Pan1914==turn) 
                { if(Pan1915==turn) 
                { win++; } } } } }
                if(Pan1912==turn) 
                { if(Pan1913==turn) 
                { if(Pan1914==turn) 
                { if(Pan1915==turn) 
                { if(Pan1916==turn) 
                { win++; } } } } }
                if(Pan1913==turn) 
                { if(Pan1914==turn) 
                { if(Pan1915==turn) 
                { if(Pan1916==turn) 
                { if(Pan1917==turn) 
                { win++; } } } } }
                if(Pan1914==turn) 
                { if(Pan1915==turn) 
                { if(Pan1916==turn) 
                { if(Pan1917==turn) 
                { if(Pan1918==turn) 
                { win++; } } } } }
                if(Pan1915==turn) 
                { if(Pan1916==turn) 
                { if(Pan1917==turn) 
                { if(Pan1918==turn) 
                { if(Pan1919==turn) 
                { win++; } } } } }

                /////////////////// 세로 검사 ////////////////////////////////////
                if(Pan0101==turn) 
                { if(Pan0201==turn) 
                { if(Pan0301==turn) 
                { if(Pan0401==turn) 
                { if(Pan0501==turn) 
                { win++; } } } } }
                if(Pan0102==turn) 
                { if(Pan0202==turn) 
                { if(Pan0302==turn) 
                { if(Pan0402==turn) 
                { if(Pan0502==turn) 
                { win++; } } } } }
                if(Pan0103==turn) 
                { if(Pan0203==turn) 
                { if(Pan0303==turn) 
                { if(Pan0403==turn) 
                { if(Pan0503==turn) 
                { win++; } } } } }
                if(Pan0104==turn) 
                { if(Pan0204==turn) 
                { if(Pan0304==turn) 
                { if(Pan0404==turn) 
                { if(Pan0504==turn) 
                { win++; } } } } }
                if(Pan0105==turn) 
                { if(Pan0205==turn) 
                { if(Pan0305==turn) 
                { if(Pan0405==turn) 
                { if(Pan0505==turn) 
                { win++; } } } } }
                if(Pan0106==turn) 
                { if(Pan0206==turn) 
                { if(Pan0306==turn) 
                { if(Pan0406==turn) 
                { if(Pan0506==turn) 
                { win++; } } } } }
                if(Pan0107==turn) 
                { if(Pan0207==turn) 
                { if(Pan0307==turn) 
                { if(Pan0407==turn) 
                { if(Pan0507==turn) 
                { win++; } } } } }
                if(Pan0108==turn) 
                { if(Pan0208==turn) 
                { if(Pan0308==turn) 
                { if(Pan0408==turn) 
                { if(Pan0508==turn) 
                { win++; } } } } }
                if(Pan0109==turn) 
                { if(Pan0209==turn) 
                { if(Pan0309==turn) 
                { if(Pan0409==turn) 
                { if(Pan0509==turn) 
                { win++; } } } } }
                if(Pan0110==turn) 
                { if(Pan0210==turn) 
                { if(Pan0310==turn) 
                { if(Pan0410==turn) 
                { if(Pan0510==turn) 
                { win++; } } } } }
                if(Pan0111==turn) 
                { if(Pan0211==turn) 
                { if(Pan0311==turn) 
                { if(Pan0411==turn) 
                { if(Pan0511==turn) 
                { win++; } } } } }
                if(Pan0112==turn) 
                { if(Pan0212==turn) 
                { if(Pan0312==turn) 
                { if(Pan0412==turn) 
                { if(Pan0512==turn) 
                { win++; } } } } }
                if(Pan0113==turn) 
                { if(Pan0213==turn) 
                { if(Pan0313==turn) 
                { if(Pan0413==turn) 
                { if(Pan0513==turn) 
                { win++; } } } } }
                if(Pan0114==turn) 
                { if(Pan0214==turn) 
                { if(Pan0314==turn) 
                { if(Pan0414==turn) 
                { if(Pan0514==turn) 
                { win++; } } } } }
                if(Pan0115==turn) 
                { if(Pan0215==turn) 
                { if(Pan0315==turn) 
                { if(Pan0415==turn) 
                { if(Pan0515==turn) 
                { win++; } } } } }
                if(Pan0116==turn) 
                { if(Pan0216==turn) 
                { if(Pan0316==turn) 
                { if(Pan0416==turn) 
                { if(Pan0516==turn) 
                { win++; } } } } }
                if(Pan0117==turn) 
                { if(Pan0217==turn) 
                { if(Pan0317==turn) 
                { if(Pan0417==turn) 
                { if(Pan0517==turn) 
                { win++; } } } } }
                if(Pan0118==turn) 
                { if(Pan0218==turn) 
                { if(Pan0318==turn) 
                { if(Pan0418==turn) 
                { if(Pan0518==turn) 
                { win++; } } } } }
                if(Pan0119==turn) 
                { if(Pan0219==turn) 
                { if(Pan0319==turn) 
                { if(Pan0419==turn) 
                { if(Pan0519==turn) 
                { win++; } } } } }
                if(Pan0201==turn) 
                { if(Pan0301==turn) 
                { if(Pan0401==turn) 
                { if(Pan0501==turn) 
                { if(Pan0601==turn) 
                { win++; } } } } }
                if(Pan0202==turn) 
                { if(Pan0302==turn) 
                { if(Pan0402==turn) 
                { if(Pan0502==turn) 
                { if(Pan0602==turn) 
                { win++; } } } } }
                if(Pan0203==turn) 
                { if(Pan0303==turn) 
                { if(Pan0403==turn) 
                { if(Pan0503==turn) 
                { if(Pan0603==turn) 
                { win++; } } } } }
                if(Pan0204==turn) 
                { if(Pan0304==turn) 
                { if(Pan0404==turn) 
                { if(Pan0504==turn) 
                { if(Pan0604==turn) 
                { win++; } } } } }
                if(Pan0205==turn) 
                { if(Pan0305==turn) 
                { if(Pan0405==turn) 
                { if(Pan0505==turn) 
                { if(Pan0605==turn) 
                { win++; } } } } }
                if(Pan0206==turn) 
                { if(Pan0306==turn) 
                { if(Pan0406==turn) 
                { if(Pan0506==turn) 
                { if(Pan0606==turn) 
                { win++; } } } } }
                if(Pan0207==turn) 
                { if(Pan0307==turn) 
                { if(Pan0407==turn) 
                { if(Pan0507==turn) 
                { if(Pan0607==turn) 
                { win++; } } } } }
                if(Pan0208==turn) 
                { if(Pan0308==turn) 
                { if(Pan0408==turn) 
                { if(Pan0508==turn) 
                { if(Pan0608==turn) 
                { win++; } } } } }
                if(Pan0209==turn) 
                { if(Pan0309==turn) 
                { if(Pan0409==turn) 
                { if(Pan0509==turn) 
                { if(Pan0609==turn) 
                { win++; } } } } }
                if(Pan0210==turn) 
                { if(Pan0310==turn) 
                { if(Pan0410==turn) 
                { if(Pan0510==turn) 
                { if(Pan0610==turn) 
                { win++; } } } } }
                if(Pan0211==turn) 
                { if(Pan0311==turn) 
                { if(Pan0411==turn) 
                { if(Pan0511==turn) 
                { if(Pan0611==turn) 
                { win++; } } } } }
                if(Pan0212==turn) 
                { if(Pan0312==turn) 
                { if(Pan0412==turn) 
                { if(Pan0512==turn) 
                { if(Pan0612==turn) 
                { win++; } } } } }
                if(Pan0213==turn) 
                { if(Pan0313==turn) 
                { if(Pan0413==turn) 
                { if(Pan0513==turn) 
                { if(Pan0613==turn) 
                { win++; } } } } }
                if(Pan0214==turn) 
                { if(Pan0314==turn) 
                { if(Pan0414==turn) 
                { if(Pan0514==turn) 
                { if(Pan0614==turn) 
                { win++; } } } } }
                if(Pan0215==turn) 
                { if(Pan0315==turn) 
                { if(Pan0415==turn) 
                { if(Pan0515==turn) 
                { if(Pan0615==turn) 
                { win++; } } } } }
                if(Pan0216==turn) 
                { if(Pan0316==turn) 
                { if(Pan0416==turn) 
                { if(Pan0516==turn) 
                { if(Pan0616==turn) 
                { win++; } } } } }
                if(Pan0217==turn) 
                { if(Pan0317==turn) 
                { if(Pan0417==turn) 
                { if(Pan0517==turn) 
                { if(Pan0617==turn) 
                { win++; } } } } }
                if(Pan0218==turn) 
                { if(Pan0318==turn) 
                { if(Pan0418==turn) 
                { if(Pan0518==turn) 
                { if(Pan0618==turn) 
                { win++; } } } } }
                if(Pan0219==turn) 
                { if(Pan0319==turn) 
                { if(Pan0419==turn) 
                { if(Pan0519==turn) 
                { if(Pan0619==turn) 
                { win++; } } } } }
                if(Pan0301==turn) 
                { if(Pan0401==turn) 
                { if(Pan0501==turn) 
                { if(Pan0601==turn) 
                { if(Pan0701==turn) 
                { win++; } } } } }
                if(Pan0302==turn) 
                { if(Pan0402==turn) 
                { if(Pan0502==turn) 
                { if(Pan0602==turn) 
                { if(Pan0702==turn) 
                { win++; } } } } }
                if(Pan0303==turn) 
                { if(Pan0403==turn) 
                { if(Pan0503==turn) 
                { if(Pan0603==turn) 
                { if(Pan0703==turn) 
                { win++; } } } } }
                if(Pan0304==turn) 
                { if(Pan0404==turn) 
                { if(Pan0504==turn) 
                { if(Pan0604==turn) 
                { if(Pan0704==turn) 
                { win++; } } } } }
                if(Pan0305==turn) 
                { if(Pan0405==turn) 
                { if(Pan0505==turn) 
                { if(Pan0605==turn) 
                { if(Pan0705==turn) 
                { win++; } } } } }
                if(Pan0306==turn) 
                { if(Pan0406==turn) 
                { if(Pan0506==turn) 
                { if(Pan0606==turn) 
                { if(Pan0706==turn) 
                { win++; } } } } }
                if(Pan0307==turn) 
                { if(Pan0407==turn) 
                { if(Pan0507==turn) 
                { if(Pan0607==turn) 
                { if(Pan0707==turn) 
                { win++; } } } } }
                if(Pan0308==turn) 
                { if(Pan0408==turn) 
                { if(Pan0508==turn) 
                { if(Pan0608==turn) 
                { if(Pan0708==turn) 
                { win++; } } } } }
                if(Pan0309==turn) 
                { if(Pan0409==turn) 
                { if(Pan0509==turn) 
                { if(Pan0609==turn) 
                { if(Pan0709==turn) 
                { win++; } } } } }
                if(Pan0310==turn) 
                { if(Pan0410==turn) 
                { if(Pan0510==turn) 
                { if(Pan0610==turn) 
                { if(Pan0710==turn) 
                { win++; } } } } }
                if(Pan0311==turn) 
                { if(Pan0411==turn) 
                { if(Pan0511==turn) 
                { if(Pan0611==turn) 
                { if(Pan0711==turn) 
                { win++; } } } } }
                if(Pan0312==turn) 
                { if(Pan0412==turn) 
                { if(Pan0512==turn) 
                { if(Pan0612==turn) 
                { if(Pan0712==turn) 
                { win++; } } } } }
                if(Pan0313==turn) 
                { if(Pan0413==turn) 
                { if(Pan0513==turn) 
                { if(Pan0613==turn) 
                { if(Pan0713==turn) 
                { win++; } } } } }
                if(Pan0314==turn) 
                { if(Pan0414==turn) 
                { if(Pan0514==turn) 
                { if(Pan0614==turn) 
                { if(Pan0714==turn) 
                { win++; } } } } }
                if(Pan0315==turn) 
                { if(Pan0415==turn) 
                { if(Pan0515==turn) 
                { if(Pan0615==turn) 
                { if(Pan0715==turn) 
                { win++; } } } } }
                if(Pan0316==turn) 
                { if(Pan0416==turn) 
                { if(Pan0516==turn) 
                { if(Pan0616==turn) 
                { if(Pan0716==turn) 
                { win++; } } } } }
                if(Pan0317==turn) 
                { if(Pan0417==turn) 
                { if(Pan0517==turn) 
                { if(Pan0617==turn) 
                { if(Pan0717==turn) 
                { win++; } } } } }
                if(Pan0318==turn) 
                { if(Pan0418==turn) 
                { if(Pan0518==turn) 
                { if(Pan0618==turn) 
                { if(Pan0718==turn) 
                { win++; } } } } }
                if(Pan0319==turn) 
                { if(Pan0419==turn) 
                { if(Pan0519==turn) 
                { if(Pan0619==turn) 
                { if(Pan0719==turn) 
                { win++; } } } } }
                if(Pan0401==turn) 
                { if(Pan0501==turn) 
                { if(Pan0601==turn) 
                { if(Pan0701==turn) 
                { if(Pan0801==turn) 
                { win++; } } } } }
                if(Pan0402==turn) 
                { if(Pan0502==turn) 
                { if(Pan0602==turn) 
                { if(Pan0702==turn) 
                { if(Pan0802==turn) 
                { win++; } } } } }
                if(Pan0403==turn) 
                { if(Pan0503==turn) 
                { if(Pan0603==turn) 
                { if(Pan0703==turn) 
                { if(Pan0803==turn) 
                { win++; } } } } }
                if(Pan0404==turn) 
                { if(Pan0504==turn) 
                { if(Pan0604==turn) 
                { if(Pan0704==turn) 
                { if(Pan0804==turn) 
                { win++; } } } } }
                if(Pan0405==turn) 
                { if(Pan0505==turn) 
                { if(Pan0605==turn) 
                { if(Pan0705==turn) 
                { if(Pan0805==turn) 
                { win++; } } } } }
                if(Pan0406==turn) 
                { if(Pan0506==turn) 
                { if(Pan0606==turn) 
                { if(Pan0706==turn) 
                { if(Pan0806==turn) 
                { win++; } } } } }
                if(Pan0407==turn) 
                { if(Pan0507==turn) 
                { if(Pan0607==turn) 
                { if(Pan0707==turn) 
                { if(Pan0807==turn) 
                { win++; } } } } }
                if(Pan0408==turn) 
                { if(Pan0508==turn) 
                { if(Pan0608==turn) 
                { if(Pan0708==turn) 
                { if(Pan0808==turn) 
                { win++; } } } } }
                if(Pan0409==turn) 
                { if(Pan0509==turn) 
                { if(Pan0609==turn) 
                { if(Pan0709==turn) 
                { if(Pan0809==turn) 
                { win++; } } } } }
                if(Pan0410==turn) 
                { if(Pan0510==turn) 
                { if(Pan0610==turn) 
                { if(Pan0710==turn) 
                { if(Pan0810==turn) 
                { win++; } } } } }
                if(Pan0411==turn) 
                { if(Pan0511==turn) 
                { if(Pan0611==turn) 
                { if(Pan0711==turn) 
                { if(Pan0811==turn) 
                { win++; } } } } }
                if(Pan0412==turn) 
                { if(Pan0512==turn) 
                { if(Pan0612==turn) 
                { if(Pan0712==turn) 
                { if(Pan0812==turn) 
                { win++; } } } } }
                if(Pan0413==turn) 
                { if(Pan0513==turn) 
                { if(Pan0613==turn) 
                { if(Pan0713==turn) 
                { if(Pan0813==turn) 
                { win++; } } } } }
                if(Pan0414==turn) 
                { if(Pan0514==turn) 
                { if(Pan0614==turn) 
                { if(Pan0714==turn) 
                { if(Pan0814==turn) 
                { win++; } } } } }
                if(Pan0415==turn) 
                { if(Pan0515==turn) 
                { if(Pan0615==turn) 
                { if(Pan0715==turn) 
                { if(Pan0815==turn) 
                { win++; } } } } }
                if(Pan0416==turn) 
                { if(Pan0516==turn) 
                { if(Pan0616==turn) 
                { if(Pan0716==turn) 
                { if(Pan0816==turn) 
                { win++; } } } } }
                if(Pan0417==turn) 
                { if(Pan0517==turn) 
                { if(Pan0617==turn) 
                { if(Pan0717==turn) 
                { if(Pan0817==turn) 
                { win++; } } } } }
                if(Pan0418==turn) 
                { if(Pan0518==turn) 
                { if(Pan0618==turn) 
                { if(Pan0718==turn) 
                { if(Pan0818==turn) 
                { win++; } } } } }
                if(Pan0419==turn) 
                { if(Pan0519==turn) 
                { if(Pan0619==turn) 
                { if(Pan0719==turn) 
                { if(Pan0819==turn) 
                { win++; } } } } }
                if(Pan0501==turn) 
                { if(Pan0601==turn) 
                { if(Pan0701==turn) 
                { if(Pan0801==turn) 
                { if(Pan0901==turn) 
                { win++; } } } } }
                if(Pan0502==turn) 
                { if(Pan0602==turn) 
                { if(Pan0702==turn) 
                { if(Pan0802==turn) 
                { if(Pan0902==turn) 
                { win++; } } } } }
                if(Pan0503==turn) 
                { if(Pan0603==turn) 
                { if(Pan0703==turn) 
                { if(Pan0803==turn) 
                { if(Pan0903==turn) 
                { win++; } } } } }
                if(Pan0504==turn) 
                { if(Pan0604==turn) 
                { if(Pan0704==turn) 
                { if(Pan0804==turn) 
                { if(Pan0904==turn) 
                { win++; } } } } }
                if(Pan0505==turn) 
                { if(Pan0605==turn) 
                { if(Pan0705==turn) 
                { if(Pan0805==turn) 
                { if(Pan0905==turn) 
                { win++; } } } } }
                if(Pan0506==turn) 
                { if(Pan0606==turn) 
                { if(Pan0706==turn) 
                { if(Pan0806==turn) 
                { if(Pan0906==turn) 
                { win++; } } } } }
                if(Pan0507==turn) 
                { if(Pan0607==turn) 
                { if(Pan0707==turn) 
                { if(Pan0807==turn) 
                { if(Pan0907==turn) 
                { win++; } } } } }
                if(Pan0508==turn) 
                { if(Pan0608==turn) 
                { if(Pan0708==turn) 
                { if(Pan0808==turn) 
                { if(Pan0908==turn) 
                { win++; } } } } }
                if(Pan0509==turn) 
                { if(Pan0609==turn) 
                { if(Pan0709==turn) 
                { if(Pan0809==turn) 
                { if(Pan0909==turn) 
                { win++; } } } } }
                if(Pan0510==turn) 
                { if(Pan0610==turn) 
                { if(Pan0710==turn) 
                { if(Pan0810==turn) 
                { if(Pan0910==turn) 
                { win++; } } } } }
                if(Pan0511==turn) 
                { if(Pan0611==turn) 
                { if(Pan0711==turn) 
                { if(Pan0811==turn) 
                { if(Pan0911==turn) 
                { win++; } } } } }
                if(Pan0512==turn) 
                { if(Pan0612==turn) 
                { if(Pan0712==turn) 
                { if(Pan0812==turn) 
                { if(Pan0912==turn) 
                { win++; } } } } }
                if(Pan0513==turn) 
                { if(Pan0613==turn) 
                { if(Pan0713==turn) 
                { if(Pan0813==turn) 
                { if(Pan0913==turn) 
                { win++; } } } } }
                if(Pan0514==turn) 
                { if(Pan0614==turn) 
                { if(Pan0714==turn) 
                { if(Pan0814==turn) 
                { if(Pan0914==turn) 
                { win++; } } } } }
                if(Pan0515==turn) 
                { if(Pan0615==turn) 
                { if(Pan0715==turn) 
                { if(Pan0815==turn) 
                { if(Pan0915==turn) 
                { win++; } } } } }
                if(Pan0516==turn) 
                { if(Pan0616==turn) 
                { if(Pan0716==turn) 
                { if(Pan0816==turn) 
                { if(Pan0916==turn) 
                { win++; } } } } }
                if(Pan0517==turn) 
                { if(Pan0617==turn) 
                { if(Pan0717==turn) 
                { if(Pan0817==turn) 
                { if(Pan0917==turn) 
                { win++; } } } } }
                if(Pan0518==turn) 
                { if(Pan0618==turn) 
                { if(Pan0718==turn) 
                { if(Pan0818==turn) 
                { if(Pan0918==turn) 
                { win++; } } } } }
                if(Pan0519==turn) 
                { if(Pan0619==turn) 
                { if(Pan0719==turn) 
                { if(Pan0819==turn) 
                { if(Pan0919==turn) 
                { win++; } } } } }
                if(Pan0601==turn) 
                { if(Pan0701==turn) 
                { if(Pan0801==turn) 
                { if(Pan0901==turn) 
                { if(Pan1001==turn) 
                { win++; } } } } }
                if(Pan0602==turn) 
                { if(Pan0702==turn) 
                { if(Pan0802==turn) 
                { if(Pan0902==turn) 
                { if(Pan1002==turn) 
                { win++; } } } } }
                if(Pan0603==turn) 
                { if(Pan0703==turn) 
                { if(Pan0803==turn) 
                { if(Pan0903==turn) 
                { if(Pan1003==turn) 
                { win++; } } } } }
                if(Pan0604==turn) 
                { if(Pan0704==turn) 
                { if(Pan0804==turn) 
                { if(Pan0904==turn) 
                { if(Pan1004==turn) 
                { win++; } } } } }
                if(Pan0605==turn) 
                { if(Pan0705==turn) 
                { if(Pan0805==turn) 
                { if(Pan0905==turn) 
                { if(Pan1005==turn) 
                { win++; } } } } }
                if(Pan0606==turn) 
                { if(Pan0706==turn) 
                { if(Pan0806==turn) 
                { if(Pan0906==turn) 
                { if(Pan1006==turn) 
                { win++; } } } } }
                if(Pan0607==turn) 
                { if(Pan0707==turn) 
                { if(Pan0807==turn) 
                { if(Pan0907==turn) 
                { if(Pan1007==turn) 
                { win++; } } } } }
                if(Pan0608==turn) 
                { if(Pan0708==turn) 
                { if(Pan0808==turn) 
                { if(Pan0908==turn) 
                { if(Pan1008==turn) 
                { win++; } } } } }
                if(Pan0609==turn) 
                { if(Pan0709==turn) 
                { if(Pan0809==turn) 
                { if(Pan0909==turn) 
                { if(Pan1009==turn) 
                { win++; } } } } }
                if(Pan0610==turn) 
                { if(Pan0710==turn) 
                { if(Pan0810==turn) 
                { if(Pan0910==turn) 
                { if(Pan1010==turn) 
                { win++; } } } } }
                if(Pan0611==turn) 
                { if(Pan0711==turn) 
                { if(Pan0811==turn) 
                { if(Pan0911==turn) 
                { if(Pan1011==turn) 
                { win++; } } } } }
                if(Pan0612==turn) 
                { if(Pan0712==turn) 
                { if(Pan0812==turn) 
                { if(Pan0912==turn) 
                { if(Pan1012==turn) 
                { win++; } } } } }
                if(Pan0613==turn) 
                { if(Pan0713==turn) 
                { if(Pan0813==turn) 
                { if(Pan0913==turn) 
                { if(Pan1013==turn) 
                { win++; } } } } }
                if(Pan0614==turn) 
                { if(Pan0714==turn) 
                { if(Pan0814==turn) 
                { if(Pan0914==turn) 
                { if(Pan1014==turn) 
                { win++; } } } } }
                if(Pan0615==turn) 
                { if(Pan0715==turn) 
                { if(Pan0815==turn) 
                { if(Pan0915==turn) 
                { if(Pan1015==turn) 
                { win++; } } } } }
                if(Pan0616==turn) 
                { if(Pan0716==turn) 
                { if(Pan0816==turn) 
                { if(Pan0916==turn) 
                { if(Pan1016==turn) 
                { win++; } } } } }
                if(Pan0617==turn) 
                { if(Pan0717==turn) 
                { if(Pan0817==turn) 
                { if(Pan0917==turn) 
                { if(Pan1017==turn) 
                { win++; } } } } }
                if(Pan0618==turn) 
                { if(Pan0718==turn) 
                { if(Pan0818==turn) 
                { if(Pan0918==turn) 
                { if(Pan1018==turn) 
                { win++; } } } } }
                if(Pan0619==turn) 
                { if(Pan0719==turn) 
                { if(Pan0819==turn) 
                { if(Pan0919==turn) 
                { if(Pan1019==turn) 
                { win++; } } } } }
                if(Pan0701==turn) 
                { if(Pan0801==turn) 
                { if(Pan0901==turn) 
                { if(Pan1001==turn) 
                { if(Pan1101==turn) 
                { win++; } } } } }
                if(Pan0702==turn) 
                { if(Pan0802==turn) 
                { if(Pan0902==turn) 
                { if(Pan1002==turn) 
                { if(Pan1102==turn) 
                { win++; } } } } }
                if(Pan0703==turn) 
                { if(Pan0803==turn) 
                { if(Pan0903==turn) 
                { if(Pan1003==turn) 
                { if(Pan1103==turn) 
                { win++; } } } } }
                if(Pan0704==turn) 
                { if(Pan0804==turn) 
                { if(Pan0904==turn) 
                { if(Pan1004==turn) 
                { if(Pan1104==turn) 
                { win++; } } } } }
                if(Pan0705==turn) 
                { if(Pan0805==turn) 
                { if(Pan0905==turn) 
                { if(Pan1005==turn) 
                { if(Pan1105==turn) 
                { win++; } } } } }
                if(Pan0706==turn) 
                { if(Pan0806==turn) 
                { if(Pan0906==turn) 
                { if(Pan1006==turn) 
                { if(Pan1106==turn) 
                { win++; } } } } }
                if(Pan0707==turn) 
                { if(Pan0807==turn) 
                { if(Pan0907==turn) 
                { if(Pan1007==turn) 
                { if(Pan1107==turn) 
                { win++; } } } } }
                if(Pan0708==turn) 
                { if(Pan0808==turn) 
                { if(Pan0908==turn) 
                { if(Pan1008==turn) 
                { if(Pan1108==turn) 
                { win++; } } } } }
                if(Pan0709==turn) 
                { if(Pan0809==turn) 
                { if(Pan0909==turn) 
                { if(Pan1009==turn) 
                { if(Pan1109==turn) 
                { win++; } } } } }
                if(Pan0710==turn) 
                { if(Pan0810==turn) 
                { if(Pan0910==turn) 
                { if(Pan1010==turn) 
                { if(Pan1110==turn) 
                { win++; } } } } }
                if(Pan0711==turn) 
                { if(Pan0811==turn) 
                { if(Pan0911==turn) 
                { if(Pan1011==turn) 
                { if(Pan1111==turn) 
                { win++; } } } } }
                if(Pan0712==turn) 
                { if(Pan0812==turn) 
                { if(Pan0912==turn) 
                { if(Pan1012==turn) 
                { if(Pan1112==turn) 
                { win++; } } } } }
                if(Pan0713==turn) 
                { if(Pan0813==turn) 
                { if(Pan0913==turn) 
                { if(Pan1013==turn) 
                { if(Pan1113==turn) 
                { win++; } } } } }
                if(Pan0714==turn) 
                { if(Pan0814==turn) 
                { if(Pan0914==turn) 
                { if(Pan1014==turn) 
                { if(Pan1114==turn) 
                { win++; } } } } }
                if(Pan0715==turn) 
                { if(Pan0815==turn) 
                { if(Pan0915==turn) 
                { if(Pan1015==turn) 
                { if(Pan1115==turn) 
                { win++; } } } } }
                if(Pan0716==turn) 
                { if(Pan0816==turn) 
                { if(Pan0916==turn) 
                { if(Pan1016==turn) 
                { if(Pan1116==turn) 
                { win++; } } } } }
                if(Pan0717==turn) 
                { if(Pan0817==turn) 
                { if(Pan0917==turn) 
                { if(Pan1017==turn) 
                { if(Pan1117==turn) 
                { win++; } } } } }
                if(Pan0718==turn) 
                { if(Pan0818==turn) 
                { if(Pan0918==turn) 
                { if(Pan1018==turn) 
                { if(Pan1118==turn) 
                { win++; } } } } }
                if(Pan0719==turn) 
                { if(Pan0819==turn) 
                { if(Pan0919==turn) 
                { if(Pan1019==turn) 
                { if(Pan1119==turn) 
                { win++; } } } } }
                if(Pan0801==turn) 
                { if(Pan0901==turn) 
                { if(Pan1001==turn) 
                { if(Pan1101==turn) 
                { if(Pan1201==turn) 
                { win++; } } } } }
                if(Pan0802==turn) 
                { if(Pan0902==turn) 
                { if(Pan1002==turn) 
                { if(Pan1102==turn) 
                { if(Pan1202==turn) 
                { win++; } } } } }
                if(Pan0803==turn) 
                { if(Pan0903==turn) 
                { if(Pan1003==turn) 
                { if(Pan1103==turn) 
                { if(Pan1203==turn) 
                { win++; } } } } }
                if(Pan0804==turn) 
                { if(Pan0904==turn) 
                { if(Pan1004==turn) 
                { if(Pan1104==turn) 
                { if(Pan1204==turn) 
                { win++; } } } } }
                if(Pan0805==turn) 
                { if(Pan0905==turn) 
                { if(Pan1005==turn) 
                { if(Pan1105==turn) 
                { if(Pan1205==turn) 
                { win++; } } } } }
                if(Pan0806==turn) 
                { if(Pan0906==turn) 
                { if(Pan1006==turn) 
                { if(Pan1106==turn) 
                { if(Pan1206==turn) 
                { win++; } } } } }
                if(Pan0807==turn) 
                { if(Pan0907==turn) 
                { if(Pan1007==turn) 
                { if(Pan1107==turn) 
                { if(Pan1207==turn) 
                { win++; } } } } }
                if(Pan0808==turn) 
                { if(Pan0908==turn) 
                { if(Pan1008==turn) 
                { if(Pan1108==turn) 
                { if(Pan1208==turn) 
                { win++; } } } } }
                if(Pan0809==turn) 
                { if(Pan0909==turn) 
                { if(Pan1009==turn) 
                { if(Pan1109==turn) 
                { if(Pan1209==turn) 
                { win++; } } } } }
                if(Pan0810==turn) 
                { if(Pan0910==turn) 
                { if(Pan1010==turn) 
                { if(Pan1110==turn) 
                { if(Pan1210==turn) 
                { win++; } } } } }
                if(Pan0811==turn) 
                { if(Pan0911==turn) 
                { if(Pan1011==turn) 
                { if(Pan1111==turn) 
                { if(Pan1211==turn) 
                { win++; } } } } }
                if(Pan0812==turn) 
                { if(Pan0912==turn) 
                { if(Pan1012==turn) 
                { if(Pan1112==turn) 
                { if(Pan1212==turn) 
                { win++; } } } } }
                if(Pan0813==turn) 
                { if(Pan0913==turn) 
                { if(Pan1013==turn) 
                { if(Pan1113==turn) 
                { if(Pan1213==turn) 
                { win++; } } } } }
                if(Pan0814==turn) 
                { if(Pan0914==turn) 
                { if(Pan1014==turn) 
                { if(Pan1114==turn) 
                { if(Pan1214==turn) 
                { win++; } } } } }
                if(Pan0815==turn) 
                { if(Pan0915==turn) 
                { if(Pan1015==turn) 
                { if(Pan1115==turn) 
                { if(Pan1215==turn) 
                { win++; } } } } }
                if(Pan0816==turn) 
                { if(Pan0916==turn) 
                { if(Pan1016==turn) 
                { if(Pan1116==turn) 
                { if(Pan1216==turn) 
                { win++; } } } } }
                if(Pan0817==turn) 
                { if(Pan0917==turn) 
                { if(Pan1017==turn) 
                { if(Pan1117==turn) 
                { if(Pan1217==turn) 
                { win++; } } } } }
                if(Pan0818==turn) 
                { if(Pan0918==turn) 
                { if(Pan1018==turn) 
                { if(Pan1118==turn) 
                { if(Pan1218==turn) 
                { win++; } } } } }
                if(Pan0819==turn) 
                { if(Pan0919==turn) 
                { if(Pan1019==turn) 
                { if(Pan1119==turn) 
                { if(Pan1219==turn) 
                { win++; } } } } }
                if(Pan0901==turn) 
                { if(Pan1001==turn) 
                { if(Pan1101==turn) 
                { if(Pan1201==turn) 
                { if(Pan1301==turn) 
                { win++; } } } } }
                if(Pan0902==turn) 
                { if(Pan1002==turn) 
                { if(Pan1102==turn) 
                { if(Pan1202==turn) 
                { if(Pan1302==turn) 
                { win++; } } } } }
                if(Pan0903==turn) 
                { if(Pan1003==turn) 
                { if(Pan1103==turn) 
                { if(Pan1203==turn) 
                { if(Pan1303==turn) 
                { win++; } } } } }
                if(Pan0904==turn) 
                { if(Pan1004==turn) 
                { if(Pan1104==turn) 
                { if(Pan1204==turn) 
                { if(Pan1304==turn) 
                { win++; } } } } }
                if(Pan0905==turn) 
                { if(Pan1005==turn) 
                { if(Pan1105==turn) 
                { if(Pan1205==turn) 
                { if(Pan1305==turn) 
                { win++; } } } } }
                if(Pan0906==turn) 
                { if(Pan1006==turn) 
                { if(Pan1106==turn) 
                { if(Pan1206==turn) 
                { if(Pan1306==turn) 
                { win++; } } } } }
                if(Pan0907==turn) 
                { if(Pan1007==turn) 
                { if(Pan1107==turn) 
                { if(Pan1207==turn) 
                { if(Pan1307==turn) 
                { win++; } } } } }
                if(Pan0908==turn) 
                { if(Pan1008==turn) 
                { if(Pan1108==turn) 
                { if(Pan1208==turn) 
                { if(Pan1308==turn) 
                { win++; } } } } }
                if(Pan0909==turn) 
                { if(Pan1009==turn) 
                { if(Pan1109==turn) 
                { if(Pan1209==turn) 
                { if(Pan1309==turn) 
                { win++; } } } } }
                if(Pan0910==turn) 
                { if(Pan1010==turn) 
                { if(Pan1110==turn) 
                { if(Pan1210==turn) 
                { if(Pan1310==turn) 
                { win++; } } } } }
                if(Pan0911==turn) 
                { if(Pan1011==turn) 
                { if(Pan1111==turn) 
                { if(Pan1211==turn) 
                { if(Pan1311==turn) 
                { win++; } } } } }
                if(Pan0912==turn) 
                { if(Pan1012==turn) 
                { if(Pan1112==turn) 
                { if(Pan1212==turn) 
                { if(Pan1312==turn) 
                { win++; } } } } }
                if(Pan0913==turn) 
                { if(Pan1013==turn) 
                { if(Pan1113==turn) 
                { if(Pan1213==turn) 
                { if(Pan1313==turn) 
                { win++; } } } } }
                if(Pan0914==turn) 
                { if(Pan1014==turn) 
                { if(Pan1114==turn) 
                { if(Pan1214==turn) 
                { if(Pan1314==turn) 
                { win++; } } } } }
                if(Pan0915==turn) 
                { if(Pan1015==turn) 
                { if(Pan1115==turn) 
                { if(Pan1215==turn) 
                { if(Pan1315==turn) 
                { win++; } } } } }
                if(Pan0916==turn) 
                { if(Pan1016==turn) 
                { if(Pan1116==turn) 
                { if(Pan1216==turn) 
                { if(Pan1316==turn) 
                { win++; } } } } }
                if(Pan0917==turn) 
                { if(Pan1017==turn) 
                { if(Pan1117==turn) 
                { if(Pan1217==turn) 
                { if(Pan1317==turn) 
                { win++; } } } } }
                if(Pan0918==turn) 
                { if(Pan1018==turn) 
                { if(Pan1118==turn) 
                { if(Pan1218==turn) 
                { if(Pan1318==turn) 
                { win++; } } } } }
                if(Pan0919==turn) 
                { if(Pan1019==turn) 
                { if(Pan1119==turn) 
                { if(Pan1219==turn) 
                { if(Pan1319==turn) 
                { win++; } } } } }
                if(Pan1001==turn) 
                { if(Pan1101==turn) 
                { if(Pan1201==turn) 
                { if(Pan1301==turn) 
                { if(Pan1401==turn) 
                { win++; } } } } }
                if(Pan1002==turn) 
                { if(Pan1102==turn) 
                { if(Pan1202==turn) 
                { if(Pan1302==turn) 
                { if(Pan1402==turn) 
                { win++; } } } } }
                if(Pan1003==turn) 
                { if(Pan1103==turn) 
                { if(Pan1203==turn) 
                { if(Pan1303==turn) 
                { if(Pan1403==turn) 
                { win++; } } } } }
                if(Pan1004==turn) 
                { if(Pan1104==turn) 
                { if(Pan1204==turn) 
                { if(Pan1304==turn) 
                { if(Pan1404==turn) 
                { win++; } } } } }
                if(Pan1005==turn) 
                { if(Pan1105==turn) 
                { if(Pan1205==turn) 
                { if(Pan1305==turn) 
                { if(Pan1405==turn) 
                { win++; } } } } }
                if(Pan1006==turn) 
                { if(Pan1106==turn) 
                { if(Pan1206==turn) 
                { if(Pan1306==turn) 
                { if(Pan1406==turn) 
                { win++; } } } } }
                if(Pan1007==turn) 
                { if(Pan1107==turn) 
                { if(Pan1207==turn) 
                { if(Pan1307==turn) 
                { if(Pan1407==turn) 
                { win++; } } } } }
                if(Pan1008==turn) 
                { if(Pan1108==turn) 
                { if(Pan1208==turn) 
                { if(Pan1308==turn) 
                { if(Pan1408==turn) 
                { win++; } } } } }
                if(Pan1009==turn) 
                { if(Pan1109==turn) 
                { if(Pan1209==turn) 
                { if(Pan1309==turn) 
                { if(Pan1409==turn) 
                { win++; } } } } }
                if(Pan1010==turn) 
                { if(Pan1110==turn) 
                { if(Pan1210==turn) 
                { if(Pan1310==turn) 
                { if(Pan1410==turn) 
                { win++; } } } } }
                if(Pan1011==turn) 
                { if(Pan1111==turn) 
                { if(Pan1211==turn) 
                { if(Pan1311==turn) 
                { if(Pan1411==turn) 
                { win++; } } } } }
                if(Pan1012==turn) 
                { if(Pan1112==turn) 
                { if(Pan1212==turn) 
                { if(Pan1312==turn) 
                { if(Pan1412==turn) 
                { win++; } } } } }
                if(Pan1013==turn) 
                { if(Pan1113==turn) 
                { if(Pan1213==turn) 
                { if(Pan1313==turn) 
                { if(Pan1413==turn) 
                { win++; } } } } }
                if(Pan1014==turn) 
                { if(Pan1114==turn) 
                { if(Pan1214==turn) 
                { if(Pan1314==turn) 
                { if(Pan1414==turn) 
                { win++; } } } } }
                if(Pan1015==turn) 
                { if(Pan1115==turn) 
                { if(Pan1215==turn) 
                { if(Pan1315==turn) 
                { if(Pan1415==turn) 
                { win++; } } } } }
                if(Pan1016==turn) 
                { if(Pan1116==turn) 
                { if(Pan1216==turn) 
                { if(Pan1316==turn) 
                { if(Pan1416==turn) 
                { win++; } } } } }
                if(Pan1017==turn) 
                { if(Pan1117==turn) 
                { if(Pan1217==turn) 
                { if(Pan1317==turn) 
                { if(Pan1417==turn) 
                { win++; } } } } }
                if(Pan1018==turn) 
                { if(Pan1118==turn) 
                { if(Pan1218==turn) 
                { if(Pan1318==turn) 
                { if(Pan1418==turn) 
                { win++; } } } } }
                if(Pan1019==turn) 
                { if(Pan1119==turn) 
                { if(Pan1219==turn) 
                { if(Pan1319==turn) 
                { if(Pan1419==turn) 
                { win++; } } } } }
                if(Pan1101==turn) 
                { if(Pan1201==turn) 
                { if(Pan1301==turn) 
                { if(Pan1401==turn) 
                { if(Pan1501==turn) 
                { win++; } } } } }
                if(Pan1102==turn) 
                { if(Pan1202==turn) 
                { if(Pan1302==turn) 
                { if(Pan1402==turn) 
                { if(Pan1502==turn) 
                { win++; } } } } }
                if(Pan1103==turn) 
                { if(Pan1203==turn) 
                { if(Pan1303==turn) 
                { if(Pan1403==turn) 
                { if(Pan1503==turn) 
                { win++; } } } } }
                if(Pan1104==turn) 
                { if(Pan1204==turn) 
                { if(Pan1304==turn) 
                { if(Pan1404==turn) 
                { if(Pan1504==turn) 
                { win++; } } } } }
                if(Pan1105==turn) 
                { if(Pan1205==turn) 
                { if(Pan1305==turn) 
                { if(Pan1405==turn) 
                { if(Pan1505==turn) 
                { win++; } } } } }
                if(Pan1106==turn) 
                { if(Pan1206==turn) 
                { if(Pan1306==turn) 
                { if(Pan1406==turn) 
                { if(Pan1506==turn) 
                { win++; } } } } }
                if(Pan1107==turn) 
                { if(Pan1207==turn) 
                { if(Pan1307==turn) 
                { if(Pan1407==turn) 
                { if(Pan1507==turn) 
                { win++; } } } } }
                if(Pan1108==turn) 
                { if(Pan1208==turn) 
                { if(Pan1308==turn) 
                { if(Pan1408==turn) 
                { if(Pan1508==turn) 
                { win++; } } } } }
                if(Pan1109==turn) 
                { if(Pan1209==turn) 
                { if(Pan1309==turn) 
                { if(Pan1409==turn) 
                { if(Pan1509==turn) 
                { win++; } } } } }
                if(Pan1110==turn) 
                { if(Pan1210==turn) 
                { if(Pan1310==turn) 
                { if(Pan1410==turn) 
                { if(Pan1510==turn) 
                { win++; } } } } }
                if(Pan1111==turn) 
                { if(Pan1211==turn) 
                { if(Pan1311==turn) 
                { if(Pan1411==turn) 
                { if(Pan1511==turn) 
                { win++; } } } } }
                if(Pan1112==turn) 
                { if(Pan1212==turn) 
                { if(Pan1312==turn) 
                { if(Pan1412==turn) 
                { if(Pan1512==turn) 
                { win++; } } } } }
                if(Pan1113==turn) 
                { if(Pan1213==turn) 
                { if(Pan1313==turn) 
                { if(Pan1413==turn) 
                { if(Pan1513==turn) 
                { win++; } } } } }
                if(Pan1114==turn) 
                { if(Pan1214==turn) 
                { if(Pan1314==turn) 
                { if(Pan1414==turn) 
                { if(Pan1514==turn) 
                { win++; } } } } }
                if(Pan1115==turn) 
                { if(Pan1215==turn) 
                { if(Pan1315==turn) 
                { if(Pan1415==turn) 
                { if(Pan1515==turn) 
                { win++; } } } } }
                if(Pan1116==turn) 
                { if(Pan1216==turn) 
                { if(Pan1316==turn) 
                { if(Pan1416==turn) 
                { if(Pan1516==turn) 
                { win++; } } } } }
                if(Pan1117==turn) 
                { if(Pan1217==turn) 
                { if(Pan1317==turn) 
                { if(Pan1417==turn) 
                { if(Pan1517==turn) 
                { win++; } } } } }
                if(Pan1118==turn) 
                { if(Pan1218==turn) 
                { if(Pan1318==turn) 
                { if(Pan1418==turn) 
                { if(Pan1518==turn) 
                { win++; } } } } }
                if(Pan1119==turn) 
                { if(Pan1219==turn) 
                { if(Pan1319==turn) 
                { if(Pan1419==turn) 
                { if(Pan1519==turn) 
                { win++; } } } } }
                if(Pan1201==turn) 
                { if(Pan1301==turn) 
                { if(Pan1401==turn) 
                { if(Pan1501==turn) 
                { if(Pan1601==turn) 
                { win++; } } } } }
                if(Pan1202==turn) 
                { if(Pan1302==turn) 
                { if(Pan1402==turn) 
                { if(Pan1502==turn) 
                { if(Pan1602==turn) 
                { win++; } } } } }
                if(Pan1203==turn) 
                { if(Pan1303==turn) 
                { if(Pan1403==turn) 
                { if(Pan1503==turn) 
                { if(Pan1603==turn) 
                { win++; } } } } }
                if(Pan1204==turn) 
                { if(Pan1304==turn) 
                { if(Pan1404==turn) 
                { if(Pan1504==turn) 
                { if(Pan1604==turn) 
                { win++; } } } } }
                if(Pan1205==turn) 
                { if(Pan1305==turn) 
                { if(Pan1405==turn) 
                { if(Pan1505==turn) 
                { if(Pan1605==turn) 
                { win++; } } } } }
                if(Pan1206==turn) 
                { if(Pan1306==turn) 
                { if(Pan1406==turn) 
                { if(Pan1506==turn) 
                { if(Pan1606==turn) 
                { win++; } } } } }
                if(Pan1207==turn) 
                { if(Pan1307==turn) 
                { if(Pan1407==turn) 
                { if(Pan1507==turn) 
                { if(Pan1607==turn) 
                { win++; } } } } }
                if(Pan1208==turn) 
                { if(Pan1308==turn) 
                { if(Pan1408==turn) 
                { if(Pan1508==turn) 
                { if(Pan1608==turn) 
                { win++; } } } } }
                if(Pan1209==turn) 
                { if(Pan1309==turn) 
                { if(Pan1409==turn) 
                { if(Pan1509==turn) 
                { if(Pan1609==turn) 
                { win++; } } } } }
                if(Pan1210==turn) 
                { if(Pan1310==turn) 
                { if(Pan1410==turn) 
                { if(Pan1510==turn) 
                { if(Pan1610==turn) 
                { win++; } } } } }
                if(Pan1211==turn) 
                { if(Pan1311==turn) 
                { if(Pan1411==turn) 
                { if(Pan1511==turn) 
                { if(Pan1611==turn) 
                { win++; } } } } }
                if(Pan1212==turn) 
                { if(Pan1312==turn) 
                { if(Pan1412==turn) 
                { if(Pan1512==turn) 
                { if(Pan1612==turn) 
                { win++; } } } } }
                if(Pan1213==turn) 
                { if(Pan1313==turn) 
                { if(Pan1413==turn) 
                { if(Pan1513==turn) 
                { if(Pan1613==turn) 
                { win++; } } } } }
                if(Pan1214==turn) 
                { if(Pan1314==turn) 
                { if(Pan1414==turn) 
                { if(Pan1514==turn) 
                { if(Pan1614==turn) 
                { win++; } } } } }
                if(Pan1215==turn) 
                { if(Pan1315==turn) 
                { if(Pan1415==turn) 
                { if(Pan1515==turn) 
                { if(Pan1615==turn) 
                { win++; } } } } }
                if(Pan1216==turn) 
                { if(Pan1316==turn) 
                { if(Pan1416==turn) 
                { if(Pan1516==turn) 
                { if(Pan1616==turn) 
                { win++; } } } } }
                if(Pan1217==turn) 
                { if(Pan1317==turn) 
                { if(Pan1417==turn) 
                { if(Pan1517==turn) 
                { if(Pan1617==turn) 
                { win++; } } } } }
                if(Pan1218==turn) 
                { if(Pan1318==turn) 
                { if(Pan1418==turn) 
                { if(Pan1518==turn) 
                { if(Pan1618==turn) 
                { win++; } } } } }
                if(Pan1219==turn) 
                { if(Pan1319==turn) 
                { if(Pan1419==turn) 
                { if(Pan1519==turn) 
                { if(Pan1619==turn) 
                { win++; } } } } }
                if(Pan1301==turn) 
                { if(Pan1401==turn) 
                { if(Pan1501==turn) 
                { if(Pan1601==turn) 
                { if(Pan1701==turn) 
                { win++; } } } } }
                if(Pan1302==turn) 
                { if(Pan1402==turn) 
                { if(Pan1502==turn) 
                { if(Pan1602==turn) 
                { if(Pan1702==turn) 
                { win++; } } } } }
                if(Pan1303==turn) 
                { if(Pan1403==turn) 
                { if(Pan1503==turn) 
                { if(Pan1603==turn) 
                { if(Pan1703==turn) 
                { win++; } } } } }
                if(Pan1304==turn) 
                { if(Pan1404==turn) 
                { if(Pan1504==turn) 
                { if(Pan1604==turn) 
                { if(Pan1704==turn) 
                { win++; } } } } }
                if(Pan1305==turn) 
                { if(Pan1405==turn) 
                { if(Pan1505==turn) 
                { if(Pan1605==turn) 
                { if(Pan1705==turn) 
                { win++; } } } } }
                if(Pan1306==turn) 
                { if(Pan1406==turn) 
                { if(Pan1506==turn) 
                { if(Pan1606==turn) 
                { if(Pan1706==turn) 
                { win++; } } } } }
                if(Pan1307==turn) 
                { if(Pan1407==turn) 
                { if(Pan1507==turn) 
                { if(Pan1607==turn) 
                { if(Pan1707==turn) 
                { win++; } } } } }
                if(Pan1308==turn) 
                { if(Pan1408==turn) 
                { if(Pan1508==turn) 
                { if(Pan1608==turn) 
                { if(Pan1708==turn) 
                { win++; } } } } }
                if(Pan1309==turn) 
                { if(Pan1409==turn) 
                { if(Pan1509==turn) 
                { if(Pan1609==turn) 
                { if(Pan1709==turn) 
                { win++; } } } } }
                if(Pan1310==turn) 
                { if(Pan1410==turn) 
                { if(Pan1510==turn) 
                { if(Pan1610==turn) 
                { if(Pan1710==turn) 
                { win++; } } } } }
                if(Pan1311==turn) 
                { if(Pan1411==turn) 
                { if(Pan1511==turn) 
                { if(Pan1611==turn) 
                { if(Pan1711==turn) 
                { win++; } } } } }
                if(Pan1312==turn) 
                { if(Pan1412==turn) 
                { if(Pan1512==turn) 
                { if(Pan1612==turn) 
                { if(Pan1712==turn) 
                { win++; } } } } }
                if(Pan1313==turn) 
                { if(Pan1413==turn) 
                { if(Pan1513==turn) 
                { if(Pan1613==turn) 
                { if(Pan1713==turn) 
                { win++; } } } } }
                if(Pan1314==turn) 
                { if(Pan1414==turn) 
                { if(Pan1514==turn) 
                { if(Pan1614==turn) 
                { if(Pan1714==turn) 
                { win++; } } } } }
                if(Pan1315==turn) 
                { if(Pan1415==turn) 
                { if(Pan1515==turn) 
                { if(Pan1615==turn) 
                { if(Pan1715==turn) 
                { win++; } } } } }
                if(Pan1316==turn) 
                { if(Pan1416==turn) 
                { if(Pan1516==turn) 
                { if(Pan1616==turn) 
                { if(Pan1716==turn) 
                { win++; } } } } }
                if(Pan1317==turn) 
                { if(Pan1417==turn) 
                { if(Pan1517==turn) 
                { if(Pan1617==turn) 
                { if(Pan1717==turn) 
                { win++; } } } } }
                if(Pan1318==turn) 
                { if(Pan1418==turn) 
                { if(Pan1518==turn) 
                { if(Pan1618==turn) 
                { if(Pan1718==turn) 
                { win++; } } } } }
                if(Pan1319==turn) 
                { if(Pan1419==turn) 
                { if(Pan1519==turn) 
                { if(Pan1619==turn) 
                { if(Pan1719==turn) 
                { win++; } } } } }
                if(Pan1401==turn) 
                { if(Pan1501==turn) 
                { if(Pan1601==turn) 
                { if(Pan1701==turn) 
                { if(Pan1801==turn) 
                { win++; } } } } }
                if(Pan1402==turn) 
                { if(Pan1502==turn) 
                { if(Pan1602==turn) 
                { if(Pan1702==turn) 
                { if(Pan1802==turn) 
                { win++; } } } } }
                if(Pan1403==turn) 
                { if(Pan1503==turn) 
                { if(Pan1603==turn) 
                { if(Pan1703==turn) 
                { if(Pan1803==turn) 
                { win++; } } } } }
                if(Pan1404==turn) 
                { if(Pan1504==turn) 
                { if(Pan1604==turn) 
                { if(Pan1704==turn) 
                { if(Pan1804==turn) 
                { win++; } } } } }
                if(Pan1405==turn) 
                { if(Pan1505==turn) 
                { if(Pan1605==turn) 
                { if(Pan1705==turn) 
                { if(Pan1805==turn) 
                { win++; } } } } }
                if(Pan1406==turn) 
                { if(Pan1506==turn) 
                { if(Pan1606==turn) 
                { if(Pan1706==turn) 
                { if(Pan1806==turn) 
                { win++; } } } } }
                if(Pan1407==turn) 
                { if(Pan1507==turn) 
                { if(Pan1607==turn) 
                { if(Pan1707==turn) 
                { if(Pan1807==turn) 
                { win++; } } } } }
                if(Pan1408==turn) 
                { if(Pan1508==turn) 
                { if(Pan1608==turn) 
                { if(Pan1708==turn) 
                { if(Pan1808==turn) 
                { win++; } } } } }
                if(Pan1409==turn) 
                { if(Pan1509==turn) 
                { if(Pan1609==turn) 
                { if(Pan1709==turn) 
                { if(Pan1809==turn) 
                { win++; } } } } }
                if(Pan1410==turn) 
                { if(Pan1510==turn) 
                { if(Pan1610==turn) 
                { if(Pan1710==turn) 
                { if(Pan1810==turn) 
                { win++; } } } } }
                if(Pan1411==turn) 
                { if(Pan1511==turn) 
                { if(Pan1611==turn) 
                { if(Pan1711==turn) 
                { if(Pan1811==turn) 
                { win++; } } } } }
                if(Pan1412==turn) 
                { if(Pan1512==turn) 
                { if(Pan1612==turn) 
                { if(Pan1712==turn) 
                { if(Pan1812==turn) 
                { win++; } } } } }
                if(Pan1413==turn) 
                { if(Pan1513==turn) 
                { if(Pan1613==turn) 
                { if(Pan1713==turn) 
                { if(Pan1813==turn) 
                { win++; } } } } }
                if(Pan1414==turn) 
                { if(Pan1514==turn) 
                { if(Pan1614==turn) 
                { if(Pan1714==turn) 
                { if(Pan1814==turn) 
                { win++; } } } } }
                if(Pan1415==turn) 
                { if(Pan1515==turn) 
                { if(Pan1615==turn) 
                { if(Pan1715==turn) 
                { if(Pan1815==turn) 
                { win++; } } } } }
                if(Pan1416==turn) 
                { if(Pan1516==turn) 
                { if(Pan1616==turn) 
                { if(Pan1716==turn) 
                { if(Pan1816==turn) 
                { win++; } } } } }
                if(Pan1417==turn) 
                { if(Pan1517==turn) 
                { if(Pan1617==turn) 
                { if(Pan1717==turn) 
                { if(Pan1817==turn) 
                { win++; } } } } }
                if(Pan1418==turn) 
                { if(Pan1518==turn) 
                { if(Pan1618==turn) 
                { if(Pan1718==turn) 
                { if(Pan1818==turn) 
                { win++; } } } } }
                if(Pan1419==turn) 
                { if(Pan1519==turn) 
                { if(Pan1619==turn) 
                { if(Pan1719==turn) 
                { if(Pan1819==turn) 
                { win++; } } } } }
                if(Pan1501==turn) 
                { if(Pan1601==turn) 
                { if(Pan1701==turn) 
                { if(Pan1801==turn) 
                { if(Pan1901==turn) 
                { win++; } } } } }
                if(Pan1502==turn) 
                { if(Pan1602==turn) 
                { if(Pan1702==turn) 
                { if(Pan1802==turn) 
                { if(Pan1902==turn) 
                { win++; } } } } }
                if(Pan1503==turn) 
                { if(Pan1603==turn) 
                { if(Pan1703==turn) 
                { if(Pan1803==turn) 
                { if(Pan1903==turn) 
                { win++; } } } } }
                if(Pan1504==turn) 
                { if(Pan1604==turn) 
                { if(Pan1704==turn) 
                { if(Pan1804==turn) 
                { if(Pan1904==turn) 
                { win++; } } } } }
                if(Pan1505==turn) 
                { if(Pan1605==turn) 
                { if(Pan1705==turn) 
                { if(Pan1805==turn) 
                { if(Pan1905==turn) 
                { win++; } } } } }
                if(Pan1506==turn) 
                { if(Pan1606==turn) 
                { if(Pan1706==turn) 
                { if(Pan1806==turn) 
                { if(Pan1906==turn) 
                { win++; } } } } }
                if(Pan1507==turn) 
                { if(Pan1607==turn) 
                { if(Pan1707==turn) 
                { if(Pan1807==turn) 
                { if(Pan1907==turn) 
                { win++; } } } } }
                if(Pan1508==turn) 
                { if(Pan1608==turn) 
                { if(Pan1708==turn) 
                { if(Pan1808==turn) 
                { if(Pan1908==turn) 
                { win++; } } } } }
                if(Pan1509==turn) 
                { if(Pan1609==turn) 
                { if(Pan1709==turn) 
                { if(Pan1809==turn) 
                { if(Pan1909==turn) 
                { win++; } } } } }
                if(Pan1510==turn) 
                { if(Pan1610==turn) 
                { if(Pan1710==turn) 
                { if(Pan1810==turn) 
                { if(Pan1910==turn) 
                { win++; } } } } }
                if(Pan1511==turn) 
                { if(Pan1611==turn) 
                { if(Pan1711==turn) 
                { if(Pan1811==turn) 
                { if(Pan1911==turn) 
                { win++; } } } } }
                if(Pan1512==turn) 
                { if(Pan1612==turn) 
                { if(Pan1712==turn) 
                { if(Pan1812==turn) 
                { if(Pan1912==turn) 
                { win++; } } } } }
                if(Pan1513==turn) 
                { if(Pan1613==turn) 
                { if(Pan1713==turn) 
                { if(Pan1813==turn) 
                { if(Pan1913==turn) 
                { win++; } } } } }
                if(Pan1514==turn) 
                { if(Pan1614==turn) 
                { if(Pan1714==turn) 
                { if(Pan1814==turn) 
                { if(Pan1914==turn) 
                { win++; } } } } }
                if(Pan1515==turn) 
                { if(Pan1615==turn) 
                { if(Pan1715==turn) 
                { if(Pan1815==turn) 
                { if(Pan1915==turn) 
                { win++; } } } } }
                if(Pan1516==turn) 
                { if(Pan1616==turn) 
                { if(Pan1716==turn) 
                { if(Pan1816==turn) 
                { if(Pan1916==turn) 
                { win++; } } } } }
                if(Pan1517==turn) 
                { if(Pan1617==turn) 
                { if(Pan1717==turn) 
                { if(Pan1817==turn) 
                { if(Pan1917==turn) 
                { win++; } } } } }
                if(Pan1518==turn) 
                { if(Pan1618==turn) 
                { if(Pan1718==turn) 
                { if(Pan1818==turn) 
                { if(Pan1918==turn) 
                { win++; } } } } }
                if(Pan1519==turn) 
                { if(Pan1619==turn) 
                { if(Pan1719==turn) 
                { if(Pan1819==turn) 
                { if(Pan1919==turn) 
                { win++; } } } } }

                /////////////////// y = -x 대각선 검사 ////////////////////////////
                if(Pan0101==turn) 
                { if(Pan0202==turn) 
                { if(Pan0303==turn) 
                { if(Pan0404==turn) 
                { if(Pan0505==turn) 
                { win++; } } } } }
                if(Pan0102==turn) 
                { if(Pan0203==turn) 
                { if(Pan0304==turn) 
                { if(Pan0405==turn) 
                { if(Pan0506==turn) 
                { win++; } } } } }
                if(Pan0103==turn) 
                { if(Pan0204==turn) 
                { if(Pan0305==turn) 
                { if(Pan0406==turn) 
                { if(Pan0507==turn) 
                { win++; } } } } }
                if(Pan0104==turn) 
                { if(Pan0205==turn) 
                { if(Pan0306==turn) 
                { if(Pan0407==turn) 
                { if(Pan0508==turn) 
                { win++; } } } } }
                if(Pan0105==turn) 
                { if(Pan0206==turn) 
                { if(Pan0307==turn) 
                { if(Pan0408==turn) 
                { if(Pan0509==turn) 
                { win++; } } } } }
                if(Pan0110==turn) 
                { if(Pan0211==turn) 
                { if(Pan0312==turn) 
                { if(Pan0413==turn) 
                { if(Pan0514==turn) 
                { win++; } } } } }
                if(Pan0111==turn) 
                { if(Pan0212==turn) 
                { if(Pan0313==turn) 
                { if(Pan0414==turn) 
                { if(Pan0515==turn) 
                { win++; } } } } }
                if(Pan0112==turn) 
                { if(Pan0213==turn) 
                { if(Pan0314==turn) 
                { if(Pan0415==turn) 
                { if(Pan0516==turn) 
                { win++; } } } } }
                if(Pan0113==turn) 
                { if(Pan0214==turn) 
                { if(Pan0315==turn) 
                { if(Pan0416==turn) 
                { if(Pan0517==turn) 
                { win++; } } } } }
                if(Pan0114==turn) 
                { if(Pan0215==turn) 
                { if(Pan0316==turn) 
                { if(Pan0417==turn) 
                { if(Pan0518==turn) 
                { win++; } } } } }
                if(Pan0115==turn) 
                { if(Pan0216==turn) 
                { if(Pan0317==turn) 
                { if(Pan0418==turn) 
                { if(Pan0519==turn) 
                { win++; } } } } }
                if(Pan0201==turn) 
                { if(Pan0302==turn) 
                { if(Pan0403==turn) 
                { if(Pan0504==turn) 
                { if(Pan0605==turn) 
                { win++; } } } } }
                if(Pan0202==turn) 
                { if(Pan0303==turn) 
                { if(Pan0404==turn) 
                { if(Pan0505==turn) 
                { if(Pan0606==turn) 
                { win++; } } } } }
                if(Pan0203==turn) 
                { if(Pan0304==turn) 
                { if(Pan0405==turn) 
                { if(Pan0506==turn) 
                { if(Pan0607==turn) 
                { win++; } } } } }
                if(Pan0204==turn) 
                { if(Pan0305==turn) 
                { if(Pan0406==turn) 
                { if(Pan0507==turn) 
                { if(Pan0608==turn) 
                { win++; } } } } }
                if(Pan0205==turn) 
                { if(Pan0306==turn) 
                { if(Pan0407==turn) 
                { if(Pan0508==turn) 
                { if(Pan0609==turn) 
                { win++; } } } } }
                if(Pan0210==turn) 
                { if(Pan0311==turn) 
                { if(Pan0412==turn) 
                { if(Pan0513==turn) 
                { if(Pan0614==turn) 
                { win++; } } } } }
                if(Pan0211==turn) 
                { if(Pan0312==turn) 
                { if(Pan0413==turn) 
                { if(Pan0514==turn) 
                { if(Pan0615==turn) 
                { win++; } } } } }
                if(Pan0212==turn) 
                { if(Pan0313==turn) 
                { if(Pan0414==turn) 
                { if(Pan0515==turn) 
                { if(Pan0616==turn) 
                { win++; } } } } }
                if(Pan0213==turn) 
                { if(Pan0314==turn) 
                { if(Pan0415==turn) 
                { if(Pan0516==turn) 
                { if(Pan0617==turn) 
                { win++; } } } } }
                if(Pan0214==turn) 
                { if(Pan0315==turn) 
                { if(Pan0416==turn) 
                { if(Pan0517==turn) 
                { if(Pan0618==turn) 
                { win++; } } } } }
                if(Pan0215==turn) 
                { if(Pan0316==turn) 
                { if(Pan0417==turn) 
                { if(Pan0518==turn) 
                { if(Pan0619==turn) 
                { win++; } } } } }
                if(Pan0301==turn) 
                { if(Pan0402==turn) 
                { if(Pan0503==turn) 
                { if(Pan0604==turn) 
                { if(Pan0705==turn) 
                { win++; } } } } }
                if(Pan0302==turn) 
                { if(Pan0403==turn) 
                { if(Pan0504==turn) 
                { if(Pan0605==turn) 
                { if(Pan0706==turn) 
                { win++; } } } } }
                if(Pan0303==turn) 
                { if(Pan0404==turn) 
                { if(Pan0505==turn) 
                { if(Pan0606==turn) 
                { if(Pan0707==turn) 
                { win++; } } } } }
                if(Pan0304==turn) 
                { if(Pan0405==turn) 
                { if(Pan0506==turn) 
                { if(Pan0607==turn) 
                { if(Pan0708==turn) 
                { win++; } } } } }
                if(Pan0305==turn) 
                { if(Pan0406==turn) 
                { if(Pan0507==turn) 
                { if(Pan0608==turn) 
                { if(Pan0709==turn) 
                { win++; } } } } }
                if(Pan0310==turn) 
                { if(Pan0411==turn) 
                { if(Pan0512==turn) 
                { if(Pan0613==turn) 
                { if(Pan0714==turn) 
                { win++; } } } } }
                if(Pan0311==turn) 
                { if(Pan0412==turn) 
                { if(Pan0513==turn) 
                { if(Pan0614==turn) 
                { if(Pan0715==turn) 
                { win++; } } } } }
                if(Pan0312==turn) 
                { if(Pan0413==turn) 
                { if(Pan0514==turn) 
                { if(Pan0615==turn) 
                { if(Pan0716==turn) 
                { win++; } } } } }
                if(Pan0313==turn) 
                { if(Pan0414==turn) 
                { if(Pan0515==turn) 
                { if(Pan0616==turn) 
                { if(Pan0717==turn) 
                { win++; } } } } }
                if(Pan0314==turn) 
                { if(Pan0415==turn) 
                { if(Pan0516==turn) 
                { if(Pan0617==turn) 
                { if(Pan0718==turn) 
                { win++; } } } } }
                if(Pan0315==turn) 
                { if(Pan0416==turn) 
                { if(Pan0517==turn) 
                { if(Pan0618==turn) 
                { if(Pan0719==turn) 
                { win++; } } } } }
                if(Pan0401==turn) 
                { if(Pan0502==turn) 
                { if(Pan0603==turn) 
                { if(Pan0704==turn) 
                { if(Pan0805==turn) 
                { win++; } } } } }
                if(Pan0402==turn) 
                { if(Pan0503==turn) 
                { if(Pan0604==turn) 
                { if(Pan0705==turn) 
                { if(Pan0806==turn) 
                { win++; } } } } }
                if(Pan0403==turn) 
                { if(Pan0504==turn) 
                { if(Pan0605==turn) 
                { if(Pan0706==turn) 
                { if(Pan0807==turn) 
                { win++; } } } } }
                if(Pan0404==turn) 
                { if(Pan0505==turn) 
                { if(Pan0606==turn) 
                { if(Pan0707==turn) 
                { if(Pan0808==turn) 
                { win++; } } } } }
                if(Pan0405==turn) 
                { if(Pan0506==turn) 
                { if(Pan0607==turn) 
                { if(Pan0708==turn) 
                { if(Pan0809==turn) 
                { win++; } } } } }
                if(Pan0410==turn) 
                { if(Pan0511==turn) 
                { if(Pan0612==turn) 
                { if(Pan0713==turn) 
                { if(Pan0814==turn) 
                { win++; } } } } }
                if(Pan0411==turn) 
                { if(Pan0512==turn) 
                { if(Pan0613==turn) 
                { if(Pan0714==turn) 
                { if(Pan0815==turn) 
                { win++; } } } } }
                if(Pan0412==turn) 
                { if(Pan0513==turn) 
                { if(Pan0614==turn) 
                { if(Pan0715==turn) 
                { if(Pan0816==turn) 
                { win++; } } } } }
                if(Pan0413==turn) 
                { if(Pan0514==turn) 
                { if(Pan0615==turn) 
                { if(Pan0716==turn) 
                { if(Pan0817==turn) 
                { win++; } } } } }
                if(Pan0414==turn) 
                { if(Pan0515==turn) 
                { if(Pan0616==turn) 
                { if(Pan0717==turn) 
                { if(Pan0818==turn) 
                { win++; } } } } }
                if(Pan0415==turn) 
                { if(Pan0516==turn) 
                { if(Pan0617==turn) 
                { if(Pan0718==turn) 
                { if(Pan0819==turn) 
                { win++; } } } } }
                if(Pan0501==turn) 
                { if(Pan0602==turn) 
                { if(Pan0703==turn) 
                { if(Pan0804==turn) 
                { if(Pan0905==turn) 
                { win++; } } } } }
                if(Pan0502==turn) 
                { if(Pan0603==turn) 
                { if(Pan0704==turn) 
                { if(Pan0805==turn) 
                { if(Pan0906==turn) 
                { win++; } } } } }
                if(Pan0503==turn) 
                { if(Pan0604==turn) 
                { if(Pan0705==turn) 
                { if(Pan0806==turn) 
                { if(Pan0907==turn) 
                { win++; } } } } }
                if(Pan0504==turn) 
                { if(Pan0605==turn) 
                { if(Pan0706==turn) 
                { if(Pan0807==turn) 
                { if(Pan0908==turn) 
                { win++; } } } } }
                if(Pan0505==turn) 
                { if(Pan0606==turn) 
                { if(Pan0707==turn) 
                { if(Pan0808==turn) 
                { if(Pan0909==turn) 
                { win++; } } } } }
                if(Pan0510==turn) 
                { if(Pan0611==turn) 
                { if(Pan0712==turn) 
                { if(Pan0813==turn) 
                { if(Pan0914==turn) 
                { win++; } } } } }
                if(Pan0511==turn) 
                { if(Pan0612==turn) 
                { if(Pan0713==turn) 
                { if(Pan0814==turn) 
                { if(Pan0915==turn) 
                { win++; } } } } }
                if(Pan0512==turn) 
                { if(Pan0613==turn) 
                { if(Pan0714==turn) 
                { if(Pan0815==turn) 
                { if(Pan0916==turn) 
                { win++; } } } } }
                if(Pan0513==turn) 
                { if(Pan0614==turn) 
                { if(Pan0715==turn) 
                { if(Pan0816==turn) 
                { if(Pan0917==turn) 
                { win++; } } } } }
                if(Pan0514==turn) 
                { if(Pan0615==turn) 
                { if(Pan0716==turn) 
                { if(Pan0817==turn) 
                { if(Pan0918==turn) 
                { win++; } } } } }
                if(Pan0515==turn) 
                { if(Pan0616==turn) 
                { if(Pan0717==turn) 
                { if(Pan0818==turn) 
                { if(Pan0919==turn) 
                { win++; } } } } }
                if(Pan0606==turn) 
                { if(Pan0707==turn) 
                { if(Pan0808==turn) 
                { if(Pan0909==turn) 
                { if(Pan1010==turn) 
                { win++; } } } } }
                if(Pan0610==turn) 
                { if(Pan0711==turn) 
                { if(Pan0812==turn) 
                { if(Pan0913==turn) 
                { if(Pan1014==turn) 
                { win++; } } } } }
                if(Pan0611==turn) 
                { if(Pan0712==turn) 
                { if(Pan0813==turn) 
                { if(Pan0914==turn) 
                { if(Pan1015==turn) 
                { win++; } } } } }
                if(Pan0612==turn) 
                { if(Pan0713==turn) 
                { if(Pan0814==turn) 
                { if(Pan0915==turn) 
                { if(Pan1016==turn) 
                { win++; } } } } }
                if(Pan0613==turn) 
                { if(Pan0714==turn) 
                { if(Pan0815==turn) 
                { if(Pan0916==turn) 
                { if(Pan1017==turn) 
                { win++; } } } } }
                if(Pan0614==turn) 
                { if(Pan0715==turn) 
                { if(Pan0816==turn) 
                { if(Pan0917==turn) 
                { if(Pan1018==turn) 
                { win++; } } } } }
                if(Pan0615==turn) 
                { if(Pan0716==turn) 
                { if(Pan0817==turn) 
                { if(Pan0918==turn) 
                { if(Pan1019==turn) 
                { win++; } } } } }
                if(Pan0707==turn) 
                { if(Pan0808==turn) 
                { if(Pan0909==turn) 
                { if(Pan1010==turn) 
                { if(Pan1111==turn) 
                { win++; } } } } }
                if(Pan0710==turn) 
                { if(Pan0811==turn) 
                { if(Pan0912==turn) 
                { if(Pan1013==turn) 
                { if(Pan1114==turn) 
                { win++; } } } } }
                if(Pan0711==turn) 
                { if(Pan0812==turn) 
                { if(Pan0913==turn) 
                { if(Pan1014==turn) 
                { if(Pan1115==turn) 
                { win++; } } } } }
                if(Pan0712==turn) 
                { if(Pan0813==turn) 
                { if(Pan0914==turn) 
                { if(Pan1015==turn) 
                { if(Pan1116==turn) 
                { win++; } } } } }
                if(Pan0713==turn) 
                { if(Pan0814==turn) 
                { if(Pan0915==turn) 
                { if(Pan1016==turn) 
                { if(Pan1117==turn) 
                { win++; } } } } }
                if(Pan0714==turn) 
                { if(Pan0815==turn) 
                { if(Pan0916==turn) 
                { if(Pan1017==turn) 
                { if(Pan1118==turn) 
                { win++; } } } } }
                if(Pan0715==turn) 
                { if(Pan0816==turn) 
                { if(Pan0917==turn) 
                { if(Pan1018==turn) 
                { if(Pan1119==turn) 
                { win++; } } } } }
                if(Pan0808==turn) 
                { if(Pan0909==turn) 
                { if(Pan1010==turn) 
                { if(Pan1111==turn) 
                { if(Pan1212==turn) 
                { win++; } } } } }
                if(Pan0810==turn) 
                { if(Pan0911==turn) 
                { if(Pan1012==turn) 
                { if(Pan1113==turn) 
                { if(Pan1214==turn) 
                { win++; } } } } }
                if(Pan0811==turn) 
                { if(Pan0912==turn) 
                { if(Pan1013==turn) 
                { if(Pan1114==turn) 
                { if(Pan1215==turn) 
                { win++; } } } } }
                if(Pan0812==turn) 
                { if(Pan0913==turn) 
                { if(Pan1014==turn) 
                { if(Pan1115==turn) 
                { if(Pan1216==turn) 
                { win++; } } } } }
                if(Pan0813==turn) 
                { if(Pan0914==turn) 
                { if(Pan1015==turn) 
                { if(Pan1116==turn) 
                { if(Pan1217==turn) 
                { win++; } } } } }
                if(Pan0814==turn) 
                { if(Pan0915==turn) 
                { if(Pan1016==turn) 
                { if(Pan1117==turn) 
                { if(Pan1218==turn) 
                { win++; } } } } }
                if(Pan0815==turn) 
                { if(Pan0916==turn) 
                { if(Pan1017==turn) 
                { if(Pan1118==turn) 
                { if(Pan1219==turn) 
                { win++; } } } } }
                if(Pan0909==turn) 
                { if(Pan1010==turn) 
                { if(Pan1111==turn) 
                { if(Pan1212==turn) 
                { if(Pan1313==turn) 
                { win++; } } } } }
                if(Pan0910==turn) 
                { if(Pan1011==turn) 
                { if(Pan1112==turn) 
                { if(Pan1213==turn) 
                { if(Pan1314==turn) 
                { win++; } } } } }
                if(Pan0911==turn) 
                { if(Pan1012==turn) 
                { if(Pan1113==turn) 
                { if(Pan1214==turn) 
                { if(Pan1315==turn) 
                { win++; } } } } }
                if(Pan0912==turn) 
                { if(Pan1013==turn) 
                { if(Pan1114==turn) 
                { if(Pan1215==turn) 
                { if(Pan1316==turn) 
                { win++; } } } } }
                if(Pan0913==turn) 
                { if(Pan1014==turn) 
                { if(Pan1115==turn) 
                { if(Pan1216==turn) 
                { if(Pan1317==turn) 
                { win++; } } } } }
                if(Pan0914==turn) 
                { if(Pan1015==turn) 
                { if(Pan1116==turn) 
                { if(Pan1217==turn) 
                { if(Pan1318==turn) 
                { win++; } } } } }
                if(Pan0915==turn) 
                { if(Pan1016==turn) 
                { if(Pan1117==turn) 
                { if(Pan1218==turn) 
                { if(Pan1319==turn) 
                { win++; } } } } }
                if(Pan1001==turn) 
                { if(Pan1102==turn) 
                { if(Pan1203==turn) 
                { if(Pan1304==turn) 
                { if(Pan1405==turn) 
                { win++; } } } } }
                if(Pan1002==turn) 
                { if(Pan1103==turn) 
                { if(Pan1204==turn) 
                { if(Pan1305==turn) 
                { if(Pan1406==turn) 
                { win++; } } } } }
                if(Pan1003==turn) 
                { if(Pan1104==turn) 
                { if(Pan1205==turn) 
                { if(Pan1306==turn) 
                { if(Pan1407==turn) 
                { win++; } } } } }
                if(Pan1004==turn) 
                { if(Pan1105==turn) 
                { if(Pan1206==turn) 
                { if(Pan1307==turn) 
                { if(Pan1408==turn) 
                { win++; } } } } }
                if(Pan1005==turn) 
                { if(Pan1106==turn) 
                { if(Pan1207==turn) 
                { if(Pan1308==turn) 
                { if(Pan1409==turn) 
                { win++; } } } } }
                if(Pan1006==turn) 
                { if(Pan1107==turn) 
                { if(Pan1208==turn) 
                { if(Pan1309==turn) 
                { if(Pan1410==turn) 
                { win++; } } } } }
                if(Pan1007==turn) 
                { if(Pan1108==turn) 
                { if(Pan1209==turn) 
                { if(Pan1310==turn) 
                { if(Pan1411==turn) 
                { win++; } } } } }
                if(Pan1008==turn) 
                { if(Pan1109==turn) 
                { if(Pan1210==turn) 
                { if(Pan1311==turn) 
                { if(Pan1412==turn) 
                { win++; } } } } }
                if(Pan1009==turn) 
                { if(Pan1110==turn) 
                { if(Pan1211==turn) 
                { if(Pan1312==turn) 
                { if(Pan1413==turn) 
                { win++; } } } } }
                if(Pan1010==turn) 
                { if(Pan1111==turn) 
                { if(Pan1212==turn) 
                { if(Pan1313==turn) 
                { if(Pan1414==turn) 
                { win++; } } } } }
                if(Pan1011==turn) 
                { if(Pan1112==turn) 
                { if(Pan1213==turn) 
                { if(Pan1314==turn) 
                { if(Pan1415==turn) 
                { win++; } } } } }
                if(Pan1012==turn) 
                { if(Pan1113==turn) 
                { if(Pan1214==turn) 
                { if(Pan1315==turn) 
                { if(Pan1416==turn) 
                { win++; } } } } }
                if(Pan1013==turn) 
                { if(Pan1114==turn) 
                { if(Pan1215==turn) 
                { if(Pan1316==turn) 
                { if(Pan1417==turn) 
                { win++; } } } } }
                if(Pan1014==turn) 
                { if(Pan1115==turn) 
                { if(Pan1216==turn) 
                { if(Pan1317==turn) 
                { if(Pan1418==turn) 
                { win++; } } } } }
                if(Pan1015==turn) 
                { if(Pan1116==turn) 
                { if(Pan1217==turn) 
                { if(Pan1318==turn) 
                { if(Pan1419==turn) 
                { win++; } } } } }
                if(Pan1101==turn) 
                { if(Pan1202==turn) 
                { if(Pan1303==turn) 
                { if(Pan1404==turn) 
                { if(Pan1505==turn) 
                { win++; } } } } }
                if(Pan1102==turn) 
                { if(Pan1203==turn) 
                { if(Pan1304==turn) 
                { if(Pan1405==turn) 
                { if(Pan1506==turn) 
                { win++; } } } } }
                if(Pan1103==turn) 
                { if(Pan1204==turn) 
                { if(Pan1305==turn) 
                { if(Pan1406==turn) 
                { if(Pan1507==turn) 
                { win++; } } } } }
                if(Pan1104==turn) 
                { if(Pan1205==turn) 
                { if(Pan1306==turn) 
                { if(Pan1407==turn) 
                { if(Pan1508==turn) 
                { win++; } } } } }
                if(Pan1105==turn) 
                { if(Pan1206==turn) 
                { if(Pan1307==turn) 
                { if(Pan1408==turn) 
                { if(Pan1509==turn) 
                { win++; } } } } }
                if(Pan1106==turn) 
                { if(Pan1207==turn) 
                { if(Pan1308==turn) 
                { if(Pan1409==turn) 
                { if(Pan1510==turn) 
                { win++; } } } } }
                if(Pan1107==turn) 
                { if(Pan1208==turn) 
                { if(Pan1309==turn) 
                { if(Pan1410==turn) 
                { if(Pan1511==turn) 
                { win++; } } } } }
                if(Pan1108==turn) 
                { if(Pan1209==turn) 
                { if(Pan1310==turn) 
                { if(Pan1411==turn) 
                { if(Pan1512==turn) 
                { win++; } } } } }
                if(Pan1109==turn) 
                { if(Pan1210==turn) 
                { if(Pan1311==turn) 
                { if(Pan1412==turn) 
                { if(Pan1513==turn) 
                { win++; } } } } }
                if(Pan1110==turn) 
                { if(Pan1211==turn) 
                { if(Pan1312==turn) 
                { if(Pan1413==turn) 
                { if(Pan1514==turn) 
                { win++; } } } } }
                if(Pan1111==turn) 
                { if(Pan1212==turn) 
                { if(Pan1313==turn) 
                { if(Pan1414==turn) 
                { if(Pan1515==turn) 
                { win++; } } } } }
                if(Pan1112==turn) 
                { if(Pan1213==turn) 
                { if(Pan1314==turn) 
                { if(Pan1415==turn) 
                { if(Pan1516==turn) 
                { win++; } } } } }
                if(Pan1113==turn) 
                { if(Pan1214==turn) 
                { if(Pan1315==turn) 
                { if(Pan1416==turn) 
                { if(Pan1517==turn) 
                { win++; } } } } }
                if(Pan1114==turn) 
                { if(Pan1215==turn) 
                { if(Pan1316==turn) 
                { if(Pan1417==turn) 
                { if(Pan1518==turn) 
                { win++; } } } } }
                if(Pan1115==turn) 
                { if(Pan1216==turn) 
                { if(Pan1317==turn) 
                { if(Pan1418==turn) 
                { if(Pan1519==turn) 
                { win++; } } } } }
                if(Pan1201==turn) 
                { if(Pan1302==turn) 
                { if(Pan1403==turn) 
                { if(Pan1504==turn) 
                { if(Pan1605==turn) 
                { win++; } } } } }
                if(Pan1202==turn) 
                { if(Pan1303==turn) 
                { if(Pan1404==turn) 
                { if(Pan1505==turn) 
                { if(Pan1606==turn) 
                { win++; } } } } }
                if(Pan1203==turn) 
                { if(Pan1304==turn) 
                { if(Pan1405==turn) 
                { if(Pan1506==turn) 
                { if(Pan1607==turn) 
                { win++; } } } } }
                if(Pan1204==turn) 
                { if(Pan1305==turn) 
                { if(Pan1406==turn) 
                { if(Pan1507==turn) 
                { if(Pan1608==turn) 
                { win++; } } } } }
                if(Pan1205==turn) 
                { if(Pan1306==turn) 
                { if(Pan1407==turn) 
                { if(Pan1508==turn) 
                { if(Pan1609==turn) 
                { win++; } } } } }
                if(Pan1206==turn) 
                { if(Pan1307==turn) 
                { if(Pan1408==turn) 
                { if(Pan1509==turn) 
                { if(Pan1610==turn) 
                { win++; } } } } }
                if(Pan1207==turn) 
                { if(Pan1308==turn) 
                { if(Pan1409==turn) 
                { if(Pan1510==turn) 
                { if(Pan1611==turn) 
                { win++; } } } } }
                if(Pan1208==turn) 
                { if(Pan1309==turn) 
                { if(Pan1410==turn) 
                { if(Pan1511==turn) 
                { if(Pan1612==turn) 
                { win++; } } } } }
                if(Pan1209==turn) 
                { if(Pan1310==turn) 
                { if(Pan1411==turn) 
                { if(Pan1512==turn) 
                { if(Pan1613==turn) 
                { win++; } } } } }
                if(Pan1210==turn) 
                { if(Pan1311==turn) 
                { if(Pan1412==turn) 
                { if(Pan1513==turn) 
                { if(Pan1614==turn) 
                { win++; } } } } }
                if(Pan1211==turn) 
                { if(Pan1312==turn) 
                { if(Pan1413==turn) 
                { if(Pan1514==turn) 
                { if(Pan1615==turn) 
                { win++; } } } } }
                if(Pan1212==turn) 
                { if(Pan1313==turn) 
                { if(Pan1414==turn) 
                { if(Pan1515==turn) 
                { if(Pan1616==turn) 
                { win++; } } } } }
                if(Pan1213==turn) 
                { if(Pan1314==turn) 
                { if(Pan1415==turn) 
                { if(Pan1516==turn) 
                { if(Pan1617==turn) 
                { win++; } } } } }
                if(Pan1214==turn) 
                { if(Pan1315==turn) 
                { if(Pan1416==turn) 
                { if(Pan1517==turn) 
                { if(Pan1618==turn) 
                { win++; } } } } }
                if(Pan1215==turn) 
                { if(Pan1316==turn) 
                { if(Pan1417==turn) 
                { if(Pan1518==turn) 
                { if(Pan1619==turn) 
                { win++; } } } } }
                if(Pan1301==turn) 
                { if(Pan1402==turn) 
                { if(Pan1503==turn) 
                { if(Pan1604==turn) 
                { if(Pan1705==turn) 
                { win++; } } } } }
                if(Pan1302==turn) 
                { if(Pan1403==turn) 
                { if(Pan1504==turn) 
                { if(Pan1605==turn) 
                { if(Pan1706==turn) 
                { win++; } } } } }
                if(Pan1303==turn) 
                { if(Pan1404==turn) 
                { if(Pan1505==turn) 
                { if(Pan1606==turn) 
                { if(Pan1707==turn) 
                { win++; } } } } }
                if(Pan1304==turn) 
                { if(Pan1405==turn) 
                { if(Pan1506==turn) 
                { if(Pan1607==turn) 
                { if(Pan1708==turn) 
                { win++; } } } } }
                if(Pan1305==turn) 
                { if(Pan1406==turn) 
                { if(Pan1507==turn) 
                { if(Pan1608==turn) 
                { if(Pan1709==turn) 
                { win++; } } } } }
                if(Pan1306==turn) 
                { if(Pan1407==turn) 
                { if(Pan1508==turn) 
                { if(Pan1609==turn) 
                { if(Pan1710==turn) 
                { win++; } } } } }
                if(Pan1307==turn) 
                { if(Pan1408==turn) 
                { if(Pan1509==turn) 
                { if(Pan1610==turn) 
                { if(Pan1711==turn) 
                { win++; } } } } }
                if(Pan1308==turn) 
                { if(Pan1409==turn) 
                { if(Pan1510==turn) 
                { if(Pan1611==turn) 
                { if(Pan1712==turn) 
                { win++; } } } } }
                if(Pan1309==turn) 
                { if(Pan1410==turn) 
                { if(Pan1511==turn) 
                { if(Pan1612==turn) 
                { if(Pan1713==turn) 
                { win++; } } } } }
                if(Pan1310==turn) 
                { if(Pan1411==turn) 
                { if(Pan1512==turn) 
                { if(Pan1613==turn) 
                { if(Pan1714==turn) 
                { win++; } } } } }
                if(Pan1311==turn) 
                { if(Pan1412==turn) 
                { if(Pan1513==turn) 
                { if(Pan1614==turn) 
                { if(Pan1715==turn) 
                { win++; } } } } }
                if(Pan1312==turn) 
                { if(Pan1413==turn) 
                { if(Pan1514==turn) 
                { if(Pan1615==turn) 
                { if(Pan1716==turn) 
                { win++; } } } } }
                if(Pan1313==turn) 
                { if(Pan1414==turn) 
                { if(Pan1515==turn) 
                { if(Pan1616==turn) 
                { if(Pan1717==turn) 
                { win++; } } } } }
                if(Pan1314==turn) 
                { if(Pan1415==turn) 
                { if(Pan1516==turn) 
                { if(Pan1617==turn) 
                { if(Pan1718==turn) 
                { win++; } } } } }
                if(Pan1315==turn) 
                { if(Pan1416==turn) 
                { if(Pan1517==turn) 
                { if(Pan1618==turn) 
                { if(Pan1719==turn) 
                { win++; } } } } }
                if(Pan1401==turn) 
                { if(Pan1502==turn) 
                { if(Pan1603==turn) 
                { if(Pan1704==turn) 
                { if(Pan1805==turn) 
                { win++; } } } } }
                if(Pan1402==turn) 
                { if(Pan1503==turn) 
                { if(Pan1604==turn) 
                { if(Pan1705==turn) 
                { if(Pan1806==turn) 
                { win++; } } } } }
                if(Pan1403==turn) 
                { if(Pan1504==turn) 
                { if(Pan1605==turn) 
                { if(Pan1706==turn) 
                { if(Pan1807==turn) 
                { win++; } } } } }
                if(Pan1404==turn) 
                { if(Pan1505==turn) 
                { if(Pan1606==turn) 
                { if(Pan1707==turn) 
                { if(Pan1808==turn) 
                { win++; } } } } }
                if(Pan1405==turn) 
                { if(Pan1506==turn) 
                { if(Pan1607==turn) 
                { if(Pan1708==turn) 
                { if(Pan1809==turn) 
                { win++; } } } } }
                if(Pan1406==turn) 
                { if(Pan1507==turn) 
                { if(Pan1608==turn) 
                { if(Pan1709==turn) 
                { if(Pan1810==turn) 
                { win++; } } } } }
                if(Pan1407==turn) 
                { if(Pan1508==turn) 
                { if(Pan1609==turn) 
                { if(Pan1710==turn) 
                { if(Pan1811==turn) 
                { win++; } } } } }
                if(Pan1408==turn) 
                { if(Pan1509==turn) 
                { if(Pan1610==turn) 
                { if(Pan1711==turn) 
                { if(Pan1812==turn) 
                { win++; } } } } }
                if(Pan1409==turn) 
                { if(Pan1510==turn) 
                { if(Pan1611==turn) 
                { if(Pan1712==turn) 
                { if(Pan1813==turn) 
                { win++; } } } } }
                if(Pan1410==turn) 
                { if(Pan1511==turn) 
                { if(Pan1612==turn) 
                { if(Pan1713==turn) 
                { if(Pan1814==turn) 
                { win++; } } } } }
                if(Pan1411==turn) 
                { if(Pan1512==turn) 
                { if(Pan1613==turn) 
                { if(Pan1714==turn) 
                { if(Pan1815==turn) 
                { win++; } } } } }
                if(Pan1412==turn) 
                { if(Pan1513==turn) 
                { if(Pan1614==turn) 
                { if(Pan1715==turn) 
                { if(Pan1816==turn) 
                { win++; } } } } }
                if(Pan1413==turn) 
                { if(Pan1514==turn) 
                { if(Pan1615==turn) 
                { if(Pan1716==turn) 
                { if(Pan1817==turn) 
                { win++; } } } } }
                if(Pan1414==turn) 
                { if(Pan1515==turn) 
                { if(Pan1616==turn) 
                { if(Pan1717==turn) 
                { if(Pan1818==turn) 
                { win++; } } } } }
                if(Pan1415==turn) 
                { if(Pan1516==turn) 
                { if(Pan1617==turn) 
                { if(Pan1718==turn) 
                { if(Pan1819==turn) 
                { win++; } } } } }
                if(Pan1501==turn) 
                { if(Pan1602==turn) 
                { if(Pan1703==turn) 
                { if(Pan1804==turn) 
                { if(Pan1905==turn) 
                { win++; } } } } }
                if(Pan1502==turn) 
                { if(Pan1603==turn) 
                { if(Pan1704==turn) 
                { if(Pan1805==turn) 
                { if(Pan1906==turn) 
                { win++; } } } } }
                if(Pan1503==turn) 
                { if(Pan1604==turn) 
                { if(Pan1705==turn) 
                { if(Pan1806==turn) 
                { if(Pan1907==turn) 
                { win++; } } } } }
                if(Pan1504==turn) 
                { if(Pan1605==turn) 
                { if(Pan1706==turn) 
                { if(Pan1807==turn) 
                { if(Pan1908==turn) 
                { win++; } } } } }
                if(Pan1505==turn) 
                { if(Pan1606==turn) 
                { if(Pan1707==turn) 
                { if(Pan1808==turn) 
                { if(Pan1909==turn) 
                { win++; } } } } }
                if(Pan1506==turn) 
                { if(Pan1607==turn) 
                { if(Pan1708==turn) 
                { if(Pan1809==turn) 
                { if(Pan1910==turn) 
                { win++; } } } } }
                if(Pan1507==turn) 
                { if(Pan1608==turn) 
                { if(Pan1709==turn) 
                { if(Pan1810==turn) 
                { if(Pan1911==turn) 
                { win++; } } } } }
                if(Pan1508==turn) 
                { if(Pan1609==turn) 
                { if(Pan1710==turn) 
                { if(Pan1811==turn) 
                { if(Pan1912==turn) 
                { win++; } } } } }
                if(Pan1509==turn) 
                { if(Pan1610==turn) 
                { if(Pan1711==turn) 
                { if(Pan1812==turn) 
                { if(Pan1913==turn) 
                { win++; } } } } }
                if(Pan1510==turn) 
                { if(Pan1611==turn) 
                { if(Pan1712==turn) 
                { if(Pan1813==turn) 
                { if(Pan1914==turn) 
                { win++; } } } } }
                if(Pan1511==turn) 
                { if(Pan1612==turn) 
                { if(Pan1713==turn) 
                { if(Pan1814==turn) 
                { if(Pan1915==turn) 
                { win++; } } } } }
                if(Pan1512==turn) 
                { if(Pan1613==turn) 
                { if(Pan1714==turn) 
                { if(Pan1815==turn) 
                { if(Pan1916==turn) 
                { win++; } } } } }
                if(Pan1513==turn) 
                { if(Pan1614==turn) 
                { if(Pan1715==turn) 
                { if(Pan1816==turn) 
                { if(Pan1917==turn) 
                { win++; } } } } }
                if(Pan1514==turn) 
                { if(Pan1615==turn) 
                { if(Pan1716==turn) 
                { if(Pan1817==turn) 
                { if(Pan1918==turn) 
                { win++; } } } } }
                if(Pan1515==turn) 
                { if(Pan1616==turn) 
                { if(Pan1717==turn) 
                { if(Pan1818==turn) 
                { if(Pan1919==turn) 
                { win++; } } } } }

                ////////////////// y = x 대각선 검사 //////////////////////////////
                if(Pan0105==turn) 
                { if(Pan0204==turn) 
                { if(Pan0303==turn) 
                { if(Pan0402==turn) 
                { if(Pan0501==turn) 
                { win++; } } } } }
                if(Pan0106==turn) 
                { if(Pan0205==turn) 
                { if(Pan0304==turn) 
                { if(Pan0403==turn) 
                { if(Pan0502==turn) 
                { win++; } } } } }
                if(Pan0107==turn) 
                { if(Pan0206==turn) 
                { if(Pan0305==turn) 
                { if(Pan0404==turn) 
                { if(Pan0503==turn) 
                { win++; } } } } }
                if(Pan0108==turn) 
                { if(Pan0207==turn) 
                { if(Pan0306==turn) 
                { if(Pan0405==turn) 
                { if(Pan0504==turn) 
                { win++; } } } } }
                if(Pan0109==turn) 
                { if(Pan0208==turn) 
                { if(Pan0307==turn) 
                { if(Pan0406==turn) 
                { if(Pan0505==turn) 
                { win++; } } } } }
                if(Pan0113==turn) 
                { if(Pan0212==turn) 
                { if(Pan0311==turn) 
                { if(Pan0410==turn) 
                { if(Pan0509==turn) 
                { win++; } } } } }
                if(Pan0114==turn) 
                { if(Pan0213==turn) 
                { if(Pan0312==turn) 
                { if(Pan0411==turn) 
                { if(Pan0510==turn) 
                { win++; } } } } }
                if(Pan0115==turn) 
                { if(Pan0214==turn) 
                { if(Pan0313==turn) 
                { if(Pan0412==turn) 
                { if(Pan0511==turn) 
                { win++; } } } } }
                if(Pan0116==turn) 
                { if(Pan0215==turn) 
                { if(Pan0314==turn) 
                { if(Pan0413==turn) 
                { if(Pan0512==turn) 
                { win++; } } } } }
                if(Pan0117==turn) 
                { if(Pan0216==turn) 
                { if(Pan0315==turn) 
                { if(Pan0414==turn) 
                { if(Pan0513==turn) 
                { win++; } } } } }
                if(Pan0118==turn) 
                { if(Pan0217==turn) 
                { if(Pan0316==turn) 
                { if(Pan0415==turn) 
                { if(Pan0514==turn) 
                { win++; } } } } }
                if(Pan0119==turn) 
                { if(Pan0218==turn) 
                { if(Pan0317==turn) 
                { if(Pan0416==turn) 
                { if(Pan0515==turn) 
                { win++; } } } } }
                if(Pan0205==turn) 
                { if(Pan0304==turn) 
                { if(Pan0403==turn) 
                { if(Pan0502==turn) 
                { if(Pan0601==turn) 
                { win++; } } } } }
                if(Pan0206==turn) 
                { if(Pan0305==turn) 
                { if(Pan0404==turn) 
                { if(Pan0503==turn) 
                { if(Pan0602==turn) 
                { win++; } } } } }
                if(Pan0207==turn) 
                { if(Pan0306==turn) 
                { if(Pan0405==turn) 
                { if(Pan0504==turn) 
                { if(Pan0603==turn) 
                { win++; } } } } }
                if(Pan0208==turn) 
                { if(Pan0307==turn) 
                { if(Pan0406==turn) 
                { if(Pan0505==turn) 
                { if(Pan0604==turn) 
                { win++; } } } } }
                if(Pan0209==turn) 
                { if(Pan0308==turn) 
                { if(Pan0407==turn) 
                { if(Pan0506==turn) 
                { if(Pan0605==turn) 
                { win++; } } } } }
                if(Pan0213==turn) 
                { if(Pan0312==turn) 
                { if(Pan0411==turn) 
                { if(Pan0510==turn) 
                { if(Pan0609==turn) 
                { win++; } } } } }
                if(Pan0214==turn) 
                { if(Pan0313==turn) 
                { if(Pan0412==turn) 
                { if(Pan0511==turn) 
                { if(Pan0610==turn) 
                { win++; } } } } }
                if(Pan0215==turn) 
                { if(Pan0314==turn) 
                { if(Pan0413==turn) 
                { if(Pan0512==turn) 
                { if(Pan0611==turn) 
                { win++; } } } } }
                if(Pan0216==turn) 
                { if(Pan0315==turn) 
                { if(Pan0414==turn) 
                { if(Pan0513==turn) 
                { if(Pan0612==turn) 
                { win++; } } } } }
                if(Pan0217==turn) 
                { if(Pan0316==turn) 
                { if(Pan0415==turn) 
                { if(Pan0514==turn) 
                { if(Pan0613==turn) 
                { win++; } } } } }
                if(Pan0218==turn) 
                { if(Pan0317==turn) 
                { if(Pan0416==turn) 
                { if(Pan0515==turn) 
                { if(Pan0614==turn) 
                { win++; } } } } }
                if(Pan0219==turn) 
                { if(Pan0318==turn) 
                { if(Pan0417==turn) 
                { if(Pan0516==turn) 
                { if(Pan0615==turn) 
                { win++; } } } } }
                if(Pan0305==turn) 
                { if(Pan0404==turn) 
                { if(Pan0503==turn) 
                { if(Pan0602==turn) 
                { if(Pan0701==turn) 
                { win++; } } } } }
                if(Pan0306==turn) 
                { if(Pan0405==turn) 
                { if(Pan0504==turn) 
                { if(Pan0603==turn) 
                { if(Pan0702==turn) 
                { win++; } } } } }
                if(Pan0307==turn) 
                { if(Pan0406==turn) 
                { if(Pan0505==turn) 
                { if(Pan0604==turn) 
                { if(Pan0703==turn) 
                { win++; } } } } }
                if(Pan0308==turn) 
                { if(Pan0407==turn) 
                { if(Pan0506==turn) 
                { if(Pan0605==turn) 
                { if(Pan0704==turn) 
                { win++; } } } } }
                if(Pan0309==turn) 
                { if(Pan0408==turn) 
                { if(Pan0507==turn) 
                { if(Pan0606==turn) 
                { if(Pan0705==turn) 
                { win++; } } } } }
                if(Pan0313==turn) 
                { if(Pan0412==turn) 
                { if(Pan0511==turn) 
                { if(Pan0610==turn) 
                { if(Pan0709==turn) 
                { win++; } } } } }
                if(Pan0314==turn) 
                { if(Pan0413==turn) 
                { if(Pan0512==turn) 
                { if(Pan0611==turn) 
                { if(Pan0710==turn) 
                { win++; } } } } }
                if(Pan0315==turn) 
                { if(Pan0414==turn) 
                { if(Pan0513==turn) 
                { if(Pan0612==turn) 
                { if(Pan0711==turn) 
                { win++; } } } } }
                if(Pan0316==turn) 
                { if(Pan0415==turn) 
                { if(Pan0514==turn) 
                { if(Pan0613==turn) 
                { if(Pan0712==turn) 
                { win++; } } } } }
                if(Pan0317==turn) 
                { if(Pan0416==turn) 
                { if(Pan0515==turn) 
                { if(Pan0614==turn) 
                { if(Pan0713==turn) 
                { win++; } } } } }
                if(Pan0318==turn) 
                { if(Pan0417==turn) 
                { if(Pan0516==turn) 
                { if(Pan0615==turn) 
                { if(Pan0714==turn) 
                { win++; } } } } }
                if(Pan0319==turn) 
                { if(Pan0418==turn) 
                { if(Pan0517==turn) 
                { if(Pan0616==turn) 
                { if(Pan0715==turn) 
                { win++; } } } } }
                if(Pan0405==turn) 
                { if(Pan0504==turn) 
                { if(Pan0603==turn) 
                { if(Pan0702==turn) 
                { if(Pan0801==turn) 
                { win++; } } } } }
                if(Pan0406==turn) 
                { if(Pan0505==turn) 
                { if(Pan0604==turn) 
                { if(Pan0703==turn) 
                { if(Pan0802==turn) 
                { win++; } } } } }
                if(Pan0407==turn) 
                { if(Pan0506==turn) 
                { if(Pan0605==turn) 
                { if(Pan0704==turn) 
                { if(Pan0803==turn) 
                { win++; } } } } }
                if(Pan0408==turn) 
                { if(Pan0507==turn) 
                { if(Pan0606==turn) 
                { if(Pan0705==turn) 
                { if(Pan0804==turn) 
                { win++; } } } } }
                if(Pan0409==turn) 
                { if(Pan0508==turn) 
                { if(Pan0607==turn) 
                { if(Pan0706==turn) 
                { if(Pan0805==turn) 
                { win++; } } } } }
                if(Pan0413==turn) 
                { if(Pan0512==turn) 
                { if(Pan0611==turn) 
                { if(Pan0710==turn) 
                { if(Pan0809==turn) 
                { win++; } } } } }
                if(Pan0414==turn) 
                { if(Pan0513==turn) 
                { if(Pan0612==turn) 
                { if(Pan0711==turn) 
                { if(Pan0810==turn) 
                { win++; } } } } }
                if(Pan0415==turn) 
                { if(Pan0514==turn) 
                { if(Pan0613==turn) 
                { if(Pan0712==turn) 
                { if(Pan0811==turn) 
                { win++; } } } } }
                if(Pan0416==turn) 
                { if(Pan0515==turn) 
                { if(Pan0614==turn) 
                { if(Pan0713==turn) 
                { if(Pan0812==turn) 
                { win++; } } } } }
                if(Pan0417==turn) 
                { if(Pan0516==turn) 
                { if(Pan0615==turn) 
                { if(Pan0714==turn) 
                { if(Pan0813==turn) 
                { win++; } } } } }
                if(Pan0418==turn) 
                { if(Pan0517==turn) 
                { if(Pan0616==turn) 
                { if(Pan0715==turn) 
                { if(Pan0814==turn) 
                { win++; } } } } }
                if(Pan0419==turn) 
                { if(Pan0518==turn) 
                { if(Pan0617==turn) 
                { if(Pan0716==turn) 
                { if(Pan0815==turn) 
                { win++; } } } } }
                if(Pan0505==turn) 
                { if(Pan0604==turn) 
                { if(Pan0703==turn) 
                { if(Pan0802==turn) 
                { if(Pan0901==turn) 
                { win++; } } } } }
                if(Pan0506==turn) 
                { if(Pan0605==turn) 
                { if(Pan0704==turn) 
                { if(Pan0803==turn) 
                { if(Pan0902==turn) 
                { win++; } } } } }
                if(Pan0507==turn) 
                { if(Pan0606==turn) 
                { if(Pan0705==turn) 
                { if(Pan0804==turn) 
                { if(Pan0903==turn) 
                { win++; } } } } }
                if(Pan0508==turn) 
                { if(Pan0607==turn) 
                { if(Pan0706==turn) 
                { if(Pan0805==turn) 
                { if(Pan0904==turn) 
                { win++; } } } } }
                if(Pan0509==turn) 
                { if(Pan0608==turn) 
                { if(Pan0707==turn) 
                { if(Pan0806==turn) 
                { if(Pan0905==turn) 
                { win++; } } } } }
                if(Pan0513==turn) 
                { if(Pan0612==turn) 
                { if(Pan0711==turn) 
                { if(Pan0810==turn) 
                { if(Pan0909==turn) 
                { win++; } } } } }
                if(Pan0514==turn) 
                { if(Pan0613==turn) 
                { if(Pan0712==turn) 
                { if(Pan0811==turn) 
                { if(Pan0910==turn) 
                { win++; } } } } }
                if(Pan0515==turn) 
                { if(Pan0614==turn) 
                { if(Pan0713==turn) 
                { if(Pan0812==turn) 
                { if(Pan0911==turn) 
                { win++; } } } } }
                if(Pan0516==turn) 
                { if(Pan0615==turn) 
                { if(Pan0714==turn) 
                { if(Pan0813==turn) 
                { if(Pan0912==turn) 
                { win++; } } } } }
                if(Pan0517==turn) 
                { if(Pan0616==turn) 
                { if(Pan0715==turn) 
                { if(Pan0814==turn) 
                { if(Pan0913==turn) 
                { win++; } } } } }
                if(Pan0518==turn) 
                { if(Pan0617==turn) 
                { if(Pan0716==turn) 
                { if(Pan0815==turn) 
                { if(Pan0914==turn) 
                { win++; } } } } }
                if(Pan0519==turn) 
                { if(Pan0618==turn) 
                { if(Pan0717==turn) 
                { if(Pan0816==turn) 
                { if(Pan0915==turn) 
                { win++; } } } } }
                if(Pan0605==turn) 
                { if(Pan0704==turn) 
                { if(Pan0803==turn) 
                { if(Pan0902==turn) 
                { if(Pan1001==turn) 
                { win++; } } } } }
                if(Pan0606==turn) 
                { if(Pan0705==turn) 
                { if(Pan0804==turn) 
                { if(Pan0903==turn) 
                { if(Pan1002==turn) 
                { win++; } } } } }
                if(Pan0607==turn) 
                { if(Pan0706==turn) 
                { if(Pan0805==turn) 
                { if(Pan0904==turn) 
                { if(Pan1003==turn) 
                { win++; } } } } }
                if(Pan0608==turn) 
                { if(Pan0707==turn) 
                { if(Pan0806==turn) 
                { if(Pan0905==turn) 
                { if(Pan1004==turn) 
                { win++; } } } } }
                if(Pan0609==turn) 
                { if(Pan0708==turn) 
                { if(Pan0807==turn) 
                { if(Pan0906==turn) 
                { if(Pan1005==turn) 
                { win++; } } } } }
                if(Pan0613==turn) 
                { if(Pan0712==turn) 
                { if(Pan0811==turn) 
                { if(Pan0910==turn) 
                { if(Pan1009==turn) 
                { win++; } } } } }
                if(Pan0614==turn) 
                { if(Pan0713==turn) 
                { if(Pan0812==turn) 
                { if(Pan0911==turn) 
                { if(Pan1010==turn) 
                { win++; } } } } }
                if(Pan0615==turn) 
                { if(Pan0714==turn) 
                { if(Pan0813==turn) 
                { if(Pan0912==turn) 
                { if(Pan1011==turn) 
                { win++; } } } } }
                if(Pan0616==turn) 
                { if(Pan0715==turn) 
                { if(Pan0814==turn) 
                { if(Pan0913==turn) 
                { if(Pan1012==turn) 
                { win++; } } } } }
                if(Pan0617==turn) 
                { if(Pan0716==turn) 
                { if(Pan0815==turn) 
                { if(Pan0914==turn) 
                { if(Pan1013==turn) 
                { win++; } } } } }
                if(Pan0618==turn) 
                { if(Pan0717==turn) 
                { if(Pan0816==turn) 
                { if(Pan0915==turn) 
                { if(Pan1014==turn) 
                { win++; } } } } }
                if(Pan0619==turn) 
                { if(Pan0718==turn) 
                { if(Pan0817==turn) 
                { if(Pan0916==turn) 
                { if(Pan1015==turn) 
                { win++; } } } } }
                if(Pan0705==turn) 
                { if(Pan0804==turn) 
                { if(Pan0903==turn) 
                { if(Pan1002==turn) 
                { if(Pan1101==turn) 
                { win++; } } } } }
                if(Pan0706==turn) 
                { if(Pan0805==turn) 
                { if(Pan0904==turn) 
                { if(Pan1003==turn) 
                { if(Pan1102==turn) 
                { win++; } } } } }
                if(Pan0707==turn) 
                { if(Pan0806==turn) 
                { if(Pan0905==turn) 
                { if(Pan1004==turn) 
                { if(Pan1103==turn) 
                { win++; } } } } }
                if(Pan0708==turn) 
                { if(Pan0807==turn) 
                { if(Pan0906==turn) 
                { if(Pan1005==turn) 
                { if(Pan1104==turn) 
                { win++; } } } } }
                if(Pan0709==turn) 
                { if(Pan0808==turn) 
                { if(Pan0907==turn) 
                { if(Pan1006==turn) 
                { if(Pan1105==turn) 
                { win++; } } } } }
                if(Pan0712==turn) 
                { if(Pan0811==turn) 
                { if(Pan0910==turn) 
                { if(Pan1009==turn) 
                { if(Pan1108==turn) 
                { win++; } } } } }
                if(Pan0713==turn) 
                { if(Pan0812==turn) 
                { if(Pan0911==turn) 
                { if(Pan1010==turn) 
                { if(Pan1109==turn) 
                { win++; } } } } }
                if(Pan0714==turn) 
                { if(Pan0813==turn) 
                { if(Pan0912==turn) 
                { if(Pan1011==turn) 
                { if(Pan1110==turn) 
                { win++; } } } } }
                if(Pan0715==turn) 
                { if(Pan0814==turn) 
                { if(Pan0913==turn) 
                { if(Pan1012==turn) 
                { if(Pan1111==turn) 
                { win++; } } } } }
                if(Pan0716==turn) 
                { if(Pan0815==turn) 
                { if(Pan0914==turn) 
                { if(Pan1013==turn) 
                { if(Pan1112==turn) 
                { win++; } } } } }
                if(Pan0717==turn) 
                { if(Pan0816==turn) 
                { if(Pan0915==turn) 
                { if(Pan1014==turn) 
                { if(Pan1113==turn) 
                { win++; } } } } }
                if(Pan0718==turn) 
                { if(Pan0817==turn) 
                { if(Pan0916==turn) 
                { if(Pan1015==turn) 
                { if(Pan1114==turn) 
                { win++; } } } } }
                if(Pan0719==turn) 
                { if(Pan0818==turn) 
                { if(Pan0917==turn) 
                { if(Pan1016==turn) 
                { if(Pan1115==turn) 
                { win++; } } } } }
                if(Pan0805==turn) 
                { if(Pan0904==turn) 
                { if(Pan1003==turn) 
                { if(Pan1102==turn) 
                { if(Pan1201==turn) 
                { win++; } } } } }
                if(Pan0806==turn) 
                { if(Pan0905==turn) 
                { if(Pan1004==turn) 
                { if(Pan1103==turn) 
                { if(Pan1202==turn) 
                { win++; } } } } }
                if(Pan0807==turn) 
                { if(Pan0906==turn) 
                { if(Pan1005==turn) 
                { if(Pan1104==turn) 
                { if(Pan1203==turn) 
                { win++; } } } } }
                if(Pan0808==turn) 
                { if(Pan0907==turn) 
                { if(Pan1006==turn) 
                { if(Pan1105==turn) 
                { if(Pan1204==turn) 
                { win++; } } } } }
                if(Pan0809==turn) 
                { if(Pan0908==turn) 
                { if(Pan1007==turn) 
                { if(Pan1106==turn) 
                { if(Pan1205==turn) 
                { win++; } } } } }
                if(Pan0811==turn) 
                { if(Pan0910==turn) 
                { if(Pan1009==turn) 
                { if(Pan1108==turn) 
                { if(Pan1207==turn) 
                { win++; } } } } }
                if(Pan0813==turn) 
                { if(Pan0912==turn) 
                { if(Pan1011==turn) 
                { if(Pan1110==turn) 
                { if(Pan1209==turn) 
                { win++; } } } } }
                if(Pan0814==turn) 
                { if(Pan0913==turn) 
                { if(Pan1012==turn) 
                { if(Pan1111==turn) 
                { if(Pan1210==turn) 
                { win++; } } } } }
                if(Pan0815==turn) 
                { if(Pan0914==turn) 
                { if(Pan1013==turn) 
                { if(Pan1112==turn) 
                { if(Pan1211==turn) 
                { win++; } } } } }
                if(Pan0816==turn) 
                { if(Pan0915==turn) 
                { if(Pan1014==turn) 
                { if(Pan1113==turn) 
                { if(Pan1212==turn) 
                { win++; } } } } }
                if(Pan0817==turn) 
                { if(Pan0916==turn) 
                { if(Pan1015==turn) 
                { if(Pan1114==turn) 
                { if(Pan1213==turn) 
                { win++; } } } } }
                if(Pan0818==turn) 
                { if(Pan0917==turn) 
                { if(Pan1016==turn) 
                { if(Pan1115==turn) 
                { if(Pan1214==turn) 
                { win++; } } } } }
                if(Pan0819==turn) 
                { if(Pan0918==turn) 
                { if(Pan1017==turn) 
                { if(Pan1116==turn) 
                { if(Pan1215==turn) 
                { win++; } } } } }
                if(Pan0905==turn) 
                { if(Pan1004==turn) 
                { if(Pan1103==turn) 
                { if(Pan1202==turn) 
                { if(Pan1301==turn) 
                { win++; } } } } }
                if(Pan0906==turn) 
                { if(Pan1005==turn) 
                { if(Pan1104==turn) 
                { if(Pan1203==turn) 
                { if(Pan1302==turn) 
                { win++; } } } } }
                if(Pan0907==turn) 
                { if(Pan1006==turn) 
                { if(Pan1105==turn) 
                { if(Pan1204==turn) 
                { if(Pan1303==turn) 
                { win++; } } } } }
                if(Pan0908==turn) 
                { if(Pan1007==turn) 
                { if(Pan1106==turn) 
                { if(Pan1205==turn) 
                { if(Pan1304==turn) 
                { win++; } } } } }
                if(Pan0909==turn) 
                { if(Pan1008==turn) 
                { if(Pan1107==turn) 
                { if(Pan1206==turn) 
                { if(Pan1305==turn) 
                { win++; } } } } }
                if(Pan0910==turn) 
                { if(Pan1009==turn) 
                { if(Pan1108==turn) 
                { if(Pan1207==turn) 
                { if(Pan1306==turn) 
                { win++; } } } } }
                if(Pan0913==turn) 
                { if(Pan1012==turn) 
                { if(Pan1111==turn) 
                { if(Pan1210==turn) 
                { if(Pan1309==turn) 
                { win++; } } } } }
                if(Pan0914==turn) 
                { if(Pan1013==turn) 
                { if(Pan1112==turn) 
                { if(Pan1211==turn) 
                { if(Pan1310==turn) 
                { win++; } } } } }
                if(Pan0915==turn) 
                { if(Pan1014==turn) 
                { if(Pan1113==turn) 
                { if(Pan1212==turn) 
                { if(Pan1311==turn) 
                { win++; } } } } }
                if(Pan0916==turn) 
                { if(Pan1015==turn) 
                { if(Pan1114==turn) 
                { if(Pan1213==turn) 
                { if(Pan1312==turn) 
                { win++; } } } } }
                if(Pan0917==turn) 
                { if(Pan1016==turn) 
                { if(Pan1115==turn) 
                { if(Pan1214==turn) 
                { if(Pan1313==turn) 
                { win++; } } } } }
                if(Pan0918==turn) 
                { if(Pan1017==turn) 
                { if(Pan1116==turn) 
                { if(Pan1215==turn) 
                { if(Pan1314==turn) 
                { win++; } } } } }
                if(Pan0919==turn) 
                { if(Pan1018==turn) 
                { if(Pan1117==turn) 
                { if(Pan1216==turn) 
                { if(Pan1315==turn) 
                { win++; } } } } }
                if(Pan1005==turn) 
                { if(Pan1104==turn) 
                { if(Pan1203==turn) 
                { if(Pan1302==turn) 
                { if(Pan1401==turn) 
                { win++; } } } } }
                if(Pan1006==turn) 
                { if(Pan1105==turn) 
                { if(Pan1204==turn) 
                { if(Pan1303==turn) 
                { if(Pan1402==turn) 
                { win++; } } } } }
                if(Pan1007==turn) 
                { if(Pan1106==turn) 
                { if(Pan1205==turn) 
                { if(Pan1304==turn) 
                { if(Pan1403==turn) 
                { win++; } } } } }
                if(Pan1008==turn) 
                { if(Pan1107==turn) 
                { if(Pan1206==turn) 
                { if(Pan1305==turn) 
                { if(Pan1404==turn) 
                { win++; } } } } }
                if(Pan1009==turn) 
                { if(Pan1108==turn) 
                { if(Pan1207==turn) 
                { if(Pan1306==turn) 
                { if(Pan1405==turn) 
                { win++; } } } } }
                if(Pan1010==turn) 
                { if(Pan1109==turn) 
                { if(Pan1208==turn) 
                { if(Pan1307==turn) 
                { if(Pan1406==turn) 
                { win++; } } } } }
                if(Pan1011==turn) 
                { if(Pan1110==turn) 
                { if(Pan1209==turn) 
                { if(Pan1308==turn) 
                { if(Pan1407==turn) 
                { win++; } } } } }
                if(Pan1012==turn) 
                { if(Pan1111==turn) 
                { if(Pan1210==turn) 
                { if(Pan1309==turn) 
                { if(Pan1408==turn) 
                { win++; } } } } }
                if(Pan1013==turn) 
                { if(Pan1112==turn) 
                { if(Pan1211==turn) 
                { if(Pan1310==turn) 
                { if(Pan1409==turn) 
                { win++; } } } } }
                if(Pan1014==turn) 
                { if(Pan1113==turn) 
                { if(Pan1212==turn) 
                { if(Pan1311==turn) 
                { if(Pan1410==turn) 
                { win++; } } } } }
                if(Pan1015==turn) 
                { if(Pan1114==turn) 
                { if(Pan1213==turn) 
                { if(Pan1312==turn) 
                { if(Pan1411==turn) 
                { win++; } } } } }
                if(Pan1016==turn) 
                { if(Pan1115==turn) 
                { if(Pan1214==turn) 
                { if(Pan1313==turn) 
                { if(Pan1412==turn) 
                { win++; } } } } }
                if(Pan1017==turn) 
                { if(Pan1116==turn) 
                { if(Pan1215==turn) 
                { if(Pan1314==turn) 
                { if(Pan1413==turn) 
                { win++; } } } } }
                if(Pan1018==turn) 
                { if(Pan1117==turn) 
                { if(Pan1216==turn) 
                { if(Pan1315==turn) 
                { if(Pan1414==turn) 
                { win++; } } } } }
                if(Pan1019==turn) 
                { if(Pan1118==turn) 
                { if(Pan1217==turn) 
                { if(Pan1316==turn) 
                { if(Pan1415==turn) 
                { win++; } } } } }
                if(Pan1105==turn) 
                { if(Pan1204==turn) 
                { if(Pan1303==turn) 
                { if(Pan1402==turn) 
                { if(Pan1501==turn) 
                { win++; } } } } }
                if(Pan1106==turn) 
                { if(Pan1205==turn) 
                { if(Pan1304==turn) 
                { if(Pan1403==turn) 
                { if(Pan1502==turn) 
                { win++; } } } } }
                if(Pan1107==turn) 
                { if(Pan1206==turn) 
                { if(Pan1305==turn) 
                { if(Pan1404==turn) 
                { if(Pan1503==turn) 
                { win++; } } } } }
                if(Pan1108==turn) 
                { if(Pan1207==turn) 
                { if(Pan1306==turn) 
                { if(Pan1405==turn) 
                { if(Pan1504==turn) 
                { win++; } } } } }
                if(Pan1109==turn) 
                { if(Pan1208==turn) 
                { if(Pan1307==turn) 
                { if(Pan1406==turn) 
                { if(Pan1505==turn) 
                { win++; } } } } }
                if(Pan1110==turn) 
                { if(Pan1209==turn) 
                { if(Pan1308==turn) 
                { if(Pan1407==turn) 
                { if(Pan1506==turn) 
                { win++; } } } } }
                if(Pan1111==turn) 
                { if(Pan1210==turn) 
                { if(Pan1309==turn) 
                { if(Pan1408==turn) 
                { if(Pan1507==turn) 
                { win++; } } } } }
                if(Pan1112==turn) 
                { if(Pan1211==turn) 
                { if(Pan1310==turn) 
                { if(Pan1409==turn) 
                { if(Pan1508==turn) 
                { win++; } } } } }
                if(Pan1113==turn) 
                { if(Pan1212==turn) 
                { if(Pan1311==turn) 
                { if(Pan1410==turn) 
                { if(Pan1509==turn) 
                { win++; } } } } }
                if(Pan1114==turn) 
                { if(Pan1213==turn) 
                { if(Pan1312==turn) 
                { if(Pan1411==turn) 
                { if(Pan1510==turn) 
                { win++; } } } } }
                if(Pan1115==turn) 
                { if(Pan1214==turn) 
                { if(Pan1313==turn) 
                { if(Pan1412==turn) 
                { if(Pan1511==turn) 
                { win++; } } } } }
                if(Pan1116==turn) 
                { if(Pan1215==turn) 
                { if(Pan1314==turn) 
                { if(Pan1413==turn) 
                { if(Pan1512==turn) 
                { win++; } } } } }
                if(Pan1117==turn) 
                { if(Pan1216==turn) 
                { if(Pan1315==turn) 
                { if(Pan1414==turn) 
                { if(Pan1513==turn) 
                { win++; } } } } }
                if(Pan1118==turn) 
                { if(Pan1217==turn) 
                { if(Pan1316==turn) 
                { if(Pan1415==turn) 
                { if(Pan1514==turn) 
                { win++; } } } } }
                if(Pan1119==turn) 
                { if(Pan1218==turn) 
                { if(Pan1317==turn) 
                { if(Pan1416==turn) 
                { if(Pan1515==turn) 
                { win++; } } } } }
                if(Pan1205==turn) 
                { if(Pan1304==turn) 
                { if(Pan1403==turn) 
                { if(Pan1502==turn) 
                { if(Pan1601==turn) 
                { win++; } } } } }
                if(Pan1206==turn) 
                { if(Pan1305==turn) 
                { if(Pan1404==turn) 
                { if(Pan1503==turn) 
                { if(Pan1602==turn) 
                { win++; } } } } }
                if(Pan1207==turn) 
                { if(Pan1306==turn) 
                { if(Pan1405==turn) 
                { if(Pan1504==turn) 
                { if(Pan1603==turn) 
                { win++; } } } } }
                if(Pan1208==turn) 
                { if(Pan1307==turn) 
                { if(Pan1406==turn) 
                { if(Pan1505==turn) 
                { if(Pan1604==turn) 
                { win++; } } } } }
                if(Pan1209==turn) 
                { if(Pan1308==turn) 
                { if(Pan1407==turn) 
                { if(Pan1506==turn) 
                { if(Pan1605==turn) 
                { win++; } } } } }
                if(Pan1210==turn) 
                { if(Pan1309==turn) 
                { if(Pan1408==turn) 
                { if(Pan1507==turn) 
                { if(Pan1606==turn) 
                { win++; } } } } }
                if(Pan1211==turn) 
                { if(Pan1310==turn) 
                { if(Pan1409==turn) 
                { if(Pan1508==turn) 
                { if(Pan1607==turn) 
                { win++; } } } } }
                if(Pan1212==turn) 
                { if(Pan1311==turn) 
                { if(Pan1410==turn) 
                { if(Pan1509==turn) 
                { if(Pan1608==turn) 
                { win++; } } } } }
                if(Pan1213==turn) 
                { if(Pan1312==turn) 
                { if(Pan1411==turn) 
                { if(Pan1510==turn) 
                { if(Pan1609==turn) 
                { win++; } } } } }
                if(Pan1214==turn) 
                { if(Pan1313==turn) 
                { if(Pan1412==turn) 
                { if(Pan1511==turn) 
                { if(Pan1610==turn) 
                { win++; } } } } }
                if(Pan1215==turn) 
                { if(Pan1314==turn) 
                { if(Pan1413==turn) 
                { if(Pan1512==turn) 
                { if(Pan1611==turn) 
                { win++; } } } } }
                if(Pan1216==turn) 
                { if(Pan1315==turn) 
                { if(Pan1414==turn) 
                { if(Pan1513==turn) 
                { if(Pan1612==turn) 
                { win++; } } } } }
                if(Pan1217==turn) 
                { if(Pan1316==turn) 
                { if(Pan1415==turn) 
                { if(Pan1514==turn) 
                { if(Pan1613==turn) 
                { win++; } } } } }
                if(Pan1218==turn) 
                { if(Pan1317==turn) 
                { if(Pan1416==turn) 
                { if(Pan1515==turn) 
                { if(Pan1614==turn) 
                { win++; } } } } }
                if(Pan1219==turn) 
                { if(Pan1318==turn) 
                { if(Pan1417==turn) 
                { if(Pan1516==turn) 
                { if(Pan1615==turn) 
                { win++; } } } } }
                if(Pan1305==turn) 
                { if(Pan1404==turn) 
                { if(Pan1503==turn) 
                { if(Pan1602==turn) 
                { if(Pan1701==turn) 
                { win++; } } } } }
                if(Pan1306==turn) 
                { if(Pan1405==turn) 
                { if(Pan1504==turn) 
                { if(Pan1603==turn) 
                { if(Pan1702==turn) 
                { win++; } } } } }
                if(Pan1307==turn) 
                { if(Pan1406==turn) 
                { if(Pan1505==turn) 
                { if(Pan1604==turn) 
                { if(Pan1703==turn) 
                { win++; } } } } }
                if(Pan1308==turn) 
                { if(Pan1407==turn) 
                { if(Pan1506==turn) 
                { if(Pan1605==turn) 
                { if(Pan1704==turn) 
                { win++; } } } } }
                if(Pan1309==turn) 
                { if(Pan1408==turn) 
                { if(Pan1507==turn) 
                { if(Pan1606==turn) 
                { if(Pan1705==turn) 
                { win++; } } } } }
                if(Pan1310==turn) 
                { if(Pan1409==turn) 
                { if(Pan1508==turn) 
                { if(Pan1607==turn) 
                { if(Pan1706==turn) 
                { win++; } } } } }
                if(Pan1311==turn) 
                { if(Pan1410==turn) 
                { if(Pan1509==turn) 
                { if(Pan1608==turn) 
                { if(Pan1707==turn) 
                { win++; } } } } }
                if(Pan1312==turn) 
                { if(Pan1411==turn) 
                { if(Pan1510==turn) 
                { if(Pan1609==turn) 
                { if(Pan1708==turn) 
                { win++; } } } } }
                if(Pan1313==turn) 
                { if(Pan1412==turn) 
                { if(Pan1511==turn) 
                { if(Pan1610==turn) 
                { if(Pan1709==turn) 
                { win++; } } } } }
                if(Pan1314==turn) 
                { if(Pan1413==turn) 
                { if(Pan1512==turn) 
                { if(Pan1611==turn) 
                { if(Pan1710==turn) 
                { win++; } } } } }
                if(Pan1315==turn) 
                { if(Pan1414==turn) 
                { if(Pan1513==turn) 
                { if(Pan1612==turn) 
                { if(Pan1711==turn) 
                { win++; } } } } }
                if(Pan1316==turn) 
                { if(Pan1415==turn) 
                { if(Pan1514==turn) 
                { if(Pan1613==turn) 
                { if(Pan1712==turn) 
                { win++; } } } } }
                if(Pan1317==turn) 
                { if(Pan1416==turn) 
                { if(Pan1515==turn) 
                { if(Pan1614==turn) 
                { if(Pan1713==turn) 
                { win++; } } } } }
                if(Pan1318==turn) 
                { if(Pan1417==turn) 
                { if(Pan1516==turn) 
                { if(Pan1615==turn) 
                { if(Pan1714==turn) 
                { win++; } } } } }
                if(Pan1319==turn) 
                { if(Pan1418==turn) 
                { if(Pan1517==turn) 
                { if(Pan1616==turn) 
                { if(Pan1715==turn) 
                { win++; } } } } }
                if(Pan1405==turn) 
                { if(Pan1504==turn) 
                { if(Pan1603==turn) 
                { if(Pan1702==turn) 
                { if(Pan1801==turn) 
                { win++; } } } } }
                if(Pan1406==turn) 
                { if(Pan1505==turn) 
                { if(Pan1604==turn) 
                { if(Pan1703==turn) 
                { if(Pan1802==turn) 
                { win++; } } } } }
                if(Pan1407==turn) 
                { if(Pan1506==turn) 
                { if(Pan1605==turn) 
                { if(Pan1704==turn) 
                { if(Pan1803==turn) 
                { win++; } } } } }
                if(Pan1408==turn) 
                { if(Pan1507==turn) 
                { if(Pan1606==turn) 
                { if(Pan1705==turn) 
                { if(Pan1804==turn) 
                { win++; } } } } }
                if(Pan1409==turn) 
                { if(Pan1508==turn) 
                { if(Pan1607==turn) 
                { if(Pan1706==turn) 
                { if(Pan1805==turn) 
                { win++; } } } } }
                if(Pan1410==turn) 
                { if(Pan1509==turn) 
                { if(Pan1608==turn) 
                { if(Pan1707==turn) 
                { if(Pan1806==turn) 
                { win++; } } } } }
                if(Pan1411==turn) 
                { if(Pan1510==turn) 
                { if(Pan1609==turn) 
                { if(Pan1708==turn) 
                { if(Pan1807==turn) 
                { win++; } } } } }
                if(Pan1412==turn) 
                { if(Pan1511==turn) 
                { if(Pan1610==turn) 
                { if(Pan1709==turn) 
                { if(Pan1808==turn) 
                { win++; } } } } }
                if(Pan1413==turn) 
                { if(Pan1512==turn) 
                { if(Pan1611==turn) 
                { if(Pan1710==turn) 
                { if(Pan1809==turn) 
                { win++; } } } } }
                if(Pan1414==turn) 
                { if(Pan1513==turn) 
                { if(Pan1612==turn) 
                { if(Pan1711==turn) 
                { if(Pan1810==turn) 
                { win++; } } } } }
                if(Pan1415==turn) 
                { if(Pan1514==turn) 
                { if(Pan1613==turn) 
                { if(Pan1712==turn) 
                { if(Pan1811==turn) 
                { win++; } } } } }
                if(Pan1416==turn) 
                { if(Pan1515==turn) 
                { if(Pan1614==turn) 
                { if(Pan1713==turn) 
                { if(Pan1812==turn) 
                { win++; } } } } }
                if(Pan1417==turn) 
                { if(Pan1516==turn) 
                { if(Pan1615==turn) 
                { if(Pan1714==turn) 
                { if(Pan1813==turn) 
                { win++; } } } } }
                if(Pan1418==turn) 
                { if(Pan1517==turn) 
                { if(Pan1616==turn) 
                { if(Pan1715==turn) 
                { if(Pan1814==turn) 
                { win++; } } } } }
                if(Pan1419==turn) 
                { if(Pan1518==turn) 
                { if(Pan1617==turn) 
                { if(Pan1716==turn) 
                { if(Pan1815==turn) 
                { win++; } } } } }
                if(Pan1505==turn) 
                { if(Pan1604==turn) 
                { if(Pan1703==turn) 
                { if(Pan1802==turn) 
                { if(Pan1901==turn) 
                { win++; } } } } }
                if(Pan1506==turn) 
                { if(Pan1605==turn) 
                { if(Pan1704==turn) 
                { if(Pan1803==turn) 
                { if(Pan1902==turn) 
                { win++; } } } } }
                if(Pan1507==turn) 
                { if(Pan1606==turn) 
                { if(Pan1705==turn) 
                { if(Pan1804==turn) 
                { if(Pan1903==turn) 
                { win++; } } } } }
                if(Pan1508==turn) 
                { if(Pan1607==turn) 
                { if(Pan1706==turn) 
                { if(Pan1805==turn) 
                { if(Pan1904==turn) 
                { win++; } } } } }
                if(Pan1509==turn) 
                { if(Pan1608==turn) 
                { if(Pan1707==turn) 
                { if(Pan1806==turn) 
                { if(Pan1905==turn) 
                { win++; } } } } }
                if(Pan1510==turn) 
                { if(Pan1609==turn) 
                { if(Pan1708==turn) 
                { if(Pan1807==turn) 
                { if(Pan1906==turn) 
                { win++; } } } } }
                if(Pan1511==turn) 
                { if(Pan1610==turn) 
                { if(Pan1709==turn) 
                { if(Pan1808==turn) 
                { if(Pan1907==turn) 
                { win++; } } } } }
                if(Pan1512==turn) 
                { if(Pan1611==turn) 
                { if(Pan1710==turn) 
                { if(Pan1809==turn) 
                { if(Pan1908==turn) 
                { win++; } } } } }
                if(Pan1513==turn) 
                { if(Pan1612==turn) 
                { if(Pan1711==turn) 
                { if(Pan1810==turn) 
                { if(Pan1909==turn) 
                { win++; } } } } }
                if(Pan1514==turn) 
                { if(Pan1613==turn) 
                { if(Pan1712==turn) 
                { if(Pan1811==turn) 
                { if(Pan1910==turn) 
                { win++; } } } } }
                if(Pan1515==turn) 
                { if(Pan1614==turn) 
                { if(Pan1713==turn) 
                { if(Pan1812==turn) 
                { if(Pan1911==turn) 
                { win++; } } } } }
                if(Pan1516==turn) 
                { if(Pan1615==turn) 
                { if(Pan1714==turn) 
                { if(Pan1813==turn) 
                { if(Pan1912==turn) 
                { win++; } } } } }
                if(Pan1517==turn) 
                { if(Pan1616==turn) 
                { if(Pan1715==turn) 
                { if(Pan1814==turn) 
                { if(Pan1913==turn) 
                { win++; } } } } }
                if(Pan1518==turn) 
                { if(Pan1617==turn) 
                { if(Pan1716==turn) 
                { if(Pan1815==turn) 
                { if(Pan1914==turn) 
                { win++; } } } } }
                if(Pan1519==turn) 
                { if(Pan1618==turn) 
                { if(Pan1717==turn) 
                { if(Pan1816==turn) 
                { if(Pan1915==turn) 
                { win++; } } } } }

                /* 턴을 바꾼다 */
                if(turn==1)        
                    turn=2;
                else if(turn==2)
                    turn=1;
            }

        }
    }
    return 0; // 종료다! 우하하
}
```

**끄읕**
