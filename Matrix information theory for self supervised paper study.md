contrastive larning은 큰 틀에서는 alignment와 uniformity다. 

같은 input으로부터의 다른 augmentation의 결과 \-\> z\_1 , z\_2일때,

maximum entropy encoding을 추진하는 loss의 예시:

L\_mec \= \-gamma\*log(det(identity\_d \+ lambda\*z\_1 \* z\_2\_T))

q) det안의 식은 항상 대각행렬인가?맞다면 왜?

Learning method로 볼때, 1\) contrastive learning 2\) Non contrastive learning이 있다.  
Loss function은 1\) Uniformity \+ Alignment 2\) Uniformity가 있다

현존하는 maximum entropy encoding framework는 명시적으로 다른 branch로부터 기연한 feature matrices를 구별하지 않는다.

MCE \= maximum cross entropy

이 논문에서의 알고리즘 Matrix SSL은 matrix alignment loss를 non contrastive methods로 통합한다. \-\> 실증적 결과 향상

Matrix SSL \= Matrix Uniformity \+ Matrix Alignment loss components

Matrix Uniformity는 identity matrix I\_d와 함께 aligns cross covariance matrix of feature matrices Z\_1,Z\_2를 한다.

Matrix Uniformity loss는 주로 행렬의 요소들이 특정한 방식으로 균일하게 분포되도록 유도한다. 값의 편향이나 쏠림을 최소화한다. \-\> 데이터 다양성 보장

e.g) Frobenius Norm 기반 Uniformity loss : 행렬의 각 요소가 균일하게 작아지도록 강제하는 방식.

반면에, Matrix alignment는 z1,z2의 auto covariance matrices를 aligning하는데 집중한다.

by-product : 

closed form : 

closed form relationship between effective rank and matrix KL : 

effective rank는 ml methods평가하는데 좋은 메트릭이다.  
matrix A가 있을때, 이 A의 singular value들에 대한 entropy다.

이 논문은 imagenet datasets에 대해 sota 달성했다.(linear evaluation settings인 경우에는 특히 그러하다)

coco detection같은 전이 학습의 경우에도 sota다.  
background : self supervised learning은 unlabeled data로부터 의미있는 representations를 학습하기 위한 방법론이다. 보통은, 2-view augmentation을 사용한다.   
1\. online network   
2\. target network

보통은 input data에 random transformation을 사용한다 \-\> z\_i라는 feature representation을 generate한다. 

이 z는 contrastive learning이냐 non contrastive learning이냐에 따라 다르게 처리된다

1\. contrastive learning

similar object는 align하고 dissimilar object는 apart시킨다. infoNCE가 가장 보편적인 contrastive learning이다. 여기서는 cosine similarity를 쓴다.

2\. Non contrastive learning

feature embeddings에 대한 total coding rate을 극대화하길 바란다.   
online network와 target network 둘다 feature map f의 approximations라는걸 감안하면 zz\_T를 추정하기 위해 z\_1와 z\_2의 cross covariance를 사용한다.

maximal entropy coding(MEC) loss는 항상 대각행렬이 되나?

모든 non zero A에 대해 A\*A\_T는 positive semi-definite다. 이걸 활용한다. strong minimization property가 있으므로

TCR과 MCE/MKL의 연결점을 만들어야한다.

4.의 MCE-based uniformity loss definition은 regularized된 covariance matrix ZZ\_T와 regularized(scaled) identity matrix와의 거리를 측정한다.

이 논문의 Main theorem : 모든 TCR loss는 MCE/MKL loss로 변형이 가능하다.(반대는 불가능하다. TCR은 operand가 하나고 MCE/MKL은 2개이므로

Matrix uniformity and alignment : TCR loss를 최소화하는 covariance matrix는 scaled identity matrix다.

하지만, 만약 직접적으로 Z의 covariance를 사용하면 최적화는 sub optimal이다

theorem 5.1에 의해, 만약 covariance matrix를 centered하더라도 여전히 scaled idenetity matrix와 align될것이라는 것을 정당화한다(maximal effective rank와 unit trace에서).

matrix information uniformity \= 특이값이 같을때 \-\> (1/d)\*identity

이 논문에서는 supervised, contrastive, non contrastive의 차이점을 탐구하기 위한 단일 툴로 effective rank를 사용할 것을 제안하고 있다.

Experiment

1\. 각각의 image에 대해 augmentation을 두번씩 적용 \-\> 두 different views  
2\. Siamese network로부터 branch 하나 선택하고(online network로 사용), 다른 branch 하나는 target network로 사용.   
3\. 특이점 하나 : loss backward 사용하지 않고 exponential moving average method 통해 parameter를 update한다.  
