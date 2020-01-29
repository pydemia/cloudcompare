# cloudcompare
Cloud Service Comparison

## MLOps 

* [연구개요](mlops/overview/overview.md#연구개요)
  - [MLOps의 정의](mlops/overview/overview.md#mlops-정의)
  - [As-is 대비 차별점](mlops/overview/overview.md#as-is-대비-차별점-devops--data-engineering)
  - [연구범위](mlops/overview/overview.md#연구범위)
<br/>
의
* 서비스 현황
  - Vendor별 MLOps 서비스
    * AWS
      - SageMaker
    * Azure
      - [Machine Learning](mlops/azure/machine_learning/azure-ml.md#azure-machine-learning)
    * GCP
      - AI Platform
    * Databricks
      - Databricks
    * SK
      - AccuInsight+
<br/>

* 서비스 비교
  - Coverage: Inclusiveness & Exclusiveness
    * Pipelining
    * Scripting
      - Language(SDK)
      - Interfaces(Tools, IDE)
    * Versioning
      - Codes(Scripts)
      - Models
      - Workflows
    * CI/CD
    * Validating
      - Data
      - Models(Outputs)
    * Monitoring
      - System
      - Quality
  - Automaticity
  - Compatibility
    * ML Modeling
      - Tensorflow, TFX
    * Compute Resources
      - GPUs
    * Distribution
      - Docker-based
      - HDFS-based
    * Orchestration
      - Kubeflow
      - Apache Airflow
<br/>

* 서비스 예시
  - Source Type
    * Streaming
    * Batch
  - Service Type
    * Real-time
    * Batch
