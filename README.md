## Linear Regression  
![LinearReg](https://user-images.githubusercontent.com/86847564/143281799-575b292b-b68d-4dad-bb19-ba290360a172.gif)

data set : 1500, random_normal, heights, weights  
X: heights  
Y: weights  

weights = heights * 0.4 + 1 + random_noise  

hypothesis: weights = heights * W + b  
W means parameter, weight  
b means parameter, bias  

epoch: 100  
in 16 epoch weights(W and b) converged on a straight line  

Model predicts that W == 0.40570816 and b == 0.05904188  
![predict](https://user-images.githubusercontent.com/86847564/143284579-bf6a1055-6c60-4345-bb64-19af9be0da51.png)

### input data ? 입력데이터의 '갯수' 가 '아님!' . 입력 데이터의 특징의 수라고 생각해야 한다.  
예: 붓꽃 데이터 개수를 입력데이터 노드 개수에 반영되는게 아니라, 꽃받침 길이, 꽃받침 너비, 꽃입 길이, 꽃잎 너비 이렇게 4개가 되어야 한다.  
헷갈리기 때문에 잘 기억해야 함

keras 코드를 이용해서 손실값을 구하는 경우 binary cross entropy는 출력층 활성화함수로 softmax가 아니라 sigmoid를 사용하는 경우도 있다.  
tf.keras.losses.SparseCategoricalCrossentropy : 출력이 one-hot encoding 형태가 아니라 정수형인 경우  
tf.keras.losses.CategoricalCrossentropy : 출력이 one-hot encoding 형태인 경우  

레이어와 노드 수를 헷갈리지 말기  
은닉층 레이어 갯수는 노드수가 아니다. 입력층 은닉층 출력층으로 생각하면 좋음.  

GAN  
구분자를 먼저 훈련시킨 뒤, 생성자를 훈련시키는 순서로 진행.  
cross entropy loss : GAN은 0과 1사이의 실수값을 출력하기 때문에, 여기에 log를 씌우면 log는 (0,1] 범위에서는 (음의무한대,0]이기 때문에 0으로 가까워진다는 것의 의미는 최대화 한다는 의미. (0으로 가까워지거나 음수값을 갖게 되기 때문에 0이 가장 큰 수)

Fully Connected Network
완전 연결 계층. 가장 먼저 배우는 그림을 떠올려보면 되는데, 모든 노드들이 연결되어있는 것을 의미한다.  

배치정규화 : tf.compat.v1.layers.batch_normalization  
어디에서 배치 정규화를 주로 하는지?  
Affine 계층 -> 배치정규화 -> 활성화함수  
배치정규화 이후에 행렬곱을 했었는데, 그러면 안됨.  
대신 활성화함수 이후에 배치정규화를 하기도 한다.  
W*X + b 이후에 정규화를 진행  

AutoEncoder 특징  
비지도 학습, label이 주어지지 않는다  
입력층 노드 수보다 은닉층 노드 수가 적다. 이유는 특징을 압축하는 효과(Pooling과 유사한 효과인것 같다)  
@ 과제를 할 때, 인코더와 디코더에 레이어를 추가한 경우 특징을 잘 잡아내지 못하고 노이즈가 발생.  

GAN 특징  
생성자와 구분자를 따로 학습  
생성자보다 구분자를 먼저 학습.  
생성자를 학습할 때는 구분자를 학습하지 않는다. (dropout batchnormalization등 적용할 때 주의)  
활성화 함수를 다양하게 적용해볼 수 있다.  
출력값은 0~1 사이값으로 표현되며, 생성자의 경우 구분자가 1에 가깝게 출력되는 것을 목표로 하고 구분자의 경우 진짜를 진짜라고, 가짜를 가짜라고 판단해야 하기 때문에 진짜 이미지에 대해서는 1에 가깝게 판단해야 하고, 가짜 이미지에 대해서는 0에 가깝게 판단해야 한다.  
이떄문에 손실함수 log를 이용하여 log(1-(가짜이미지)) log(진짜이미지) 값을 얻게되며, log이기 때문에 0에서 1 구간에서 음의 무한대부터 0까지를 y값으로 갖게 된다.  
이는 0이 '최댓값'이기 때문에, 최대화 하는 방향으로 손실함수를 작성해야 하는것을 의미하며, tf1 버전의 경우 minimize를 사용해야 하기 때문에 반드시 음수값을 붙여준다.  

CNN을 구현하는 것보다, 전이학습을 통해 얻은 결과가 더 높은 경우도 있지만 그렇지 않은 경우도 존재함.  
만약 학습한 데이터가 테스트할 데이터와 유사하거나 같은 카테고리라면 어느정도의 성능을 기대할 수 있지만, 그렇지 않은 경우라면 오히려 정확도가 떨어질 수 있기 때문  
