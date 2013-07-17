# Time Capsule

TC 브로셔의 불명확한 사용 시나리오들에 대한 간단 메모입니다. 2011.12.22 일 기준.

TC 는 네트웍 타임머신 장비로 마케팅되고 있는데 기능만 뜯어보면 인터넷 유무선 공유기와 네트웍 디스크 기능이 함께 들어있는 장치입니다. 네트웍 디스크 기능이 있으니 맥의 타임머신 백업용으로 쓸 수 있습니다. 아니면 그냥 평범한 파일 공유 용도로 쓰셔도 됩니다. 즉, 기존에 집에 있던 인터넷 공유기를 빼고 TC 를 넣으면 인터넷 외에 갑자기 2 TB 짜리 파일 서버가 생깁니다.

TC 는 여러 맥의 타임머신 백업 용도로 최적입니다. 두 대의 맥을 USB 외장하드로 백업하려면 외장하드 조합 두 벌이 필요한데 TC 는 네트웍 디스크이므로 한 대만 있으면 됩니다. 필요한 케이블이나 어뎁터가 대폭 줄어듭니다.

회사에선 iMac 을 쓰고 집에는 Air 만 들고다니는 저 같은 경우 집에 TC 를 설치하면 TC 가 미디어 파일 서버 기능을 하게 됩니다. 이불에 누워 미디어 감상을 하기 위해 Air 에 USB 하드를 매달고 다니지 않아도 됩니다.

요켠데 TC 는 NAS 나 USB 외장 하드를 대치하면서 무선이란 자유로움을 줍니다.

전 TC 가 비싸다고 생각하지 않습니다. 인터넷 공유기 사고, NAS 사고, 하드 사면 얼추 TC 가격 나옵니다.
맥이 두 대라면 백업하기 위해 복수 외장하드가 필요하므로 이런 경우도 경제적이라 할 수 있습니다. 
NAS 의 소음이나 추가 어뎁터들을 생각하면 TC 가 꽤 유리합니다. 게다가 TC 는 어뎁터가 없습니다. 그리고 초 저소음이군요.

이제부터 문제점 나갑니다.

TC 의 가장 큰 문제는 여러 사람이 사용하는 시나리오입니다.
계정을 등록하는 기능이 있고 읽기 전용, 쓰기 가능 지정을 할 수 있으나 문제는 전체 디스크 별로만 권한을 줄 수 있습니다.
폴더 별로 퍼미션을 주는 기능이 없습니다.
즉, 어떤 계정은 디스크 전체에 대해 읽기만 가능, 어떤 계정은 디스크 전체에 대해 읽고 쓰기가 가능, 이런 황당한 방식입니다.

회사 내이니 백번 양보해서 모두 읽고 쓰기 가능으로 세팅해 두고 파일 공유 기능을 써볼까했는데
문제는 파일 공유와 타임머신 백업이 같은 공간을 사용합니다. 그러니 아무에게나 읽기 쓰기 권한을 주면 아무나 내 백업을 삭제해 버릴 수 있게 됩니다. 황당합니다.
즉 TC 는 접속 계정에 대해 디스크 별로 RW 퍼미션 관리를 할 뿐 타임머신 기능을 위한 아무런 보호장치도 가지고 있지 않습니다. 

그러니 TC 를 타임머신 백업용으로 쓴다면 개인 용도 파일 공유만 가능합니다. 백업을 포기하고 파일 공유용만으로 쓴다해도 폴더 별로 권한을 줄 수 없으므로 현실적으로 모두가 읽고 쓰는 상황만이 가능합니다.

해법이 있긴한데 TC 내장하드를 꺼내서 맥에서 여러 파티션으로 나누어 재 장착하는 것입니다. 하지만 별로 하고싶지 않습니다. =,=

오늘 미친척하고 TC 를 두 대 질렀는데 회사에서는 iMac + Air 의 백업 외장 하드 세트들을 없앨 수 있을 것 같고 혼자만의 무선 서브넷을 만들 수 있었습니다. 집에선 에어에 매달고 다니던 외장 USB 세트가 사라지겠군요.

단, TC 시나리오는 개념상 3 단 백업이 아니기 때문에 중요 데이터는 가끔 USB 외장에 통 백업을 하려고 합니다. 집에서 사용할 미디어 저장용 TC 는 나라가면 걍 운명으로. =,=