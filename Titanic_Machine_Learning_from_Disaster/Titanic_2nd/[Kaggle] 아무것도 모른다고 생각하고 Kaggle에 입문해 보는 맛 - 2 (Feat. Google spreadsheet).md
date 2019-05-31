## 1. 데이터에 대한 간략한 설명(이어서)

지난 글에 이어 미처 다 하지 못한 데이터에 대한 설명을 이어서 진행해 보겠다. 먼저 데이터들이 현재 스프레드 시트상으로 나타나 있으며 크게 행(Row)과 열(Column)로 나눠서 볼 수 있고 Row에 해당하는게 PassengerID 즉 승객 개개인을 뜻한다(숫자로 색인을 했다고 보면 될 것 같다) 먼저 train.csv에서 Passenger ID를 살펴보면, 1번 승객부터 891번 승객까지 나와 있으며, Test.csv에는 892번 승객부터 1309번 승객까지 나와 있다. 즉 원래 Train과 Test 데이터는 하나의 데이터 였으며, 일부 데이터(train.csv)만 가지고 학습이나 분석을 통해 예측한다고 생각하면 된다. 그 다음에 각각의 Column들에 관한 설명을 해보자면 다음과 같다.



* ```Survived``` : 생존 여부를 뜻한다 : 살았으면 1(True), 죽었으면 0(False)
* ```Pclass``` : 타이타닉 배 승선권 등급을 뜻한다(1 = 1등급, 2 = 2등급, 3 = 3등급, 티켓의 등급은 **사회적 부와 지위**가 어떤지 간접적으로 보여준다)
* ```Sex``` : 단순하다. 남성인지 여성인지를 뜻한다(male(남성), Female(여성))
* ```Age``` : 승객의 나이를 뜻한다(해당 데이터를 살펴보면 곳곳에 누락되어 있다(데이터가 아예 존재하지 않음))
* ```SibSp``` : #(Number) Of **sib**lings / **sp**ouses aboard the Titanic 이 말은 타이타닉 호에 **동승한 가족 중 형제 자매와, 배우자의 총원**을 의미한다(형제자매는 이복형제자매까지 가능하고 배우자는 실제 법적으로 결혼한 사이에 한함(정부(내연녀), 약혼자 제외))
* ```Parch``` : 위와 같은 의미로(**Pa**rents, **Ch**ildren) 타이타닉 호에 **동승한 가족 중 부모님과 자식들의 총원**을 의미한다(아이들은 친자식과 입양, 다 포함, 때때로 nanny(유모)와 같이 온 아이는 해당 값이 없다(부모님과 같이 안왔다 '0')라고 나와 있음)
* ```Ticket``` : 티켓의 고유 번호(일련번호, 큰 의미가 있을 것 같지 않다)
* ```Cabin``` : 객실번호(이 데이터 역시 누락된 값이 많다)
* ```Embarked``` : 타이타닉 배를 승선한 곳(선착장)



## 2. 데이터 전처리(Preprocessing)
이제 각 데이터들이 어떤건지 대략적으로 살펴보았고 데이터를 본격적으로 사용해보기 전에, 제대로 정제하여 써보려고 한다. 데이터의 종류가 많거나, 전부 다 사용한다고 해서 정확도(Accurancy)가 잘 나오지 않는다. 지금 하고 있는 타이타닉 과제를 생각해 보면, 데이터 상에서 사람들의 생존에 영향을 주는 Feature(특징, 요소)를 찾아야 한다.

---------------------------------------------------------------------------

### 	2.0 전처리를 하기에 앞서

바로 Python을 사용해서 데이터 분석에 들어가도 좋으나, 앞서 언급했다시피 구글 스프레드시트를 통해 어떤 논리와 과정으로 흘러 갈 것인지 확인해 볼 것이고, 엑셀만 사용해도 단순 함수 계산으로도 원하는 데이터를 정제해서 확률을 올리는 작업이 가능하다는걸 보이기 위해 간단하게나마 진행을 하고 78~80% 정도에 정확도를 띄우는 정도로 해보고 바로 Python을 이용한 데이터 분석을 진행해 보겠다.

---------------------------------

### 	2.1 단순한 가정에서 부터 시작 → 모두 죽었다고 가정

타이타닉 대회를 시작하면서 관련 데이터와 정보를 모른다고 생각하고 접근하기로 했었다.(제목을 보면 그렇다) 일단 데이터를 한 두번 들여다 봤으나, 실제 데이터 상에서 얼마나 죽었는지 살았는지 파악을 빨리 해보고 싶다 그러기 위해선 어떻게 해보면 좋을까 ? 그렇다 다 죽었다고 생각하고 몇 %의 적중률이 나오는지 확인하면 된다.



![origin_is_important](https://github.com/ybear90/Kaggle_competition/blob/master/Titanic_Machine_Learning_from_Disaster/Titanic_2nd/origin_is_important.PNG)

> 원본은 소중하므로 유지한 상태에서 사본을 만들어 작업하는게 좋다.

여기서 우리가 필요한 데이터는 PassengerID에 대응하는 Survive 값이므로 test.csv를 이용하여 Kaggle에 제출할 데이터를 만들어보자



![they_all_perish](https://github.com/ybear90/Kaggle_competition/blob/master/Titanic_Machine_Learning_from_Disaster/Titanic_2nd/they_all_perish.PNG)

> 시트의 맨 왼쪽 위의 직사각형 칸을 눌러주면 전부 선택 되고 사용할 쉘을 제외하고 모두 삭제를 진행해준다(```delete``` 키를 사용)



![save_csv_file](https://github.com/ybear90/Kaggle_competition/blob/master/Titanic_Machine_Learning_from_Disaster/Titanic_2nd/save_csv_file.PNG)

> ```파일``` - ```다른 이름으로 다운로드``` - ```쉼표로 구분된 값(.csv 현재시트) ``` 를 눌러준다 이름은 보통 이런식으로 자동완성 된다 test - [탭이름].csv



![submit_process](https://github.com/ybear90/Kaggle_competition/blob/master/Titanic_Machine_Learning_from_Disaster/Titanic_2nd/submit_process.PNG)

만든 파일을 드래그 해서 올리는 식으로 ```Upload Files```에 올려주고 ```Make Submission``` 버튼을 눌러주면 제출이 진행되고 아래와 같은 결과를 얻을 수 있다



![Result_all_perish](https://github.com/ybear90/Kaggle_competition/blob/master/Titanic_Machine_Learning_from_Disaster/Titanic_2nd/Result_all_perish.PNG)



답을 다 0처리(사망처리) 해버려서 적게 나올 줄 알았지만. 의외로 과반 이상 나왔다(타이타닉 해상사고에서 생존한 사람보다 죽은 사람이 더 많았다는 뜻)



--------------------------------------

### 	2.2 변수(Feature)를 하나씩 추가하기 시작

구글 스프레드 시트를 통해서 gender_submission.csv와 같은 형태로 test.csv 데이터 사본을 이용, Label(정답)에 답을 달아 제출하는 일련의 과정을 테스트 해 보았다. 이를 이용하여 다른 Feature들을 고려하여 답을 올려 보도록 해보자.

-------------------------------------------

#### 		2.2.1 여성만 살려보기(Sex feature만 이용)
정답 csv 파일을 만드는 방법은 앞 과정에서 다 설명이 되었으리라 생각이 되고 모두 다 사망으로 처리한 상태에서 다른 Feature를 고려하여 다른 답을 만들어 내는 과정을 진행해보겠다.

새로 적용하고 싶은 Feature를 반영하기 앞서 훈련(학습)용 데이터인 ```train.csv```를 통해 데이터 분석을 진행 해 보려고 한다. 원본 데이터는 ```train.csv```와 ```test.csv```를 합친 데이터지만 실제 답이 적혀져 있는 데이터는 ```train.csv``` 이므로 이 데이터 파일만 가지고 분석을 진행해 보겠다.

우리가 먼저 고려할 Feature는 Sex(성별 이므로) 모든 Feature들이 섞여 있는 데이터에서 Sex와 Survived와의 관계를 보기 위해 스프레드 시트 상에서 피벗 테이블을 통해 그 수치를 확인하는 작업을 진행해 보겠다.



![pivot_table_making_2](https://github.com/ybear90/Kaggle_competition/blob/master/Titanic_Machine_Learning_from_Disaster/Titanic_2nd/pivot_table_making_2.PNG)

> 위와 같은 이미지 처럼 피벗 테이블을 생성해준다.



![pivot_table_making_3](https://github.com/ybear90/Kaggle_competition/blob/master/Titanic_Machine_Learning_from_Disaster/Titanic_2nd/pivot_table_making_3.PNG)



피벗 테이블을 생성해 주면 위와 같이 새로운 스프레드 시트 탭이 생기고 테이블을 만들 수 있게 오른편에 행과 열과 값 탭이 설정 되어 있다. 여기서 위와 같이 행(우리가 사용할 Feature 값), 값에는(Label, 얻어낼 정답, 값)등을 추가해 주면 된다.



![pivot_table_making_4](https://github.com/ybear90/Kaggle_competition/blob/master/Titanic_Machine_Learning_from_Disaster/Titanic_2nd/pivot_table_making_4.PNG)

> 추가한 값들로 만든 테이블에서 Survived의 탭에서 SUM 하고 COUNT 옵션 값을 사용했는데 Survived의 raw data를 살펴보면 죽었을 때 0 이고 살았을 때 1이므로 SUM 옵션 값 자체를 성별 당 생존한 인원 수 라고 생각해 볼 수 있고 COUNT 값은 해당 컬럼 데이트 총 개수 이므로 해당 성별의 총 인원 수로 생각해 볼 수 있다. 실제로 생존률(전체 성별 인원 당 생존 인원 * 100)을 구해보면 여성의 생존률이 모두 다 죽었을때 확률보다 월등히 높으므로 여성일 때 다 살리는 쪽으로 세부 판단을 내리면 확률이 조금은 상승할 것이다.





![woman_only_survived_graph](https://github.com/ybear90/Kaggle_competition/blob/master/Titanic_Machine_Learning_from_Disaster/Titanic_2nd/woman_only_survived_graph.PNG)

> 스프레드 시트에서 삽입 - 차트 메뉴를 이용하면 이렇게 피벗 테이블을 이용한 그래프도 그려 낼 수 있다. 그래프를 통해 한 눈으로 Feature 당 Label 값의 추이를 확인할 수 있다.(여성 부분을 보면, COUNT와 SUM 값의 차이가 실제로 짧고 남성은 크다)



위 결과를 바탕으로 ```test.csv```에서 사본을 생성한 뒤 그 사본에서 Pclass 왼편에 새로운 열을 만들어 주고 거기에 다가 시트 수식으로 여자는 생존했고 남자는 죽었다는 식으로 필터링을 진행해 보겠다. 엑셀을 해보거나 스프레드 시트를 많이 사용한 사람들은 수식을 어떻게 입력해야 하는지 아시겠지만 일단 이런 식으로 새로만든 열에 적용하면 될 것이다.

<pre><code> = IF(E2 = "female", 1, 0)</code></pre>

> Survived 열에 적용할 수식인데 그대로 해석 해 보면 E2(Sex에 해당하는 열에 첫 데이터 좌표)값이 "female"이면 1(살았다), 아니면 0(죽었다)를 반환해라 라는 단순 조건문이다.



이렇게 답을내는 것 까지 해보았는데 문제는 이것이다 답을 낸 데이터를 제외하고 지우려고 보니, E2 이하 모든 데이터가 삭제되게 되고 그러면 해당 수식에서 값이 사라지는 결과가 초래되므로 값 결과에 에러가 발생하게 된다. 이를 방지하기 위해 수동적으로 처리할 조치는 다음과 같다.



> 먼저 Survived 열의 복사 열을 오른쪽에 만들어 주고 원본 열을 복사 처리 해 준 다음, 복사 열에 결과만 붙여넣기 하고 나머지 열들을 삭제해 주고 사본 열을 B열로 땡기면 된다. 해당 작업을 다 진행하면 아래와 같이 나오게 될 것이다.



![woman_only_survived_submit](https://github.com/ybear90/Kaggle_competition/blob/master/Titanic_Machine_Learning_from_Disaster/Titanic_2nd/woman_only_survived_submit.PNG)



위의 제출결과는 굳이 확인하지는 않겠다. **(gender_submission.csv 원본 값하고 동일한 결과)**



#### 		2.2.2 성별과 배 승선권 등급을 추가해보기(Sex, Pclass feature 이용)

또다른 Feature를 사용하여 확률을 좀 더 높여보기 위해 이번엔 재력(경제력)하고 연관이 있는 Pclass를 사용해 보려고 한다. 이렇게 생각해 볼 수 있다. ```돈이 많은 사람일 수록 해상사고 당시 먼저 구출되어 생존할 가능성이 높을 것이다.```



위에서 했던 방식하고 유사하게 분석을 진행할 것인데, ```train.csv```에서 피벗 테이블을 생성한 다음, 행에는 Sex, Pclass를 추가해 주고 값에는 Survived SUM COUNT 값 들을 추가해 본다. 결과를 살펴보면 아래와 같다



![Sex_Pclass_pivot_table](https://github.com/ybear90/Kaggle_competition/blob/master/Titanic_Machine_Learning_from_Disaster/Titanic_2nd/Sex_Pclass_pivot_table.PNG)



표를 살펴보면, 유독 특이한 부분이 보일텐데, 여성의 생존 데이터 중 Pclass가 3일때의 데이터를 보면 생존률이 정확히 **50%**로 떨어져 있는 것을 확인 할 수 있다. 그래서 이 부분을 생존(1) 이 아닌 사망(0) 처리하면 오를까 ? 라고 생각할 수 있으나, 사실상 절반 절반이므로 상승을 안하던가 약간 떨어 질 수 있어 이 부분을 굳이 수정하여 답을 내릴 필요는 없다고 본다. 나머지 데이터 추이도 기존 확률을 올릴만한 특이한 feature는 보이지 않는다. 그렇다면 Pclass를 배제 할까 ? 그렇게 바로 처리하기 보단, 다른 Feature와 중첩 시켜 세부적으로 판단해보도록 하자. 



#### 		2.2.3 선착장 정보에서 특이한 점 발견(Sex, Pclass, Embarked feature 이용)

다른 Feature로 어떤 것을 대입해 볼 수 있을지 생각을 해 보았을 때, 우선적으로 시도해 볼만한 Feature들은 요금(Fare)과 동반 가족 수(SibSp, Parch), Embarked(승선한 선착장) 이렇게 보여진다, 나머지는 고유명사 이거나, 승선권의 일련번호라서 수치적으로 바로 따지려면 조건이나 가설 그리고 배경지식을 동원하여 수치화 하지 않는 이상 어렵다. 그래서 수치적으로 바로 분석할 수 있는 Feature들 중에 Embarked 데이터를 Sex, Pclass Feature에 더하여 피벗 테이블로 확인해 보겠다. Fare의 값의 스펙트럼은 넓어서 이 또한 데이터를 특정 기준으로 전처리 해주지 않는 이상, 의미있는 Feature가 되기 어렵고, 동반 가족 수 또한 각각 독립적으로 다루거나(SibSp, Parch 따로), 단지 각각 Feature에서 유무(인원수에 상관없이)만을 따졌을때는 확률이 그대로이거나, 오히려 감소하는 결과가 있었다. 그래서 남은 Embarked Feature를 적용된 기존 Feature(Sex, Pclass)에 합쳐서 보기로 한 것이다.



![Sex_Pclass_Family_ind](https://github.com/ybear90/Kaggle_competition/blob/master/Titanic_Machine_Learning_from_Disaster/Titanic_2nd/Sex_Pclass_Family_ind.PNG)

> 애석하게도, 이와 같이 사전 전처리 없이 Feature를 추가하다간 확률이 역으로 떨어지는 결과를 초래할 수 있다. 데이터를 가설을 통해 논리적으로 꼼꼼히 짚어서 구체적은 수치기준으로 경우의 수를 분류해 주거나 Feature를 조정하는 것이 조금이나마 확률을 올릴 수 있는 방법이 된다.(Feature Engineering)



![Sex_Pclass_Embarked_pivot_table](https://github.com/ybear90/Kaggle_competition/blob/master/Titanic_Machine_Learning_from_Disaster/Titanic_2nd/Sex_Pclass_Embarked_pivot_table.PNG)



위 피벗 테이블을 확인해 보면 3등급의 여성 승객이 어떤 부분에서 사상자가 많이 발생했는지 쉽게 알아볼 수 있는 부분이 있다. S(Southampton) 선착장에서 3등급 승선권을 구매한 여성들이 유독 많은 사상자가 발생한 것이다. 정확한 사건 경위 및 사유는 모르겠으나 데이터가 그렇게 이야기 해주고 있으므로 스프레드 시트의 수식을 좀더 정교하게 구성하여 3등급 중 S선착장에서 승선한 여성들의 과반을 죽었다고 판정하여, 확률을 조금 더 높여볼 수 있지 않을까라고 결론을 내렸고 아래와 같이 조건 수식을 구성하였다.

<pre><code> = IF(E2 = "female", IF(C2 = 3, IF(L2 = "S", 0, 1), 1), 0)</code></pre>

설명을 하면, 여성들 중 3등급의 승선권을 사용하고 그 중에서 S선착장에서 탄 사람들은 죽이고 나머지는 살린다, 남성은 다 사망처리한다. 이렇게 해석하면 되겠다. IF가 3중으로 중첩되어서 조금 헷갈리지만 경우를 잘 나눠서 살펴보면 직관적으로 바로 이해 될 것이다.



이렇게 나온 결과를 대입해 보면 아래와 같은 스코어를 얻을 수 있다.

![Sex_Pclass_Embarked_submit](https://github.com/ybear90/Kaggle_competition/blob/master/Titanic_Machine_Learning_from_Disaster/Titanic_2nd/Sex_Pclass_Embarked_submit.PNG)

**gender_submission : 0.76555**에서 **0.77990** 으로 **0.014**정도 확률을 끌어올렸다! 이렇게 확률을 올려나가면 된다.



#### 		2.2.4 SibSp, Parch 정보를 어떻게 이용해 볼까 ?(서로 다른 데이터 정보 합쳐보기)

앞서 추가로 적용했던 Feature들 중에 여러 시도끝에 유의미한 결과를 이끌어 내지 못했던 Feature가 있다. 바로 SibSp와 Parch인데 앞서 사용했던 가정(가족의 유무만 판단, 아무런 전처리 없이 Feature추가로 적용)외에 이렇게 생각할 수 있는 부분들이 있다.

> 가족에 관련된 각각 Feature를 하나로 합쳐서 ```가족의 규모```로 새로운 Feature를 만들어서 적용해 보면 어떨까 ? 



Train데이터에 새로운 Feature인 FamilySize를 추가했다. 다만 좀 더 객관성을 띄는 FamilySize 값을 만들기 위해 SibSp + Parch 한 값에 1을 더하겠다(가족은 나 자신도 포함되므로, 혼자일땐 FamilySize = 1) 앞에서 했던 방식대로 데이터의 경향성을 수치적으로 한눈에 보기 위해 피벗 테이블을 만들어 보면, 조금 확률을 올릴 수 있을 만한 여지를 확인해 볼 수 있다. 앞의 조건을 그대로 고려했을 때, 여성은 3등급에서 S인 경우에는 다 사망 처리 하는 경우를 제외하곤, 모두 생존인 상태이다. 그래서 추가로 더 죽일 수 있으면 죽이던가, 조금 더 살릴만한 세경우가 보이면 몇명 살려보는 것도 나쁘지 않을 것이다.  라고 생각은 했으나, 피벗 테이블 상에선 유의미한 결과를 찾지 못했다.(직접 피벗 테이블 그려보면 바로 확인 가능하다)



![new_feature_family_size](https://github.com/ybear90/Kaggle_competition/blob/master/Titanic_Machine_Learning_from_Disaster/Titanic_2nd/new_feature_family_size.PNG)



## 3. 정리 및 다음편에 진행할 사항

실제 파이썬 및 여러 외부 라이브러리와 머신러닝 라이브러리를 이용하여 바로 분석하기에 앞서, 구글 스프레드 시트를 활용하여 머신러닝 알고리즘이 하는 것 처럼 엑셀 노가다로 그럴싸하게 데이터 분석을 하는 과정을 거쳐보았다.  실제 머신러닝 알고리즘 처럼 수학적인 미세 모델링을 통해 여러 경우를 나눠서 판단 내리려면 며칠이 걸려도 모자를 수 있다. 그래서 이를 좀 더 빨리, 정확하게 여러 경우의 수를 수학적인 미세 모델링으로 확인하기 위해 다음 편에서는 본격적으로 파이썬을 사용하여 타이타닉 경진대회를 진행해 보겠다.