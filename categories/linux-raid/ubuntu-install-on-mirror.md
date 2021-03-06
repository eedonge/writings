# 디스크 미러 잡고 우분투 설치하기

### 들어가는 글

Ubuntu 10.04 Server 기준이다.

아래 처럼 남들 하는 대로 하면 편한데 괜히 고생을 하여 결과를 메모한다.

https://help.ubuntu.com/community/Installation/SoftwareRAID

### 디스크 준비

먼저, 디스크에 GPT 메타 데이터가 남아있으면 기동중인 우분투 머신에 USB 외장하드등으로 물려서 청소한다.
`gparted` 에서 `msdos` 파티션을 새로 생성하면 되겠다.

또 mdadm metadata 가 남아 있으면 하드를 장착하고 부팅하는 순간 커널이 읽고 꼬이므로 이것도 청소한다.

	mdadm --zero-superblock <device>

### 실패한 시나리오

디스크 두 대를 통으로 미러링한 후 이것을 파티셔닝해서 설치하는 시나리오들은 실패했다.
부트로더 설치 단계에서 에러가 난다. 

### 성공한 시나리오

우분투 설치 디스크로 간편하게 부팅 파티션 미러들 만들려면
번잡하지만 디스크의 미러가 아니라 각 파티션의 미러를 만들어야 한다.

우분투 인스톨러의 파티션 메니저에서 두 디스크의 파티션을 동일하게 나눈 후
같은 화면에 있는 소프트웨어 레이드 설정 메뉴를 통하면 진행에 무리가 없다.
단지 `mdadm` 의 `--assume-clean` 인자를 주지 못해서 미러를 무조간 싱크하므로 설치가 되게 느려진다.

오늘은 해보지 않았지만 (전에 해봤는데 까먹었을 수도 있지만)
`--assume-clean` 옵션을 주어 수작업으로 레이드를 묶은 후 설치를 한다면 시간을 많이 단축할 것이다.

	mdadm --create /dev/md0 --verbose --metadata 1.2 --level=1 --raid-devices=2 --assume-clean /dev/sd[ab]1

### 참고: mdadm 사용 가능 시점

초반에 Additional Components 들이 램디스크에 올라오는 절차가 끝나면
Go Back 으로 전체 설치 과정 메뉴를 부른 후 하단의 쉘로 나가 mdadm 을 사용할 수 있다.
처음부터 쉘로 나가면 mdadm 이 없다. 

### fdisk 로 수작업 파티셔닝할 때 주의점

`fdisk <device>` 명령으로 `fdisk` 진입후 `c` 명령으로 도스 호환 모드를 끈다.
이걸 안 해주면 디스크 성능이 우울해진다. '4 KiB Sector Issue' 글 참고.

기타,
u 명령으로 표시 단위 변경,
o 명령으로 새 도스 파티션 테이블 생성 (시스템, 스웝, 데이타 등),
n 명령으로 파티션 추가,
p 명령으로 확인,
w 로 저장.

### 파티션 테이블 복사

우분투 인스톨러에서 두 대의 파티션들을 하나하나 만들어도 되지만
미러하려는 기존 디스크가 있는 경우 아래 명령으로 새 디스크에 동일한 파티션 테이블을 복사할 수 있다.

	sfdisk -d <source device> | sfdisk <target device>

### 마무리

오늘 삽질의 주요 원인은 디스크를 통으로 미러링하려고 했기 때문.
우분투 인스톨러 시나리오와 문제를 일으킨다.
통으로 잡으려들지만 않으면 속도 향상을 위해 적절한 수작업은 해볼만 할 것 같다.
