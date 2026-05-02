# Silence Engine: Coding Principles

## 📝 코드 설계 원칙
### 1. 가독성 우선
- 읽기 쉬운 코드가 가장 좋은 코드다.
### 2. 개체 중심 설계
- 진행, UI, SFX 등 통합기능을 처리하는 `Manager`, 개별 개체 `Actor` 중심 설계.
- 클래스는 인지 가능한 '개체' 단위 명사로 작명.
- 메소드는 인지 가능한 '기능' 단위 명사로 작명.
- 개발 개념적 추상화는 지양.
### 2. 인지 중심 설계
- 클래스가 커지면 `Manager > Controller`, `Actor > Handler` 로 역할 위임.
- `Manager/Actor`가 `Controller/Handler`를 변수로 가진 호스트가 되어 관리하는 구조.
- `Controller/Handler`는 외부 접근불가. 호스트를 통해 통신. 인지 단위 축소.
### 3. 안전 중심 설계
- `Setup()`: `Awake()` 스텝에 해당. 변수 및 인스턴스 생성. 상호 외부 접근 금지.
- `Init()`: `Start()` 스텝에 해당. 초기값 설정. 외부 접근 가능.
- `Constructor`: 매니저 단위의 생성, `Setup()`, `Init()`, `Update()` 교통정리 필요시 담당.
- 풀링 적극 활용. `Particle`, `AudioSource` 등 메모리 누수 방지.
### 4. 성능 중심 설계
- `MonoBehaviour` 의존 최소화, `Update()` 호출 지양.
- `Manager` 싱글톤을 활용한 `Setup()`, `Init()`, `Update()` 관리.
- `Update()` 상세화. 입력, 화면, 로직, 물리 업데이트를 각각 별도로 관리.
