# Azure Machine Learning

[Documentation](https://azure.microsoft.com/ko-kr/services/machine-learning/)


* __Azure Maching Learning__: ML 모델의 학습, 배포, 자동화, 관리 및 추적에 사용할 수 있는 클라우드 기반 환경

* Tools
  - AzureML Designer(Preview, GUI): Drag & Drop
  - Jupyter Notebook (& Python AzureML SDK)
  - R AzureML SDK
  - *__Automated ML__*
  - VSCode Extension
  - AzureML CLI
  - [MLFlow(Metric Tracking & Model Deploying)](https://docs.microsoft.com/ko-kr/azure/machine-learning/how-to-use-mlflow): 
    - machine learning 실험의 수명 주기를 관리 하기 위한 오픈 소스 라이브러리.
    - MLFlow 추적: 실험 환경에 상관 없이 (원격 계산 대상, 컴퓨터에서 로컬로 또는 Azure Databricks 클러스터에서) 학습 실행 메트릭과 모델 아티팩트를 기록 하 고 추적 하는 MLflow의 구성 요소
  - [End-to-End Workflow Pipeline](https://www.kubeflow.org/docs/azure/)
    - Deployment
      * Instructions for deploying Kubeflow on Azure

    - End-to-End Pipeline Example on Azure
      * An end-to-end guide to creating a pipeline in Azure that can train, register, and   deploy an ML model that can recognize the difference between tacos and burritos

    - Access Control for Azure Deployment
      * Restrict access of your deployment to specified IP addresses

    - Troubleshooting Deployments on Azure AKS
      * Help diagnose and fix issues you may encounter in your Kubeflow deployment




### 비교: Azure Machine Learning과 Machine Learning Studio(클래식)

| | Azure Machine Learning 디자이너 | Studio(클래식) |
| :--: | :----| :--- |
| | 디자이너는 미리 보기 상태이며 Azure Machine Learning은 GA입니다. | GA(일반 공급) |
| Drag & Drop 인터페이스 | yes | yes |
| 실험 | 컴퓨팅 대상으로 크기 조정 | 크기 조정(10GB 학습 데이터 제한) |
인터페이스용 모듈 | [인기 있는 많은 모듈](https://docs.microsoft.com/ko-kr/azure/machine-learning/algorithm-module-reference/module-reference) | 다수 |
컴퓨팅 대상 Training | AML 컴퓨팅(GPU/CPU) | 전용 컴퓨팅 대상, CPU만 해당 |
컴퓨팅 대상 Inference | 실시간 유추를 위한 Azure Kubernetes Service<br/>일괄 처리 유추를 위한 AML 계산 | 전용 웹 서비스 형식, 사용자 지정 불가능 |
| ML 파이프라인 | 파이프라인 제작<br/>게시된 파이프라인<br/>파이프라인 엔드포인트<br/>[ML 파이프라인에 대해 자세히 알아보기](https://docs.microsoft.com/ko-kr/azure/machine-learning/concept-ml-pipelines) | 지원되지 않음 |
| ML Ops | 구성 가능한 배포, 모델 및 파이프라인 버전 관리 | 기본 모델 관리 및 배포 |
| 모델 | 학습 작업에 따라 다양한 표준 형식 | 독점적이며 이식 불가능 형식 |
| 자동화된 모델 교육 | 아직 ~~디자이너에서는 미지원~~<br/>인터페이스 및 SDK에서 지원 | 예 |

