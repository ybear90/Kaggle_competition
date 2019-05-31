## 1. 서론 - 다시 시작해보는 Data Science

요즈음 데이터 사이언스가 4차 산업혁명 광풍과 더불어 많이 대세화가 되가는 것 같다. 필자 본인도 3년간의 군생활을 마치고 중단했던 전공에 대한 전문성을 어떻게 끌어올려서 취업, 진학을 할까 계속 고심을 하며 조금씩 공부 자세와 마인드를 잡아나가고 있었지만, 학부시절때 제대로 마무리 하지 못한 머신러닝 관련 졸작 및 인턴쉽 과제들을 통해 뼈저리게 실력의 부족함을 통감하고 이게 역으로 나에게 데이터 사이언스를 공부하는데 있어 알게 모르게 트라우마처럼 작용했었다. 심적 방황을 하면서 전공 관련 책들과 인터넷 글들을 읽어나가는 중에 SNS등지에서 내 눈을 스쳐갔던 광고 하나가 생각이 났다. DS school 광고 였는데, 사실 일종의 가격이 만만찮은 DS관련 부트캠프로 생각을 하고 있었으나, 수강 후기란에 알고 있는 이름이 보여서 묘하게 신뢰감이 갔었고 가만히 있으면 진행이 안되고 시간만 흘러가기에 아까운 시간을 생각하며 군생활 하면서 모아둔 퇴직금 일부를 깨서 아직 완전 모른다 스스로 가정하고 입문반 부터 신청을 했다. 그렇게 머신러닝, 딥러닝, AI에 대하여 닫았던 생각을 다시 열게되는 직접적인 시작이 되었으리라곤 상상도 못했다.  
다른 수강생 분들은 입문반 프로그램의 주차별로 강의 내용과 느낌, 얻어 가는 점을 간략하게 정리하거나 해당 수업 관련 파일을 깃허브나 블로그에 일부 업로드 하는 등으로 정리되어 있었다, 나는 이렇게 해 볼 생각이다. 기본적인 4주간의 수업 내용의 뼈대와 핵심내용은 시간이 지난 지금도 머리에 꽤나 잘 남아 있는 편이라고 생각하고, 파이썬 기본 문법이나 기본적으로 오피스 사용하는 방법은 이미 알고있거나 금방 터득하는 편이기에, 따로 기록 복습을 진행하지 않은 상황이지만. 이걸 처음 데이터 사이언스에 입문사람이 내 앞에 있다고 생각하고 조금은 장황해 보일 수 있는 스토리텔링 형식으로 사소한 내용이라도 오해 및 오개념 등을 최소화 하면서(나도 사람이기에 피드백은 적극적으로 받을 생각이다) 내가 공부하고 배웠던 내용들을 여기에 최대한 녹여볼 생각이다. 하지만 나 역시 초심자이고 배울게 한창인 사람이기 때문에 혹시라도 잘못된 내용을 설명하고 있거나 이해가 잘 되지 않는 부분이 있다면 주저없이 피드백 주시면 감사하겠습니다.



## 2. 시작할 주제 - 모두의 Kaggle Tutorial : Titanic

Kaggle(kaggle.com)의 존재는 사실 14년 대학 4학년때 랩실 인턴을 지원할 때 MNIST 과제를 하느라고 잠깐 접한 적이 있었고 이후 4년여동안 마주칠 일이 없었다. 헌데 다시 시작하면서 알아보니 Kaggle로 데이터 사이언스 분야에 입문들을 많이하는 편이고, 이 또한 여러 기업, 기관, 단체등과 연계된 Competition들이 많아서 여기서 좋은 결과물을 만들어 낸다면 실제 기업 및 연구소 채용과도 연계가 심심찮게 되는 편이라고 한다. 여기서 많은 사람들이 입문 Competition으로 선택하고 현재까지도 실시간 순위를 알아 볼 수 있는. Titanic : Machine Learning from Disaster으로 진행해보려고 한다.


![Titanic_competition_main](https://github.com/ybear90/Kaggle_competition/blob/master/Titanic_Machine_Learning_from_Disaster/Titanic_1st/Titanic_competition_main.PNG)



## 3. Titanic Competition의 개요

이 대회는, 타이타닉 해상사고 당시의 승객들의 정보가 기록되어 있는 Encyclopedia Titanica의 데이터를 이용, 추후 유사한 해상 사고가 발생 했을 때 어떤 승객이 살고 죽는지를 예측해 보는 대회다. 하루에 10회정도 시도 할 수 있으며. 기한이 정해진 대회가 아니기 때문에 사실상 여러 날에 걸쳐 계속 시도해 볼 수 있는 대회다. Kaggle 메인 화면에서 Titanic을 검색하거나 그냥 바로 해당 대회가 보이는 경우가 있어 바로 링크를 타고 들어오면 된다.


![Titanic_search](https://github.com/ybear90/Kaggle_competition/blob/master/Titanic_Machine_Learning_from_Disaster/Titanic_1st/Titanic_search.PNG)



## 4. 데이터에 관한 간략한 설명

타이타닉 대회 메인화면에서 Data를 클릭을 하게 되면 데이터에 관한 간략한 설명(Overview)와 Data Dictionary(각 변수들(컬럼값)에 대한 설명)이 적혀져 있고 그리 어렵지 않은 엉어로 적혀져 있어, 중 고등학교에서 배운 수준 정도의 영어 실력이면 독해에 큰 무리가 없을거라고 생각하지만 혹시라도 영어만 보면 토가 쏠리는 사람들을 위해 간략하게 설명을 하겠다.


![Titanic_data](https://github.com/ybear90/Kaggle_competition/blob/master/Titanic_Machine_Learning_from_Disaster/Titanic_1st/Titanic_data_desc.PNG)



Data 항목에서 Data Description 항목을 들여다 보면, training set과 test set csv 파일이 있다. 즉 우리는 training data에서 우리가 필요한 feature를 골라내어, 또는 전체 feature를 다 쓰든 그 feature(해당 데이터에서 column(Sex, Pclass, Survival, Age, 등등) 들이라고 이해하면 더 쉬울 수 있다)들을 활용하여 학습을 진행한다고 보면 되고 test set csv 데이터를 열어보면 Survival 값이 빠져 있는 것을 확인 할 수 있다. Test 데이터에 Survival 내용을 채워야 한다는 것이다. 즉 Test데이터에서 Survival의 답을 맞춘다 라고 이해하시면 될 것 같다. Data파일을 모두 받아서(Kaggle 페이지에 Download All버튼 사용) 압축을 풀어보면, gender_submission이라는 알 수 없는 파일을 확인 할 수 있을 텐데, 제출파일의 샘플 본이라고 보시면 된다 Overview를 다시 살펴보면, 해당 파일은 여자는 살고 남자는 다 죽었다라고 가정하에 예측값을 넣어둔 파일이라고 친절히 적혀있다.(해당 값을 제출 해보면 0.76555 라는 적중률을 보여준다, 사소할수도 있지만 의외로 여기서 알 수 있는 점은 남자보단 여자들이 많이 살아 남았다는 것을 알 수 있다)

![Titanic_train](https://github.com/ybear90/Kaggle_competition/blob/master/Titanic_Machine_Learning_from_Disaster/Titanic_1st/Titanic_train.PNG)

![Titanic_test](https://github.com/ybear90/Kaggle_competition/blob/master/Titanic_Machine_Learning_from_Disaster/Titanic_1st/Titanic_test.PNG)

![Titanic_gender](https://github.com/ybear90/Kaggle_competition/blob/master/Titanic_Machine_Learning_from_Disaster/Titanic_1st/Titanic_gender.PNG)

보통 Kaggle 경진대회를 진행할 때, 그럴사한 column들을 골라내어 해당 raw 데이터를 그냥 아주 좋은 머신러닝 알고리즘등에 넣어 바로 계산하면 우수하게 나올 것이라고 흔히들 예상하지만, 생각보다 알고리즘의 복잡도나 우수성이 정확도에 절대적으로 영향을 끼치지 못한다. 즉 우리가 어느정도 정제가 잘 된 데이터를 사용하지 않으면, 아무리 좋은 머신러닝 알고리즘이나 툴을 쓴다 한 들 우리가 원하는 만큼의 정확도를 얻지 못한다고 생각하면 된다.

그래서 파이썬을 이용한 분석을 들어가기 앞서, 구글 스프레드시트를 사용하여 데이터 분석과 학습이 사실 어떤 사고와 논리의 연속으로 흘러가는지 간략하게 보이고 EDA(Exploratory Data Analysis)를 아주 가볍게 맛보도록 하겠다(2편에 계속...) 
