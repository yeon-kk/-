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
