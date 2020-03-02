# Microsoft NNi

- NNI(Neural Network Intelligence)은 아래의 기능 들의 자동화를 도와주는 강력한 도구
    - Feature Engineering
    - Neural Architecture Search
    - Hyperparameter Tuning
    - Model Comperssion
- AutoML(Automated Machine Learning)을 실험들을 관리
    - 로컬머신, 원격서버, OpenPAI, Kubeflow, K8S, 클라우드 같은 다른 학습 환경에서 최적의 신경망 구조, 하이퍼파라미터들을 찾기 위해 알고리즘을 튜닝

### NNI 기능 요약

- 학습 실험들을 관리하기 위해 Commnd Line과 Web UI 모두 제공
- 확장 가능한 API를 사용하면 AutoML 알고리즘과 학습 서비스를 커스터마이징 할 수 있음
- 새로운 사용자를 위해 최신 AutoML 알고리즘과 인기있는 학습 플랫폼을 제공

![https://github.com/microsoft/nni/raw/master/docs/img/overview.svg?sanitize=true](https://github.com/microsoft/nni/raw/master/docs/img/overview.svg?sanitize=true)

### NNI의 아키텍쳐

![https://user-images.githubusercontent.com/23273522/51816536-ed055580-2301-11e9-8ad8-605a79ee1b9a.png](https://user-images.githubusercontent.com/23273522/51816536-ed055580-2301-11e9-8ad8-605a79ee1b9a.png)

- 주요 컨셉
    - 실험(Experiment): 모델의 최적의 하이퍼파라미터를 찾는 것, 최적의 신경망을 찾는 것
    - 검색공간(Search Space): 모델 튜닝을 할 수 있는 영역(각 하이퍼파라미터의 변수 범위)
    - 구성(Configuration): 검색 공간의 인스턴스(각 하이퍼파라미터가 갖는 특정 값)
    - 트라이얼(Trial): 새로운 구성(하이퍼파라미터를 특정 신경망 구조를 설정)을 적용하는 개별적인 시도, 트라이얼 코드는 실행가능 해야 함
    - 튜너(Tuner):  다음 시도를 위한 새로운 구성을 생성하는 AutoML알고리즘, 다음 트라이얼은 이 구성과 함께 실행됨
    - 평가자(Assesor): 트라이얼의 중간 결과(주기적으로 테스트 데이터 셋의  accuracy를 평가)를 분석하여 이 트라이얼이 조기 종료되어야 하는지 아닌지 알려줌
    - 학습플랫폼(Training Plaform): 트라이얼을 실행하는 환경, 실험들의 구성에 의존적
- 실험의 실행
    - 튜너는 검색공간과 생성된 구성들을 수신
    - 구성은 학습 플랫폼에 제출, 추후 행위들은 튜너에 보고됨
    - 새로운 구성을 다시 생성하고 제출
- 실험의 과정
    - Step 1: 검색공간의 정의
    - Step 2: 모델 코드 업데이트
    - Step 3: 실험의 정의

### 설치(테스트 당시 최신 버전 v1.4)

    python -m pip install --upgrade nni

### 설치 검증

- Tensorflow 2.x  예제 이용
- 소스코드를 clone하여 예제 다운로드

        git clone -b v1.4 https://github.com/Microsoft/nni.git

- MNIST 에제를 실행

        nnictl create --config nni/examples/trials/mnist-tfv2/config.yml

- `INFO: Successfully Started experiment!` 메시지가 커맨드라인 창에 출력되면 성공적으로 시작된 것
- 표시된 Web UI URL을 웹 브라우저에 입력하여 접속

### 참고문서

- [NNI 공식문서](https://nni.readthedocs.io/en/latest/index.html)
- [Microsoft NNI Github](https://github.com/microsoft/nni)
