---
title: "Nordic Serial Interactive PyACI scripts"
last_modified_at: 2022-04-13T11:15:00-09:00
categories:
- Nordic
- MESH
tags:
- nordic
- ble
- mesh
- serial
excerpt: "Nordic Serial 예제 PyACI 명령어"
---

## 실행

```bash
python interactive_pyaci.py -d <COM1 or /dev/ttyACM0> [--no-logfile | -l <num>]
```

- l <num>
    - 1: error
    - 2: warning
    - 3: info
    - 4: debug

## Command 정리

### Example

```python
db = MeshDB("database/example_database.json")       # DB 연결

p = Provisioner(device, db)                         # Provisioner 설정
# Net key handler 반환 (subnet_handle)
# App key handler 반환 (appkey_handle)

p.scan_start()                                      # Device scan
# Unprovisioned Device 출력
p.scan_stop()                                       # Device scan stop

p.provision(uuid="<UUID>", name="<Set the name>")   # Provisioning
# Dev key handler 반환 (devkey_handle)
# Unicast address handler 반환 (address_handle)

cc = ConfigurationClient(db)                        # CC 모델
device.model_add(cc)                                # serial device에 model CC 모델 추가
cc.publish_set(8, 0)                                # devkey_handle/address_handle이 일치하는 장치와 연결
cc.composition_data_get()                           # 구성 데이터 요청
# composition data 출력
# features: 0-on 2-off
# elements/models: 장치가 제공하는 model id 정보
```



### Heartbeat

ConfigurationClient model 설정을 해야한다.

#### Heartbeat Publication

```python
heartbeat_publication_get()                         # heartbeat publication 정보
heartbeat_publication_set(self, dst, count, period, # heartbeat publication 설정
                            ttl=64, feature_bitfield=0, netkey_index=0)
```

- dst: Unicast or group ID, 0xFFFF: 전체 디바이스
- count: Heartbeat 메시지 전송 개수. 정수값이며, 실제 값은 log 단위로 조정된다.
  $count = integer(\log_2{count_{set}})$
    - log scale값을 정수로 변환. $count = 2^{count_{get}} + 1$
- period: Heartbeat 메시지 전송 간격. 정수값이며, 실제 값은 log 단위로 조정된다.
    - log scale값의 정수로 변환. $period = 2^{period_{get}} + 1$
- feature_bitfield: Feature 변경시 trigger되어 Heartbeat 메시지 전송
    - 1: Relay, 2: Proxy, 4: Friend, 8: Low Power (원하는 feature을 더함)
- netkey_index: Heartbeat를 보내려는 NetKey Index


#### Heartbeat Subscription

```python
heartbeat_subscription_get()                        # heartbeat subscription 정보
heartbeat_subscription_set(self, src, dst, period)  # heartbeat subscription 설정
```

- src: Unicast ID
- dst: Unicast or group ID, 0xFFFF: 전체 디바이스
- period: Heartbeat 메시지 전송 간격. 정수값이며, 실제 값은 log 단위로 조정된다.
    - log scale값의 정수로 변환. $period = 2^{period_{get}} + 1$
- count: log 값. $2^{count_{get}} - 1 < count_{real} < 2^{count_{get}}$
- min/max hop: Heartbeat 메시지가 전달되는 동안 거친 최소/최대 hop 수

