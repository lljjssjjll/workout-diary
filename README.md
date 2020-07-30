# Workout Diary
## 구성
* 프레임워크: Spring Boot
* ORM: JPA, Hibernate
* DB: H2 (초기), MySQL (개발)
* 인증: KeyCloak
## 기능
### 사용자 관련
* 사용자 가입
    * 일반
* 사용자 로그인/로그아웃
    * 일반
    * 구글 (추후)
* 사용자 비밀번호 변경
    * 일반 (추후)
* 사용자 락
    * 일반
        * 비밀번호 5회 불일치의 경우 5분 잠금
### WT 관련
* 달력에 일별 WT 기록 전체 보여주기 (일별 총세트,부위별 총세트,부위별 완료 여부 등)
* 달력에서 특정일자를 클릭하면 기록한 종목 리스트 보여주기 (이름,총세트,완료 여부 등)
* 기록한 종목을 클릭하면 수행한 종목 상세 보여주기 (세트,무게,횟수,완료 여부 등)
* 일별 종목 생성하기
    * 년월일 선택 -> 부위 선택 혹은 전체 -> 종목 추가 -> 저장 (서버 통신)
        * 일별 종목 상세 추가하기 (세트) -> 세트별 무게,횟수,완료 여부 등 변경
        * 일별 종목 상세 삭제하기 (세트)
* 일별 종목 삭제하기
* 특정날짜의 WT 기록 복사 (추후)
### 관리자 관련
* 종목 생성
## DB 모델링
* 사용자
    * 사용자 아이디 (PK)
    * 이메일 (UK,NN,최대30자)
    * 비밀번호 (NN,최대200자)
    * 역할 (NN,NORMAL/ADMIN)
    * 닉네임 (UK,NN,최대50자)
    * 생년월일
    * 성별 (MALE/FEMALE)
    * 무게 단위 (NN,KG/LB)
* 일별_종목
    * 일별_종목 아이디 (PK)
    * 사용자 아이디 (FK,MUL)
    * 종목 아이디 (FK,MUL)
    * 년월일 (MUL)
* 일별_종목_상세
    * 일별_종목_상세_아이디 (PK)
    * 일별_종목_아이디 (FK)
    * 세트
    * 무게 KG
    * 무게 LB
    * 횟수
    * 시간
    * 휴식 시간
    * 완료 여부 (NN)
* 종목
    * 종목 아이디 (PK)
    * 이름 (MUL,NN,최대30자)
    * 부위 (MUL,NN,가슴/등/하체/엉덩이/이두 등)
    * 기구 (MUL,NN,덤벨/바벨/머신/맨몸 등)
    * 무게 사용 여부 (NN)
    * 시간 사용 여부 (NN)
    * 횟수 사용 여부 (NN)