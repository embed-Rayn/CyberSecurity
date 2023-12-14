# iAID PACS 프로그램 정보 숙지

## 프로그램 개발 정보

-   언어: Java, JDK 11
-   WAS: Wildfly
-   DBMS: PostgresQL
-   계정 및 설정 정보 저장 DB: OpenLDAP
-   계정 인증: Keycloak(3rdaprty 인증 소프트웨어)

## DEMO 페이지

-   주소: http://demo.pacs.iaidimage.com/

## 프로그램 주요 통신 API

### 인증

-   Base 통신스택: HTTP
-   회원가입
-   회원정보 조회
-   로그인

--상세 프로토콜 명세 작성예정--

### 보고서 및 템플릿 조회/작성

-   DICOM 데이터에 대해서 의료진이 보고서 내용/보고서 템플릿을 작성/조회하기 위한 RESTful 기반 프로토콜
-   Base 통신스택: HTTP

--상세 프로토콜 명세 작성예정--

### DICOM 정보 조회/업로드

#### DICOM Web

-   RESTful API형태를 이용해 웹기반으로 의료 영상 및 관련 데이터를 다른 의료 시스템과 기기 간에 교환하고 공유하는 데 사용
-   통신스택: HTTP
-   기능: DICOM Web은 다음과 같은 주요 기능을 제공
    | [Query](https://www.dicomstandard.org/using/dicomweb/query-qido-rs) | Search for DICOM objects (QIDO-RS) | [DICOM PS3.18 10.6](http://dicom.nema.org/medical/dicom/current/output/chtml/part18/sect_10.6.html) |
    | -------------------------------------------------------------------------------------- | ------------------------------------------ | --------------------------------------------------------------------------------------------------- |
    | [Retrieve](https://www.dicomstandard.org/using/dicomweb/retrieve-wado-rs-and-wado-uri) | Retrieve DICOM objects (WADO-RS) | [DICOM PS3.18 10.4](http://dicom.nema.org/medical/dicom/current/output/chtml/part18/sect_10.4.html) |
    | | Retrieve single DICOM instances (WADO-URI) | [DICOM PS3.18 9](http://dicom.nema.org/medical/dicom/current/output/chtml/part18/chapter_9.html) |
    | [Store](https://www.dicomstandard.org/using/dicomweb/store-stow-rs) | Store DICOM objects (STOW-RS) | [DICOM PS3.18 10.5](http://dicom.nema.org/medical/dicom/current/output/chtml/part18/sect_10.5.html) |

#### DIMSE

-   의료 이미징 시스템 간에 DICOM 프로토콜을 사용하여 통신하는 데 사용되는 메시지 교환 프로토콜
-   Base 통신스택: TCP/IP
-   기능요약:
    -   Storage(C-Store) - 영상들이나 오버레이 같은객체들을 송/수신
    -   Query(C-Find) - 원격 장비에 질읳나느데 사용. 영상과 데이터 목록을 얻기 위해 질의
    -   C-ECHO - 양 단말기의 통신 연결이 가능한지 확인하는데 사용. (IP에서 Ping과 비슷)
    -   Transfer(C-Move) - 제 3자의 장비로 데이터를 전송
    -   Retrieval(N-Get) - 원격 장비로부터 특성 값을 가져오는데 사용
    -   -   실제 DIMSE 프로토콜은 이보다 더 정의된것이 많지만, 저희 PACS 에서 써본건 요정도 인것같습니다.
-   DIMSE 프로토콜 테스트
    -   DCMTK 또는 DCM4CHE 라이브러리에서 제공하는 통신도구를 이용할 수 있습니다.
