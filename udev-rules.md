```bash
#MODE는 udev 접근권한으로 0666은 모든 사용자가 접근 가능하다.
#SYMLINK는 시리얼에 접근하는 파일(링크)명이며 += 한 이유는 기존 /dev/loop* 이 있고 추가로 고정할 위치를 정하는 것이기 때문이다.
#==는 조건이 맞는지 확인하는 것

# 라이다
KERNEL=="loop*", SUBSYSTEM=="block", ATTR{loop/backing_file}=="*lidar.img", SYMLINK+="robot_lidar", MODE="0666"

# IMU
KERNEL=="loop*", SUBSYSTEM=="block", ATTR{loop/backing_file}=="*imu.img", SYMLINK+="robot_imu", MODE="0666"

```

| 키워드 | 구분 | 의미 | 예시 |
| :--- | :--- | :--- | :--- |
| **`SUBSYSTEM`** | 매칭 조건 | 장치가 속한 커널 하위 시스템을 지정 | `SUBSYSTEM=="usb"` |
| **`KERNEL`** | 매칭 조건 | 커널이 장치에 부여한 기본 이름을 지정 | `KERNEL=="ttyUSB*"` |
| **`ATTR{...}`** | 매칭 조건 | sysfs에 등록된 장치의 고유 속성을 지정 | `ATTR{idVendor}=="0403"` |
| **`SYMLINK+=`** | 할당 작업 | 기본 장치 파일 외에 추가로 생성할 심볼릭 링크 이름을 지정 | `SYMLINK+="my_device"` |
| **`MODE`** | 할당 작업 | 생성될 장치 파일의 권한(Permission)을 설정 | `MODE="0666"` |
| **`GROUP`** | 할당 작업 | 생성될 장치 파일의 소유 그룹을 지정 | `GROUP="dialout"` |

| 연산자 | 구분 | 의미 및 작동 방식 | 사용 예시 |
| :---: | :---: | :--- | :--- |
| **`==`** | **매칭 (비교)** | 왼쪽 항목의 값이 오른쪽 값과 **일치하는지 검사**합니다. | `SUBSYSTEM=="tty"` |
| **`=`** | **할당 (대입)** | 해당 항목의 값을 오른쪽 값으로 **새롭게 설정하거나 덮어씁니다.** | `MODE="0660"` |
| **`+=`** | **추가 (누적)** | 기존에 설정된 값들 뒤에 오른쪽 값을 **목록으로 추가**합니다. | `SYMLINK+="my_usb"` |

