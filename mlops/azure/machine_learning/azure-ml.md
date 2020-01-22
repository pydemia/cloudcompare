# Azure Machine Learning
<img src="../../images/azure-ml/azure-ml-icon.png" alt="azure-ml-icon"
	title="mlops-intersection" width="10%" height="10%" />
[*Official Documentation HERE*](https://azure.microsoft.com/ko-kr/services/machine-learning/)


## Azure AI Ecosystem

![Azure AI Eco](../../images/azure-ml/azure-ai-eco.png "azure-ai-eco")


![Azure ML Model Workflow](../../images/azure-ml/azure-ml-model-workflow.png "azure-ml-model-workflow")

![Azure ML Workspace](../../images/azure-ml/azure-ml-workspace-run_an_experiment_as_a_pipeline.png "azure-ml-workspace")

![Azure AI Eco](../../images/azure-ml/azure-mlops-architecture.png "azure-ml-architecture")

### Architecture Flow
#### Train Model
Data Scientist writes/updates the code and push it to git repo. This triggers the Azure DevOps build pipeline (continuous integration).

Once the Azure DevOps build pipeline is triggered, it performs code quality checks, data sanity tests, unit tests, builds an Azure ML Pipeline and publishes it in an Azure ML Service Workspace.

The Azure ML Pipeline is triggered once the Azure DevOps build pipeline completes. All the tasks in this pipeline runs on Azure ML Compute. Following are the tasks in this pipeline:

Train Model task executes model training script on Azure ML Compute. It outputs a model file which is stored in the run history.

Evaluate Model task evaluates the performance of the newly trained model with the model in production. If the new model performs better than the production model, the following steps are executed. If not, they will be skipped.

Register Model task takes the improved model and registers it with the Azure ML Model registry. This allows us to version control it.

#### Deploy Model
Once you have registered your ML model, you can use Azure ML + Azure DevOps to deploy it.

Azure DevOps release pipeline packages the new model along with the scoring file and its python dependencies into a docker image and pushes it to Azure Container Registry. This image is used to deploy the model as web service across QA and Prod environments. The QA environment is running on top of Azure Container Instances (ACI) and the Prod environment is built with Azure Kubernetes Service (AKS).

* __Azure Maching Learning__: ML 모델의 학습, 배포, 자동화, 관리 및 추적에 사용할 수 있는 클라우드 기반 환경

1. Build
1. Deploy

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
<br/>

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

#### 다른 서비스와 통합
Azure Machine Learning은 Azure 플랫폼의 다른 서비스와 함께 작동하며, Git 및 MLFlow 같은 오픈 소스 도구와 통합됩니다.
* **Azure Kubernetes Service, Azure Container Instances, Azure Databricks, * Azure Data Lake Analytics, Azure HDInsight** 등의 컴퓨팅 대상: [컴퓨팅 대상이란?](https://docs.microsoft.com/ko-kr/azure/machine-learning/concept-compute-target)
* **Azure Event Grid**: [Azure Machine Learning 이벤트 사용](https://docs.microsoft.com/ko-kr/azure/machine-learning/concept-event-grid-integration)
* **Azure Monitor**: [Azure Machine Learning 모니터링](https://docs.microsoft.com/ko-kr/azure/machine-learning/monitor-azure-machine-learning)
* **Azure Storage** 계정, **Azure Data Lake Storage, Azure SQL Database, Azure Database for PostgreSQL, Azure Open Datasets** 등의 데이터 저장소: [Azure 스토리지 서비스에서 데이터 액세스](https://docs.microsoft.com/ko-kr/azure/machine-learning/how-to-access-data) 및 [Azure Open Datasets](https://docs.microsoft.com/ko-kr/azure/machine-learning/how-to-create-register-datasets#create-datasets-with-azure-open-datasets)로 데이터 세트 만들기
* **Azure Virtual Network**: [가상 네트워크에서 실험 및 유추 보호](https://docs.microsoft.com/ko-kr/azure/machine-learning/how-to-enable-virtual-network)
* **Azure Pipelines**: [기계 학습 모델의 학습 및 배포](https://docs.microsoft.com/ko-kr/azure/devops/pipelines/targets/azure-machine-learning)
* **Git** Repository Log: [Git 통합](https://docs.microsoft.com/ko-kr/azure/machine-learning/concept-train-model-git-integration)
* **MLFlow**: [MLflow를 사용하여 메트릭을 추적하고 모델 배포](https://docs.microsoft.com/ko-kr/azure/machine-learning/how-to-use-mlflow)
* **Kubeflow**: [엔드투엔드 워크플로 파이프라인 빌드](https://www.kubeflow.org/docs/azure/)


### ML Pipeline

#### 수행작업

| 파이프라인 | 수행작업 | 정식 파이프
| :------ | :-------- | :------|
| **Azure Machine Learning**	| ML Scenario Template으로 재사용 가능한 ML Workflow 정의 | 데이터 -> 모델 |
| **Azure Data Factory** | 데이터 이동, 변환, 제어 작업을 그룹화 | 데이터 -> 데이터 |
| **Azure Pipelines**	| 모든 플랫폼/클라우드에 Appl.의 지속적 통합 및 전달	| 코드 -> 앱/서비스 |

#### 주요장점

| 장점 | Description |
|:--- | :------|
| **무인 실행** | 무인 방식으로 **병렬/순차 실행 및 예약**으로 안정성 확보 |
| **다른 유형의 계산** | **개별 Pipeline**을 사용하여 다양한 Compute Resource, Storage 활용 가능<br/> (**HDInsight**, **GPU 데이터 과학 Vm**, **Databricks** 등) |
| **재사용 가능** | **Pipeline Template**으로 시나리오 관리(재학습 ,Batch-scoring 등)<br/>REST 호출로 외부 시스템에 게시된 Pipeline 트리거 |
| **추적 및 버전 관리** | **Pipelines SDK**로 Data Source, Input, Output 이름과 버전 지정하여 관리 자동화<br/> 생산성 향상을 위해 스크립트/데이터로 구분하여 관리 가능 |
| **성과** | 작업항목 모듈화로 소프트웨어 품질 향상 |
| **협업** | ML Design 시 공동 작업 수행 편의성 증대 |

### 주요 Concepts

| 구분 | 설명 |
| :-- | :-- |
| **Workspace(작업 영역)** | 최상위 Resource, Azure ML 작업의 기본 Layer |
| **Environments(환경)** | ML Scripts를 위한 환경변수, 패키지, S/W 설정 지정 |
| **Data(데이터)** | ML Data 관리 통합 솔루션(Azure Storage -> ML Dataset)  |
| **Model Training** | SDK,CLI,GUI로 학습 작업 컨트롤 | 
| **ML Pipelines** |
| **Model Management(MLOps)** | Pipelining, 등록, 패키징, 배포, 모니터링, 업데이트 관리 |
| **해석** | `Python Explainers`를 활용하여 SHAP 방식 해석력 제공 |
| **Automated ML** | End-to-End 자동화 ML 서비스 |
| **Compute Instance** | `Jupyter(Python, R)`, `RStudio` 기반 노트북 환경 제공 |
| **Compute Target** | Script 실행, 서비스 Hosting 리소스/환경: 분산처리, IoT 지원 |
| **ONNX(Open Neural Network Exchange)** | Inference Optimization |  |

### Workspace(작업 영역)

* Azure ML의 최상위 Resource
* Azure ML에서 쓰이는 모든 Artifact 사용 가능한 중앙 집중식 환경
* 학습 실행 기록 유지-Logs, Metrics, Outputs, Snapshots of Scripts-최고 성능 모델 선택 가능

[Workspace 분류 체계]
![Azure ML Model Workspace](../../images/azure-ml/azure-machine-learning-taxonomy.png "azure-ml-model-workspace")

* 필요 시 외부 Azure Compute Instance 포함 가능
* User Roles: Workspace 공유
* Compute Target: Experiments 실행