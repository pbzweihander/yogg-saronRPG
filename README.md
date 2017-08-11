## 요그사론 RPG

### 기본 설정

- 게임의 형태 : 카드 전략 RPG를 빙자한 TCG
- 개발 툴 : Unity 2D

### 게임의 진행

1. 전투 방식
- 턴제로 진행(자신 -> 상대)
- 캐릭터
    - 캐릭터는 체력 바가 존재한다. 체력이 0이 된다면, 전투에서 패배한다.(스테이터스에 대해서는 추후 설명한다.)
	- 자신은 덱에서 카드를 3장 뽑아 그 중 하나의 카드를 발동한다.(마법) (카드의 종류와 덱에 대해서는 추후 설명한다.) 카드를 소모할 때마다, 카드의 특성에 따라 요그사론이 발동할 마법의 종류/확률이 변동한다.(발동 카드 풀에 카드들이 추가되는 것으로 구현한다.)
	- 사용된 카드들은 버려진다.
- 요그사론
    - 자신의 턴의 엔드페이즈 시에 요그사론이 마법을 발동할 수 있고(선택), 그 횟수는 그 이전까지 소모한 카드의 개수가 된다. 단, 요그사론이 발동할 수 있는 최대의 횟수가 정해져 있으며, 그 이상으로 카드를 소모해도 발동 횟수가 증가하지는 않는다.
    - 요그사론이 마법을 발동할 경우, 요그사론의 공격 횟수 및 발동 카드 풀이 초기화된다.
    - 요그사론의 마법의 대상은 랜덤하게 지정된다.(아군, 적군) 단, 카드의 효과에 '아군에게', '적군에게'가 포함된 경우, 대상이 제한된다.
- 적
	- 적들은 혼자(혹은 여럿)으로 구성된다. 각각의 적들은 체력이 존재한다.
	- 상대는 공격/(부가능력)을 사용한다.
- 덱을 모두 소모하게 될 경우, 버려진 카드들을 섞어 새로운 덱으로 활용한다. 이 경우, 적의 체력/공격력이 강해진다.

2. 스테이터스
- 캐릭터
	- 캐릭터는 체력, 방어력, 회피율, 경험치를 가지고 있다.
	- 방어력의 계산 : (적혀진 대미지) - (방어력) = (실 대미지)
	- 회피율의 계산 : (x/100)의 확률로 대미지 0, (1-x/100)의 확률로 (실 대미지)
	- 레벨이 상승할 때마다 체력, 방어력, 회피율이 증가한다.
- 적
	- 적은 체력, 방어력, 회피율, 공격력을 가지고 있다.

3. 카드
- 카드는 '효과'와 '기도'의 두 개의 파트로 구성되어있다.
- 효과
	- 즉발 효과는 카드를 낼 때 바로 발동된다.
	- 카드 효과의 예시는 아래와 같다.
		- 버프 : ~턴 동안 (회피율/방어력)이 ~만큼 증가합니다.
		- 회복 : 체력을 ~만큼 회복합니다.
		- 디버프 : ~턴 동안 적 ~기에게 (혼란/마비/둔화/빙결/약화)을 부여합니다.
			- 혼란 : 공격의 대상이 무작위로 설정됨.
			- 마비 : 공격을 할 수 없음.
			- 둔화 : 회피를 할 수 없음.(회피율이 0으로 설정됨)
			- 빙결 : 공격 및 회피를 할 수 없음.
			- 약화 : 적의 공격력이 낮아짐.
- 카드의 습득 : 카드는 전투의 결과, 혹은 상자 방(추후 설명)에서 얻을 수 있다. 얻은 카드는 다음 모험부터 덱을 편성하여 사용할 수 있다. 만일 같은 카드를 습득할 경우에는 대신 경험치를 얻는다.

- 기도
	- 요그사론의 발동 카드 풀에 특정 카드(들)을 추가한다.
	- 요그사론이 카드를 발동할 때, 기도 효과의 예시는 아래와 같다.
		- 공격 : 대미지를 ~만큼 줍니다.(명시X/적 ~기에게/전체)
		- 회복 : 체력을 ~만큼 회복시킵니다.(명시X/플레이어의/전체)
		- 디버프

4. 덱
- 덱은 총 15장으로 구성 되어 있다. 같은 카드가 3장씩 존재하여 총 5가지의 서로 다른 카드들로 구성된다.
- 덱의 편성은 서로 다른 5개의 카드를 선택하는 것으로 결정된다.

5. 레벨 디자인(모험)
- 맵은 초기 방, 종료 방과 그 사이를 연결짓는 하나의 방들의 길로 구성된다.
- 유저는 한 번에 한 칸씩 이동이 가능하다.
- 각 방은 3가지로 구성된다.
	- 빈 방 : 아무 특징이 없음.
	- 적 방 : 적이 있음. 전투가 진행됨.
	- 상자 방 : 상자 방에서의 이벤트는 아래와 같다.
		- 카드 습득
		- 적
		- 버프/디버프
		- 경험치
