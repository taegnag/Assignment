# Assignment
## 1. 프로그램 구동을 위한 필수 패키지 및 사용한 오픈 소스 명시
### 필수 패키지

pygame, cx_freeze 패키지를 다운로드 받아야 합니다.

버전 : python 3.10.12, pygame 2.5.2, cx_freeze 6.15.10

### 사용한 오픈소스

https://github.com/psychedelickoala/monopoly-in-pygame 

## 2. Ubuntu 20.04 기준 설치 방법 명시
1. https://github.com/taegnag/Assignment 접속 후 초록색 code 버튼을 눌러 Download Zip을 실행시킵니다.
2. 터미널을 통해 파일이 있는 경로로 이동한 뒤, 터미널에 다음과 같은 명령어를 입력합니다.

        pip install pygame

        pip install cx_freeze

        python setup.py build

3. 이후 폴더 내의 main.py를 visual studio code를 통해 실행시킵니다.

## 3. 최종 발표 슬라이드 내용과 구체적인 설명 추가
### [프로젝트 주요 특징]
수정하거나 새로 작성한 코드로 인해 기존의 코드와 진행 방식이 어떻게 달라졌는지 위주로 봐주시면 감사하겠습니다.

### [class 다이어그램]
#### 플레이어 관련 class -Player, AI, Bank
Player : 게임 참여자의 게임 내 정보를 저장하는 클래스

AI: 게임 내 AI의 게임 내 정보를 저장하는 클래스

Bank: 게임 내 빈 부동산을 소유하고 있는 클래스


#### 칸 관련 class - Square, Property(Square), Chance(Square), TaxSquares(Square), SpecialSquare(Square)
Square : 각 칸에 관련된 클래스들이 상속 받는 클래스

Property(Square) : 부동산과 관련된 클래스

Chance(Square) : 게임 내 이벤트 발생 칸과 관련된 클래스

TaxSquares(Square) : 게임 내 복지기금 납부와 지급과 관련된 클래스

SpecialSquare(Square) : 게임 내 복지기금, 감옥, 해외여행 등 특별한 기능 관련된 클래스


#### 게임 실행 관련 기타 클래스 - Roll, Botton, Palette, Card, Ratio
Roll : 주사위 정보를 담고 있는 클래스

Botton : 게임 내 우측 6개의 진행과 관련된 클래스

Palette : 게임 내 사용된 색과 관련된 클래스

Card : 게임 내 사용되는 이벤트 카드와 관련된 클래스

Ratio : 게임 내 AI가 소유한 재산에 대해 진행한 가치 판단에 대한 클래스

### [기존 코드에서 수정한 점]
#### 코드 내 수정한 부분들은 # modiification start/end here, 저희가 만든 부분들은 # start/end here로 표시해두었습니다.
#### 1. 우측상단 모서리 칸 도착하면 감옥칸으로 이송
-> 우측상단 모서리 칸을 우주여행 칸으로 바꾸어 임의의 위치로 플레이어와 AI의 위치를 변경.

#### 2. 현재 본인이 있는 칸과는 상관없이 색이 같은 부동산을 모두 소유하고 있으면 건물 건설 가능. 단, 같은 색의 부동산 간의 건물 갯수가 2개 이상 차이 날 수 없었음.
-> 현재 본인이 서있는 칸의 부동산을 본인이 소유하고 있을 시, 건물 건설 가능. 단, 건물의 수는 플레이어가 시작점에 도달한 횟수로 통제.

(예를 들어, 시작점에 0번 도착했으면 각 부동산에 건물 1채, 1번 도착하면 2채, ... , 최대 4채까지 건물 건설 가능. 이후론 건설 불가.)


#### 3. 판의 크기 40칸(10*10)
-> 부루마불에 존재하지 않는 소득세 및 공공기관 칸 등 삭제.
-> 줄어든 크기인 (9*9)에 맞추어 보드 전체적인 설정 변경.

#### 4. 은행소유(빈 땅)에 도착할 때, 땅을 구매하지 않으면 Auction과 Trade 기능 사용 가능
-> 기존 부루마불에는 부동산에 대한 경매 기능과 부동산 간 거래 기능이 존재하지 않으므로 두 기능 삭제.

#### 5. 감옥에 갇히면 더블이 나오거나 주사위를 3번 굴릴 때 까지 빠져나오지 못한다. 조건을 충족하면 감옥 무료카드를 사용하거나 50달러를 내야 나올 수 있었음..
-> 기존 부루마불에서는 감옥에 갇혔을 때, 황금카드에서 나온 감옥 탈출 카드로 빠져나올 수 있으므로 그 방식으로 변경.
-> 또한, 감옥 탈출 카드를 소유한 상태로 감옥에 갇혔을 때, 바로 카드를 사용하지 않으면 카드가 삭제되도록 한 번 더 변경.

#### 6. 통행세를 낼 돈이 없으면 부동산을 담보로 50%를 은행에 돈을 빌려온다. 땅의 소유주는 바뀌지 않지만 통행세를 걷을 수 없다.
-> 기존 부루마불에서는 자금이 없는 상황에서 부동산에 대한 담보 대출이 아닌 매각 기능을 사용하기 때문에 대출 기능을 매각 기능으로 변경.
