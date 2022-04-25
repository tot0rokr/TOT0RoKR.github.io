---
title: "Nordic Serial Firmware"
last_modified_at: 2022-04-18T10:18:00-09:00
categories:
- Nordic
- MESH
tags:
- nordic
- ble
- mesh
- serial
excerpt: "Nordic Firmware 분석자료"
---

## RAW 정보

### Hearbeat packet 수신과정

heartbeat\_init()에서 heartbeat callback 함수인 heartbeat\_opcode\_handle()을
transport\_control\_packet\_handler\_t(TRANSPORT\_CONTROL\_PACKET\_CONSUMER\_ADD, heartbeat\_opcode\_handle)를
transport\_control\_packet\_consumer\_add()를 통해
m\_control\_packet\_consumers에 등록.

거기서 control\_packet\_callback\_get을 통해서 해당 callback을 리턴받음.

위 함수는 transport\_control\_packet\_in()에서 호출되며, 해당 callback 함수를 실행시킴.
여기서 heartbeat\_opcode\_handle()이 실행 되는 것임.
위 함수는 upper\_transport\_packet\_in()에서 호출되며, control packet일 경우 수행하는 분기인 것으로 확인됨.

여기서 heartbeat subscription에 의해 데이터 가공 및 폐기를 수행.
evt 파라미터 생성 후, event\_handle() 호출

event\_handle()은 주기적인 event handler임.
event list에 등록되어있는 event들을 주기적으로 핸들링.

해당 이벤트는 serial example의 main() -> initialize() -> mesh\_init() -> nrf\_mesh\_serial\_init() -> serial\_handler\_mesh\_init()에서 추가.
해당 이벤트 핸들러는 serial\_handler\_mesh\_evt\_handle().
NRF\_MESH\_EVT\_MESSAGE\_RECEIVED
NRF\_MESH\_EVT\_IV\_UPDATE\_NOTIFICATION
NRF\_MESH\_EVT\_KEY\_REFRESH\_NOTIFICATION
NRF\_MESH\_EVT\_HB\_MESSAGE\_RECEIVED
NRF\_MESH\_EVT\_TX\_COMPLETE
메시지를 핸들링함.
데이터를 가공해서 tx\_serial()로 PC 인터페이스에 전송


```
 64 typedef struct __attribute((packed))
 65 {
 66     uint8_t length; /**< Length of the packet in bytes. */
 67     uint8_t opcode; /**< Opcode of the packet. */
 68
 69     /** Union of the various payload structures for all serial packets. */
 70     union __attribute((packed))
 71     {
 72         serial_cmd_t cmd; /**< Command packet parameters. */
 73         serial_evt_t evt; /**< Event packet parameters. */
 74     } payload;
 75 } serial_packet_t;
```



### Serial App 동작

mesh\_init() -> nrf\_mesh\_serial\_init() -> serial\_handler\_app\_cb\_set() -> m\_app\_rx\_cb에 app handler를 등록함으로써
serial command가 동작해야하는데, app handler가 null로 들어감
이 핸들러는 serial\_handler\_app\_rx()에서 호출되어야 하는데, 정상적인 동작의 경우, m\_app\_rx\_cb() 동작 후 SERIAL\_STATUS\_SUCCESS를 반환
그렇지 않은 경우(handler가 없는 경우), SERIAL\_STATUS\_REJECTED 반환



### Serial Model 동작
end\_reception() -> serial\_process() ->
serial\_process\_cmd() -> serial\_handler\_\<category\>\_rx() -> serial\_handler\_common\_rx() -> model\_command()

```
const serial_cmd_model_specific_command_t * p_cmd_params = &p_cmd->payload.cmd.access.model_cmd;
access_model_id_t model_id;
uint32_t status = access_model_id_get(p_cmd_params->model_cmd_info.model_handle, &model_id);

serial_handler_models_info_t * p_targeted_model = registered_model_get(&model_id);
```

### Serial RX log

```
00> <t:     337238>, serial.c,  129, Serial process cmd: 0x: 07FE00008141512320FA032018282A6C00FA032010FB0320C0B20400B0FA032069600400A67C6F6310FB032098CA0BA49F9F222EFB86171627002CA4559BE2C778D04D0D80C4C831A87C1BE03847D1685C0F39D2B3B2E7D1B843DDBA655619B4FEC0B4FD7E334EB743641EA666176794594B93B6448A86286EE793C267626DFA
00> <t:     337246>, serial_handler_models.c,  161, Serial RX Payload: 0x: 07FE00008141512320FA032018282A6C00FA032010FB0320C0B20400B0FA032069600400A67C6F6310FB032098CA0BA49F9F222EFB86171627002CA4559BE2C778D04D0D80C4C831A87C1BE03847D1685C0F39D2B3B2E7D1B843DDBA655619B4FEC0B4FD7E334EB743641EA666176794594B93B6448A86286EE793C267626DFA

00> <t:     424612>, serial.c,  129, Serial process cmd: 0x: 06FE00000080382320FA032018282A6C00FA032010FB0320C0B20400B0FA032069600400A67C6F6310FB032098CA0BA49F9F222EFB86171627002CA4559BE2C778D04D0D80C4C831A87C1BE03847D1685C0F39D2B3B2E7D1B843DDBA655619B4FEC0B4FD7E334EB743641EA666176794594B93B6448A86286EE793C267626DFA
00> <t:     424620>, serial_handler_models.c,  161, Serial RX Payload: 0x: 06FE00000080382320FA032018282A6C00FA032010FB0320C0B20400B0FA032069600400A67C6F6310FB032098CA0BA49F9F222EFB86171627002CA4559BE2C778D04D0D80C4C831A87C1BE03847D1685C0F39D2B3B2E7D1B843DDBA655619B4FEC0B4FD7E334EB743641EA666176794594B93B6448A86286EE793C267626DFA

00> <t:    1014495>, serial.c,  129, Serial process cmd: 0x: 05FE00008038382320FA032018282A6C00FA032010FB0320C0B20400B0FA032069600400A67C6F6310FB032098CA0BA49F9F222EFB86171627002CA4559BE2C778D04D0D80C4C831A87C1BE03847D1685C0F39D2B3B2E7D1B843DDBA655619B4FEC0B4FD7E334EB743641EA666176794594B93B6448A86286EE793C267626DFA
00> <t:    1014503>, serial_handler_models.c,  161, Serial RX Payload: 0x: 05FE00008038382320FA032018282A6C00FA032010FB0320C0B20400B0FA032069600400A67C6F6310FB032098CA0BA49F9F222EFB86171627002CA4559BE2
```

- 07FE000081415123
- 06FE0000008038
- 05FE00008038
- 구조
	- packet size length: 1 byte
	- model opcode length: 1 byte
	- model handle length: 2 bytes
	- data size: $packet\,size - 3\,bytes$
