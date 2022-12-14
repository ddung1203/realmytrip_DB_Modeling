# BCNF 3NF 증명

모든 테이블을 한 테이블로 합쳐서 분해를 통해 BCNF 혹은 3NF에 만족함을 보이겠으며, 함수 종속을 보이겠다.

TABLE = (이메일, 고객_이름, 연락처, 여권번호, 날짜, 인원, 총금액, 점수, 내용(후기), 여행지, 여 행_타입, 상품_이름, 가격, 내용(여행), 스페셜, 등록일, 여행지, 국가, 키워드1..5, 여행_경로1..5)

FD:

- FD1: 이메일 → 고객_이름, 연락처, 여권번호, 여행_아이디
- FD2: 여행_아이디 → 키워드(1..5), 여행_경로(1..5), 여행지, 국가, 여행_타입, 상품_이름, 가 격, 내용(여행), 스페셜, 등록일
- FD3: 여행_아이디, 이메일 → 점수, 내용(후기), 날짜, 인원, 총금액
- FD4: 여행지 → 국가

KEY:

- {여행_아이디, 이메일}

NON TRIVIAL한 모든 함수종속에서 결정자가 KEY인 경우 BCNF를 만족한다. 하지만 총 4개의 KEY

에 함수종속을 가지고 있으며, 분해를 진행하겠다.

TABLE = (이메일, 고객_이름, 연락처, 여권번호, 여행_아이디, 키워드1..5, 여행_경로1..5, 여행_타입, 상품_이름, 가격, 내용(여행), 스페셜, 등록일, 점수, 내용(후기), 날짜, 인원, 총금액, 여행 지, 국가)

**우선, FD1을 분해하면**

R1 = (이메일, 고객_이름, 연락처, 여권번호, 여행_아이디)

R2 = (이메일, 여행_아이디, 키워드1..5, 여행_경로1..5, 여행_타입, 상품_이름, 가격, 내용(여행), 스 페셜, 등록일, 점수, 내용(후기), 날짜, 인원, 총금액, 여행지, 국가)

로 분해가 가능하다. 하지만, 이메일 → 여행_아이디(공유), 이메일 → 여행_아이디(위시_리스트) 에서 이메일이 정해지면 여행_아이디의 값에 대한 나머지 부분이 동일한 MVD가 발생한다. 따라서

R3 = (이메일, 고객_이름, 연락처, 여권번호,)…고객

R4 = (이메일 ->> 여행_아이디)…공유

R5 = (이메일 ->> 여행_아이디)…위시리스트

의 RELATION이 만들어진다. R1, R3, R4는 NON TRIVIAL한 모든 함수종속에서 결정자가 KEY인 경우 BCNF에 해당함으로 BCNF와 MVD에 만족한다.

**다음으로 FD2를 분해하겠다**

R6 = (이메일, 여행_아이디, 키워드1..5, 여행_경로1..5, 여행타입, 상품_이름, 가격, 내용(여행), 스페 셜, 등록일, 점수, 내용(후기), 날짜, 인원, 총금액, 여행지, 국가)

에서 FD2에서 여행_아이디 ->> 키워드, 여행_아이디 ->> 여행_경로에서 여행_아이디가 정해지 면 나머지 부분이 동일한 MVD가 발생한다. 따라서

R7 = (여행_아이디 ->> 키워드)…키워드

R8 = (여행_아이디 ->> 여행_경로)…여행경로

로 분해할 수 있고

R9 = (여행_아이디 → 여행지, 국가, 여행_타입, 상품_이름, 가격, 내용(여행), 스페셜, 등록일)

로 분해할 수 있다. 하지만 NON TRIVIAL한 함수종속에서 여행지 → 국가의 **FD4가 존재한다**.

따라서

R10 = (여행_아이디 → 여행지, 여행_타입, 상품_이름, 가격, 내용(여행), 스페셜, 등록일) R11 = (여행지 → 국가)

로 분해할 수 있다. R7, R8, R10, R11 모두 NON TRIVIAL한 함수종속에서 결정자가 KEY인 경우에 해당함으로 BCNF에 만족한다.

R12 = (이메일, 여행_아이디, 점수, 내용(후기), 날짜, 인원, 총금액)

FD3의 여행_아이디, 이메일 ->> 점수, 내용(후기), 여행_아이디, 이메일 ->> 날짜, 인원, 총금액 에서 여행_아이디, 이메일이 정해지면 나머지 부분이 동일한 MVD가 발생한다. 따라서

R13 = (여행_아이디, 이메일, 날짜, 인원, 총금액)…여행_예약

R14 = (여행_아이디, 이메일, 점수, 내용)…후기 로 분해가 가능하다.

이 DATABASE SCHEMA에서 R3, R4, R5, R7, R8, R10, R11, R13 R14의 Relation으로 분해가 가능하며 Non Trivial한 모든 함수종속에서 결정자가 Key인경우에 해당함으로 모든 Relation에 대해서 BCNF 를 만족한다.

**∴ R3, R4, R5, R7, R8, R10, R11, R13 R14의 Relation으로 구성하였다**