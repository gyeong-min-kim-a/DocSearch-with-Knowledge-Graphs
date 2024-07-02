# DocSearch-with-Knowledge-Graphs
제주삼다수개발공사 문서를 활용한 지식그래프 적용 프로젝트

1. 개요
- 기간 : 2024.03~2024.06(4개월)
- 목표 
	- 문서 검색 시스템에 지식 그래프를 통합하여 단위업무명을 정확하게 매칭하고 추천, 이를 통해 문서와 관련된 정보를 효율적으로 검색하고 활용할 수 있도록 함.
- 역할
	- 단위업무명 매칭
2. 데이터세트
	- 기록물![Pasted image 20240507130751](https://github.com/gyeong-min-kim-a/DocSearch-with-Knowledge-Graphs/assets/174190109/4222b94a-3570-4beb-929b-ce1495e0012a)

	- 기록관리기준표![Pasted image 20240507130822](https://github.com/gyeong-min-kim-a/DocSearch-with-Knowledge-Graphs/assets/174190109/086290b3-b77e-4d2c-944e-a9bef4b56e53)

3. 버전1-유사도를 통한 매칭
	- 기록물 제목 -> 문장임베딩
	- 기록관리기준표['단위과제설명'] -> 문장임베딩
	- 기록물과 기록관리기준표의 단어임베딩 사이에서 유사도 계산(코사인 유사도 계산)
	- 가장 유사도가 높은 행번호를 저장하여 기록물 데이터프레임에 '재매칭_단위업무명'에 생성
	- 결과 : 맞춘 개수가 4278(113677)개로, 4%의 정답률을 가지고 있음.
	
4. 버전2-부서명에 따른 단위업무명 매칭
	- 부서별로 사용하는 단위업무명이 정해져있어, 해당 범위안에서만 선택되도록  버전1을 수정
	- 결과 : 맞춘 개수가 13272(113677)개로, 11%의 정답률을 가지고 있음. 

5. 버전3-Bert의 fine-tuning을 통한 매칭
	- 사전학습된 BERT 모델을 기반으로 데이터세트를 추가 학습 (fine-tuning) 
	- 정규표현식과 띄어쓰기 교정을 통해 데이터 정제 후, 문장 임베딩 생성 
	- 생성된 임베딩을 통해 유사도 계산 및 단위업무명 매칭 
	- 결과: 맞춘 개수가 16775(22736), 74%의 정답률을 가지고 있음