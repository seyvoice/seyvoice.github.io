# Silence Engine Code Map
현재 코드 구성과 역할 파악을 통해 오버엔지니어링을 막기 위한 코드 지도. 

## Namespace : SE.Characters
캐릭터 관련 로직

| CS               | TypeName | Type | Host/Updater   | Description |
|:-----------------|:---|:---|:---------------|:---|
| Character.cs     | Character|class| 상속 전용          |캐릭터 정보 처리. 스펙, 스탯, 전투상태|
| ChrName.cs       |ChrName|enum|                |캐릭터 이름|
| CombatState.cs   |CombatState|class| Character      |캐릭터 전투상태 정보. 턴큐, 현재 턴 등| 
| Enemy.cs         |Enemy|Character| GameManager    |적 정보 처리|
| Player.cs        |Player|Character| GameManager    |플레이어 정보 처리|
| PlayerProfile.cs |PlayerProfile|class| PlayerSpecs    |플레이어의 커스터마이징 정보| 
|                  |ChrGender	|enum|                |성별|
|                  |ChrHeight	|enum|                | 키              |
|                  |ChrShape	|enum|	| 체형             |
|                  |ChrSkin	|enum|	| 피부색            |
|                  |ChrHairStyle|enum|	| 헤어스타일          |
|                  |ChrHairColor|enum|	| 헤어색            |
|                  |ChrVoice|enum|	| 목소리            |
|                  |ChrPastime|enum|	| 여유시간에 하는 활동    |
|                  |ChrEarlyMemory|enum|	| 어린시절 기억에 남은 경험 |
|                  |ChrUpbringEvent|enum|	| 성장기 영향을 준 체험   |
|                  |ChrParagon|enum|	| 닮고 싶은 인물       |
|                  |ChrFave|enum|	| 최애 소지품         |
| Specs.cs         |Specs|class| 상속 전용          |캐릭터 스펙 정보. 최대체력, 주사위보너스 등|               
|                  |PlayerSpecs|Specs| Player         |플레이어 스펙 정보|
|                  |EnemySpecs|Specs| Enemy          |적 스펙 정보|
| Stats.cs         |Stats|class| 상속 전용          |캐릭터 스탯 정보. 현재체력, 생존여부 등|                
|                  |PlayerStats|Stats| Player         |플레이어 스탯 정보|
|                  | EnemyStats|Stats| Enemy          |적 스탯 정보|                                   
## Namespace : SE.Core
핵심 진행 로직

| CS               | TypeName | Type | Host/Updater   | Description |
|:-----------------|:---|:---|:---------------|:---|
|DiceManager.cs	|DiceManager|MonoBehaviour| |주사위 굴림 처리. 우선권 굴림, 명중 굴림 등|
|GameConst.cs	|GameConst|class| |개발편의를 위한 상수 제공. UI_btnContinue, CsvSplitter 등|
|GameManager.cs	|GameManager|MonoBehaviour|UNITY|게임의 진행 처리. 싱글톤. 하위 컨트롤러들을 랩핑해서 기능 제공|

## Namespace : SE.Core.Combat
전투 진행 로직

| CS               | TypeName | Type | Host/Updater   | Description |
|:-----------------|:---|:---|:---------------|:---|
|ActionName.cs	|ActionNam|enum| |액션 목록. 공격, 막기, 내려찍기 등|
|CombatController.cs|CombatController|class|GameManager|전투 규칙을 적용해 전투 진행 처리|
| |CombatInputState|enum| |전투 입력 상태. 대기중, 액션 선택 입력, 타겟 선택 입력 등|
| |HitReaction	|enum| |피격 반응. 방어성공, 명중, 빗나감 등|
|CombatGrade.cs	|CombatGrade|enum| |전투의 난이도 등급. 약함, 강함 등|
|Turn.cs	|Turn|enum| |액션의 세부 턴 목록. 막기1턴, 막기2턴, 모으기1턴 등|
|WeaponName.cs|WeaponName|enum| |무기 목록. 검, 망치, 철퇴 등|
|WeaponType.cs|WeaponType|enum| |무기 타입. 한손검, 둔기 등|

## Namespace : SE.Core.Narrative
네러티브 진행 로직

| CS               | TypeName | Type | Host/Updater   | Description |
|:-----------------|:---|:---|:---------------|:---|
|NarrativeController.cs|NarrativeController|class|GameManager|스토리 진행 UI 처리. 실질적으로 Presenter 역할만 수행|

## Namespace : SE.Core.Narrative.BeatModules
네러티브 진행을 위한 Beat:연출단위 모듈

| CS               | TypeName | Type | Host/Updater   | Description |
|:-----------------|:---|:---|:---------------|:---|
|Ask.cs|Ask|Beat|GameManager|선택지 모듈. 선택과 선택지를 표시, GameManager가 결과 보관|
|Beat.cs	|Beat|class|GameManager|스토리 진행 모듈의 베이스. GameManager가 처리하는 각 연출 단위|
|Combat.cs	|Combat|Beat|GameManager|전투 모듈. GameManager에 전투 시작 요청 및 전투 데이터 전달|
| |CombatData|class|Combat|전투 데이터. 적 목록, 난이도, 승리패배 분기 등|
| |MountedCombat|enum| |기마전 타입. 모두 지상전, 한쪽만 기마상태 등|
|IfChoice.cs| IfChoice|Beat|GameManager|선택 분기 모듈. 이전 선택 결과에 따라 GameManager에 Beat 분기 요청|
|PlayBgm.cs	| PlayBgm|Beat|GameManager|배경음악 모듈. 전투 후 이전 음악 복귀도 SoundManager에서 알아서|
|Talk.cs| Talk|Beat|GameManager|글쓰기 모듈. 지문, 대화를 표시. 페이지 처리 및 다른 Beat로 goto 등 기능 포함|

## Namespace : SE.Data					
데이터 저장 및 관리

| CS               | TypeName | Type                               | Host/Updater             | Description |
|:-----------------|:---|:-----------------------------------|:-------------------------|:---|
|ActionAsset.cs	|ActionAsset| SerializedScript-<br/>ableObject | Database|액션 데이터 목록을 저장관리|
|ActionData.cs	|ActionData	class| ActionAsset                        | 전투에서 사용할 수 있는 액션의 정보     |
|CharacterAsset.cs|CharacterAsset| SerializedScript-<br/>ableObject | Database|플레이어 초기값, 적 데이터를 저장관리|
|CombatSettings.cs|CombatSettings| class                              | SettingsAsset|전투관련 세팅 정보|
|ComboData.cs	|ComboData	| class                              | EnemyData|콤보 데이터. 콤보는 여러 액션으로 구성되고, 액션은 여러 턴으로 구성됨|
|Database.cs	|Database	| MonoBehaviour                      | |데이터어셋들을 싱글톤처럼 억세스 제공     |
|DevSettings.cs	|DevSettings| class	                             | SettingsAsset|개발관련 세팅. SpriteAlphaTestThreshold 등|
|EnemyData.cs	|EnemyData| class	                             | CharacterAsset|적 데이터. 이름, 무기, 사용가능 콤보, 최대체력 등|
|GradeBonusData.cs	|GradeBonusData	| class                              | CombatSettings|난이도에 따른 세팅 정보|
|LocalizeAsset.cs	|LocalizeAsset	| SerializedScript-<br/>ableObject | Database|	번역 데이터를 저장관리|
|LocalizeData.cs	|LocalizeData	| class                              | LocalizeAsset|번역 데이터. 번역키와 언어별 텍스트 정보|
|PlayerData.cs	|PlayerData	| class	                             |CharacterAsset| 플레이어 초기값 데이터. 무기, 최대체력 등 |
|SequenceAsset.cs	|SequenceAsset	| SerializedScript-<br/>ableObject | Database|스토리 시퀀스 데이터를 저장관리|
|SettingsAsset.cs	|SettingssAsset	| SerializedScript-<br/>ableObject | Database|게임세팅 데이터를 저장관리|
|WeaponAsset.cs	|WeaponAsset| SerializedScri-<br/>ptableObject   | Database|무기 데이터를 저장관리|
|WeaponData.cs	|WeaponData	| class	                             | WeaponAsset|무기 데이터. 이름, 타입, 공격배율, 우선권 보너스 등|
|WeaponTypeData.cs	|WeaponTypeData	| class                              | WeaponAsset|무기 타입 데이터. 단검, 검, 도끼, 둔기, 양손검 등|

## Namespace : SE.UI
UI 출력 로직 

| CS               | TypeName | Type | Host/Updater    | Description |
|:-----------------|:---|:---|:----------------|:---|
CharacterSheetUI.cs	|CharacterSheetUI|MonoBehaviour| UIManager       |플레이어 정보 UI. 화면우측에 항상 표시. 이름, 칭호, 능력치, 상태, 날짜 등|
|ClickButton.cs	|ClickButton|MonoBehaviour<br/>IPointerClick<br/>Handler| GameManager     |UI 클릭 처리. 입력종류, 버튼인덱스 등을 Gamanager에 전달|
| |ClickButtonType	| enum                                 |                 |	버튼 입력 종류|
|CombatPresenter.cs	|CombatPresenter| class	                               | UIManager       |전투의 UI, VFX, SFX 등 연출 처리|
|CursorControler.cs	|CursorController| class	                               | UIManager       |커서 처리. 커서 변경, 링크 감지, 툴팁 표시 등 알아서|
| |CursorStyle	| enum	                                |                 | 커서 모양|
|ICombatUI.cs	|ICombatUI| interface                            |                 | |
|PlayerCombatUI.cs	|PlayerCombatUI| MonoBehaviour<br/>ICombatUI          | CombatPresenter |플레이어 UI. CharacterSheetUI를 랩핑해서 업데이트 및 전투연출 적용|
|EnemyCombatUI.cs	|EnemyCombatUI| MonoBehaviour<br/>ICombatUI          | UIManager       |적 UI. 이미지, 이름, HP 등|
|Language.cs	|Language| enum                                 |                 |언어 목록. 영문, 한글 등|
|UIManager.cs	|UIManager| MonoBehaviour                        | UNITY           |UI 및 그래픽 처리. 싱글톤. 하위 컨트롤러들을 랩핑해서 기능 제공|

## Namespace : SE.VFX			
시각연출 출력 로직

| CS                    | TypeName | Type | Host/Updater       | Description |
|:----------------------|:---|:---|:-------------------|:---|
| ParticleController.cs |ParticleController|class| VfxManager         |파티클 재생 처리. 풀링 등 알아서|
|                       |VfxParticlePair|class| ParticleController |VFX별 프리펩 어셋정보|         
| SplatController.cs    |SplatController|class| VfxManager         |텍스트연출 재생 처리. 풀링 및 애니메이션 등 알아서 |
|                       |SplatMotionPair|class| SplatController    |SplatMotion별 AnimationClip 정보|
| SplatMotion.cs        |SplatMotion|enum|                    |텍스트연출 모션 타입. 상승, 좌우, 쉐이크 등|
| SplatText.cs          |SplatText|MonoBehaviour| SplatController    |텍스트연출. AnimationClip을 재생해 연출처리|
| Vfx.cs                |Vfx|enum|                    |파티클 연출 목록. 베기, 막기성공, 피격 출혈 등|
| VfxManager.cs         |VfxManager|MonoBehaviour|                    |모든 시각효과 처리. 싱글톤. 하위 컨트롤러들을 랩핑해서 기능 제공|

## Namespace : SE.Sound
오디오 출력 로직

| CS               | TypeName | Type          | Host/Updater  | Description |
|:-----------------|:---|:--------------|:--------------|:---|
| Ambience.cs      |Ambience| enum          |               | 앰비언스 목록. 숲, 방안, 동굴, 폭우, 모닥불, 시민들 등            |
| Bgm.cs           |Bgm| enum          |               |배경음악 목록. 편안한 진행음악, 야만적 전투음악, 영웅적 전투음악 등|
| BgmController.cs |BgmController| class         | SoundManager  |배경음악의 재생 처리. 풀링 및 페이드 등 알아서|
|                  | BgmClipPair      |class| BgmController | BGM별 AudioClip 어셋정보            |
| Sfx.cs           |Sfx| enum          |               | 효과음 목록. 흙 발소리, 나무 문 열기, 둔기 공격, 둔기 피격, 피격 출혈 등 |
| SfxController.cs |SfxController| class         | SoundManager  |효과음, 앰비언스의 재생 처리. 풀링 등 알아서|
|                  | SfxClipPair      |class| SfxController | SFX별 AudioClip 어셋정보            |
|                  | AmbienceClipPair |class| SfxController | Ambience별 AudioClip 어셋정보       |
| SoundManager.cs  |SoundManager| MonoBehaviour | UNITY         |모든 음향 처리. 싱글톤. 하위 컨트롤러들을 랩핑해서 기능 제공|
|                  | SoundSettings    |class| SoundManager  | 음향 볼륨 설정. 마스터, 음악, 효과음, 앰비언스 등 |
|                  |Mixer|enum|               |설정할 믹서 목록. 마스터, 음악, 효과음, 앰비언스|

## Namespace : SE.Etc
유틸리티 등 기타

| CS               | TypeName | Type | Host/Updater | Description |
|:-----------------|:---|:---|:-------------|:---|
|ScreenScaleListener.cs|ScreenScaleListener|MonoBehaviour|              |화면 변화 대응 처리. 항상 16:9로 내용이 표시되도록 알아서|
