# NLP_BigCamp_in_SNU
The 7th data sience boot camp BIG CAMP with big data institute of Seoul National University <br/>
From Oct. 22. 2019 to Oct. 25. 2019 in Gaepo Digital Innovation Centre<br/>

# Summaries 
## Day 1

자연어처리 분야에선 그동안 Sequence를 다룰 수 있는 RNN 모듈이 사용되어 왔음 <br/> 
자연어처리의 가장 핵심은 첫 번째 레이어에서 시작되는 임베딩<br/>
임베딩이 잘 되는 것이 매우 중요한 부분이라 할 수 있음<br/>
또한 자연어처리는 긴 역사를 가지고 있음 ex) 구글의 기계번역기 (트랜스포머 이후로 큰 발전을 함)<br/>
제 2차 세계대전 때부터 많은 투자를 받음<br/>
자연어처리의 역사는 곧 기계번역의 역사<br/>
처음에는 문법 기반 -> 통계 기반 -> 인공신경망 기반 -> 트랜스포머 기반<br/>
자연어처리의 활용 분야로는 음성비서(시리), 챗봇(Q&A), 요약기 등이 있음<br/>

컴퓨터는 우리의 말을 이해하지 못하기 때문에 이해할 수 있도록 만들어야 함<br/>
- 컴퓨터가 이해할 수 있는 representation으로 전달함<br/>
인간의 언어가 어떻게 만들어져 있는지 이해하여야 함<br/>
- Speech(음향적 전달) -> 음소 분석 -> 통사 분석 -> 의미 분석 -> 문맥 추론<br/>

많은 경우 각각의 요소의 합은 전체와 다를 수 있음<br/>
ex) 여기 왜 이렇게 더워요? -> 에어컨을 켜달라는 의미를 내포할 수 있음<br/>

### 컴퓨터가 언어를 이해할 수 있는가?
품사분석기, 구문분석기 등은 많이 개발되었지만, 컴퓨터가 이해를 할 수 있는가?<br/>
우리가 원하는 그대로 이해하는 것은 어려움<br/>
하지만 다른 접근으로 진행 중에 있음<br/>
인간의 언어는 중의성이 매우 큼 (ambiguity)<br/>

### 파이프라인 만들기
하나 하나 작은 것을 수행하여 전체를 연결하여 수행<br/>
1. 문장 단위로 나누기 (sentence segmentation)<br/>
 -> 늘 마침표 기준으로 나눠지지 않음 (소수점, 약어)<br/>
2. 단어 단위로 나누기 (word tokenization)<br/>
 -> 늘 띄어쓰기 기준으로 나눠지지 않음 (New York)<br/>
3. 품사 예측 (predicting POS)<br/>
 -> 형태소 분석기를 사용해서 품사를 지정함<br/>
4. Lemmatization (원형 복원)<br/>
 -> 형태는 변했지만, 같은 의미를 같은 단어를 원형으로 복원함<br/>
    한국어는 원형복원 모듈이 없음<br/>
5. 불용어 지정 (identifying stop words)<br/>
6. 문장 구조의 의존도 분석 (dependency parsing)<br/>
 -> 영어엔 Stanford parser, 구글 파서 등이 있음<br/>
    한국어엔 없음<br/>
    영어의 경우 어순이 정해져 있고, 형태소가 매우 복잡함 (먹으셨겠으다만은)<br/>
    하지만 한국어는 어순에 있어 비교적 자유로움<br/>
6-2. 명사구 찾기 (finding noun phrase)<br/>
7. 개체명 인식 (Named Entity Recognition)<br/>
8. 대용어 해소 (Coreference Resolution)<br/>
 -> 영어에서는 대명사가 활발하게 쓰이기 때문에 매우 중요함<br/>
    한국어는 상대적으로 중요하지 않음 (그, 그녀 등을 쓰지 않음)<br/>
모두를 작은 것으로 나눠서 이후 파이프라인으로 통합함<br/>

### 유용한 자연어처리 모듈
- spaCy
- textacy

### 분류 모델을 사용하여 의미 추출하기
자연어처리의 대부분의 문제는 분류 문제<br/>
리뷰 텍스트를 넣고, 분류 모델을 만듦 -> 텍스트를 넣으면 별로 평점이 나옴<br/>
-	이게 어떻게 작동하는 지?
분류모델이 작동을 잘 하는 이유가 많은 리뷰가 계속 생성되고, 텍스트에 숨어있는 feature를 잘 찾아내서 작동함<br/>
-	의미 파악을 매우 빠르게 함
파이프라인에 따라 진행하려면 시간이 오래 걸리지만, 분류모델은 선형회귀나 로지스틱회귀로 계산하기 때문에 매우 빠르게 답을 얻을 수 있음<br/>
-	큰 학습 데이터가 필요함
작은 데이터 셋으로는 특징을 학습하기 힘듦<br/>
데이터 셋이 클수록 정확도가 높아짐<br/>
-	리뷰 분석기, 스팸 분류기 등…
-	의미 파악, 기계 번역 등 모든 것은 분류 문제라고 볼 수 있음
-	단어의 의미를 분석할 수 있는 임베딩도 

TPU의 경우 병렬계산을 더 잘 수행함<br/>
구글에서 소량 빌려줌<br/>


## Day 2

지난 시간 단어의 의미 추론을 분류로 학습시킴<br/>
연관 개념 - RNN, LSTM, encoder와 decoder, Attention<br/>

### RNN
언어데이터의 특징 - sequentiality<br/>
이런 특징을 잘 다루는 것이 RNN 네트워크<br/>
순서로 연결되는 데이터 - sequential한 데이터<br/>
Ex) 음향, 언어…<br/>
히든 레이어가 순환되어 sequential한 정보를 연결시킴<br/>
RNN은 short term 메모리로 인해 이전 데이터를 기억하지 못함<br/>

### LSTM
RNN의 vanishing gradient를 해결하는 모델<br/>
RNN은 히든 레이어 하나만 있었던 반면, LSTM은 셀이라는 추가된 long-term 메모리 레이어가 있음<br/>
무엇을 forget하고 keep할지를 결정<br/>
시그모이드, 탄젠트 하이퍼볼리 등의 함수들을 각 게이트마다 추가함<br/>
Forget, input, output… 게이트를 가짐<br/>
1. 시그모이드 값을 써서 잊어야 할 것을 0으로 만들어서 잊게 만듦<br/>
2. 하나는 시그모이드, 하나는 탄젠트하이퍼볼리를 통과함 (새로운 특징들이 더해짐)<br/>
   잊어야 할 값과 더해져야할 값이 셀로 넘어감<br/>
3. 아웃풋 게이트는 다음 스테이트는 어떻게 될지를 결정함<br/>

### GRU
Reset 게이트와 output 게이트로 LSTM을 단순화시킴<br/>
속도도 빠르고 성능도 뛰어남<br/>
뉴욕대학교 조경현 교수가 처음 함께 고안한 모델<br/>

### Seq2seq
기존의 RNN은 마지막 값으로 결과값을 얻는 반면, seq2seq의 인코더 디코더 모델은 인코더로 입력 문장을 하나의 벡터로 만들고, 디코더로 벡터를 target language로 변환함<br/>
입력 seq에서 인코더로 생성된 vector를 context vector라고 부름<br/>
하지만 이 역시 문장이 길면 길어질수록 하나의 제한된 벡터에 표현하는데 제한이 생김<br/>
RNN의 기본적 문제에 공착하게 됨<br/>
이런 인코더 디코더 문제를 해결하기 위해 attention모델이 나옴<br/>
LSTM에서는 keep, forget을 나눈 것처럼, 어디에 주목할 것인지를 score로 계산하는 것이 attention<br/>
인코딩의 어느 부분에 집중하게 될 지를 결정<br/>
모든 인코딩의 정보를 디코딩에서 사용하자 -> 인코더와 디코더 사이에 attention layer를 생성<br/>
모든 인코더의 히든 스테이트를 제공<br/>
인코더- 디코더 모델은 번역 모델에서 많이 사용되는 모델<br/>
기계번역을 할 때, source와 target이 어떻게 연결되었는지 align하는 것이 중요 (어텐션으로)<br/>

### attention
각각의 히든스테이트에서 어떤 입력값이 어떤 출력값과 연결되는지 관계 설정<br/>
Decoder의 히든 스테이트와 인코더의 히든스테이트를 비교하여 반영<br/>
Dot-product를 한다는 것은 두 값이 얼마나 비슷한지를 구하는 것<br/>
각각의 스코어를 확률값으로 바꾸는 것이 소프트맥스 함수를 취함<br/>
다음 어텐션 레이어에서 확률값은 원래의 값과 곱함<br/>
어텐션의 가장 주목되는 값을 디코더와 연결시킴<br/>
Dot-product값이 유사도를 구한 것임<br/>

### Attention의 예시
Bahdanau - 어텐션 모델의 선구자<br/>
Luong - 인코더 레이어를 두개 쌓고 진행<br/>
앞으로도 가고, 뒤로고 감<br/>
인코딩의 레이어를 몇 개씩 쌓는지는 사람마다 다름<br/>
GNMT - 2016년 8개의 LSTM를 거쳐서 어텐션 값을 디코딩을 함<br/>
마지막 출력 층에서 ResNet (residual net)을 거치지 않고 출력 값으로 전달<br/>
히든 레이어를 여러 개를 거치는데, 어떨 때는 거치지 않고 아웃풋을 얻는 것이 더 나음<br/>
8개에서 나온 값 <br/>

### summary
벡터값 하나로 만들지 말고, 각 스테이트의 값을 사용하자<br/>

### 질문
멀티해드 어텐션에서 포지셔널 정보를 기억하는 것과 포지셔널 인코딩에서 포지셔널 정보를 기억하는 것의 차이?<br/>
Value가 무엇인지?<br/>


## Day 3

### Transformer
각각의 단어의 값을 벡터로 변환하여 self-attention에 넣음<br/>
각각의 단어로 나온 어텐션 스코어를 피드포워드에 넣음<br/>
모든 것을 다 체크해서 이 단어가 어떤 단어와 가장 강한 어텐션을 가지는 지 <br/>

스코어를 쿼리, 키, 벨류 세 개의 값으로 어텐션 스코어를 얻음<br/>
쿼리와 키를 비교해선 얻은 값이 벨류<br/>
벡터에서 내적을 시키면 얼마나 유사한지 유사도가 계산됨 (dot-product)<br/>
소프트맥스를 취해서 확률값으로 바꿈<br/>
자기 자신과 자신을 내적한 값이 가장 클 것<br/>

쿼리 - 비교하는 단어 (타켓 랭귀지)<br/>
키 - 비교되는 단어ㅏ (소스 랭귀지)<br/>
벨류 -  (소스 랭귀지)<br/>

쿼리와 키를 곱하는 것은 유사도를 구하는 것<br/>
K의 길이에 영향을 받지않도록 <br/>

원래는 머신트렌스레이션에서 나온 것<br/>
입력 불어, 출력 영어의 경우 영어에서 쿼리를 취하고, 불어에서 키, 벨류를 취함<br/>

### positional encoding
-	포지셔널 정보를 넣어주기 위함<br/>

자신 이외의 값은 어텐션을 하지 못하게끔<br/>
틀리면 weight가 조정됨<br/>

### 질문
8층을 쌓아서 컨캣하는 것이 성능 향상에 무슨 영향이 있는지?<br/>
-> 할 때마다 웨이트가 다 다르기 때문<br/>

sequential하지 않고, pararell하게 처리할 수 있음<br/>
레이어별로 비주얼라이즈를 할 수 있어서 추적이 가능함 (버트 비즈 라는 툴이 있음)<br/>


## Day 4

### BERT

실제로 transformer 그대로 쓰기 보다는 BERT를 사용함<br/>
BERT는 사전 학습된 모델<br/>
BERT 이후 다른 사전 학습 모델이 많이 나옴<br/>

작년 2018년은 NLP의 획기적인 모델이 많이 나옴<br/>
-	ELMo, BERT, GPT, ULM-FiT…<br/>
-	BERT 그동안의 sequential 모델의 패러다임을 바꿈<br/>
-	어디에나 쓸 수 있는 pre-training을 하고, fine-tuning으로 다른 모든 task를 수행함<br/>
(기존에 어려울 것이라고 예측되던 부분)<br/>
-	1. 반 지도학습으로 지도학습을 시킨 training한 모델<br/>
2. 지도학습으로 특정 task를 수행<br/>
-	Meaning extract는 쉽지 않음<br/>
텍스트에서 의미 추출은 classification task (긍정, 부정, 중립)<br/>
-	NLP의 대부분의 task는 classification<br/>
-	대부분의 task에서 BERT의 성능이 다른 모델을 능가함<br/>

### Sentence Classification
-	Input을 입력 받아 사전학습 -> fine-tuning<br/>

BERT base와 BERT large가 있음<br/>
-	Base는 GPT와 같은 사이즈
-	BERT는 학습된 transformer encoder stack
-	BERT는 Transformer의 Encoder만 가지고 만듦 (번역 task를 할 것이 아니기에 디코더 필요 없음)
-	BERT base는 Encoder가 12개, large는 24개
-	Hidden layer도 768과 1024로 증가하였고, multi-head attention도 12개와 16개로 증가
-	[CLS] token이 문장 맨 앞에 붙임
-> 단어별 특징을 추출하거나 분류하기 위함
-	BERT의 사용법만 알 경우, 모든 task를 쉽게 수행 가능함

### BERT의 특징
-	Transformer의 Encoder만 사용함
-	BERT의 사전학습 모델로 특징 추출, 분류 task를 수행
-	RNN, CNN의 경우 직접 학습을 시켜야 했지만, BERT는 이미 사전학습 되어 있기에 fine-tuning만 함으로 task를 수행 가능함
-	Transformer는 직접 번역기를 만들지 않는 한 사용하지 않음

### Embedding
-	기존에는 one-hot Encoding
-	원-핫 인코딩은 단어 간의 의미관계를 파악할 수 없음
-	주변의 단어를 통해 단어의 의미를 파악하는 것이 word embedding
단어를 벡터로 -> word2vec
-	워드임베딩이 텍스트처리에 큰 기여를 함
-	학습 방법은 주변 단어들과의 관계로 학습
-	100차원의 벡터, 10000차원의 벡터 등으로 표현
벡터의 차원이 커질수록 의미의 미세한 표현이 가능함

### ELMo
-	동의어의 문제를 해결함
-	기존의 워드임베딩은 동의어의 문제를 해결할 수 없었음
-	단어의 context를 학습해서 단어마다 다른 벡터값을 학습함
-	2018년에 나옴
-	3개의 레이어로 문맥을 추측하여 좋은 성능을 냄
-	Language modeling으로 이후에 올 단어를 예측
-	LSTM 레이어를 쓰고, forward, backward 양방향으로 학습 하고 두 레이어를 concat
-	각 레이어에 각각의 weight를 곱함
-	문장을 넣어야 embedding이 나옴
-	같은 stick일지라도 다른 vector값을 가짐 (다른 문장으로 학습하였기 때문)
-	임베딩으로 나온 값에서 특정 단어의 벡터를 추출함 (feature extraction)
-	ELMo의 경우 레이어가 올라갈 경우 단어의 context 벡터를 잘 학습함

ULM-FiT도 사전학습을 함<br/>
Transformer<br/>
OpenAI Transformer<br/>
-	BERT가 나오기 전에 디코더만을 가지고 학습을 함<br/>
-	Encoder를 넣지 않았기에 참조값 x<br/>

### BERT
-	트랜스포머의 인코더의 값을 참조
-	ELMo의 bidirectional함은 두 방향을 concat한 것
-	BERT는 동시에 한 포인트에서 bidirectional 학습을 함 (masking으로 가능했음)
-	학습 값이 [CLS]에 담겨 있음
-	15% 확률로 [mask], 다른 단어, 기존 단어로 대체
-	이 단어를 앞, 뒤 단어로 학습을 하기 때문에 성능을 향상시킴
-	이 학습을 함으로써 양 방향 학습이 가능
-	첫 번째, 두 번째 문장 끝에 [SEP] token을 넣음
-	1. [mask]된 값을 train함
-	2. 첫 문장과 두번째 문장이 연속된 문장인지 train함
-	BERT 임베딩은 ELMo와 같이 문맥에 따라 다른 의미의 단어의 의미를 알 수 있음
-	마지막 레이어의 학습 값이 가장 좋을지?
레이어마다 학습되는 값이 다르기에 모든 레이어의 합이 가장 좋은 학습 값을 가짐
다른 task에서는 두번째부터 마지막 레이어의 합이 가장 좋은 학습 값
-	Feature-extraction도 가능하게 되어 있음
-	개체명 인식

### BERT 특징
-	Wordpiece
- unknown 토큰을 없애기 위해 토크나이징
- wordpiece를 어떻게 자르냐에 따라 성능이 달라짐
-	3가지의 토큰 값을 합쳐서 값을 얻음

### Fine-tuning
-	실제 pre-training 모델을 가지고 진행
-	cls는 바이너리 클래시피케이션
-	멀티 클래스로 classification을 할 경우 멀티클래스가 될 수 있게 마지막 히든 레이어에 소프트맥스를 씌움
-	모든 task에서 가장 좋은 성능을 보여줌

### XLNet
-	Autoregressive LM?
이전 두 단어, 혹은 이후 두 단어를 가지고 예측함
context word에서 단어를 예측함 (GPT…)
일반적 NLP 테스크에 큰 성능
하지만 앞, 뒤 동시 학습을 하지 못한다는 특징
-	버트는 오토인코더
앞에서도 뒤에서도 [mask]된 단어를 예측함
버트의 단점은 [mask]를 임의로 넣고 사전 학습을 함
예를 들어 baking crisis의 경우 두 단어가 dependent한데 independent하게 마스킹을 함
-	그래서 permutation을 사용함
어떤 포지션이 있으면 서로 permute시키면 전체 토큰수의 팩토리얼 개수 만큼 가능한 경우의 수가 나옴
t의 t-1의 토큰으로 학습
-	아이디어는 굉장히 놓음
한국어 조사의 경우 이 경우에 해당
하지만 모든 경우를 팩토리얼 만큼 계산을 해야 하기 때문에 계산량이 매우 많음

### 에트리의 KorBERT
-	형태소 분석기
-	Classifier와 feature-extraction을 하면 목적에 맞게 쓸 수 있음
SKT의 KoBERT<br/>
서울대도 만들고 있음 - 다른 방식으로 (하지만 힘듦 ;;;)<br/>

### Fine-tuning 실습
허깅페이스의 프리트레인드 된 웨이트를 가져와서 클래시피케이션을 함


## Day 5

형태소 분석을 하면<br/>
먹었겠더라… 형태소 간의 의미없는 관계 분석이 됨<br/>
한국어는 임베딩과 관련된 다른 이슈가 있음<br/>
Word2vec의 기본 아이디어는 skip-gram(중심단어로 주변단어 예측) / cbow<br/>

Word2vec은 토큰 단위<br/>
Fasttext는 서브워드 단위로 분절함<br/>
대부분 영어에서 glove를 많이 씀<br/>

사전학습된 워드 임베딩을 가져옴<br/>
