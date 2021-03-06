+++
title = "Datacouncil.ai Conference Notes"
author = ["Jethro Kuan"]
lastmod = 2020-07-08T14:54:17+08:00
draft = false
+++

tags
: [Data Science]({{< relref "data_science" >}})

## Taking recommendation technology to the masses - Le Zhang (Microsoft) {#taking-recommendation-technology-to-the-masses-le-zhang--microsoft}

Challenges:

1.  Limited Resource
2.  Fragmented solutions

<https://github.com/Microsoft/recommenders> contains modular functions
for model creation, data manipulation, evaluation etc.

- SVD, SAR, ALS, NCF, Wide&Deep, xDeepFM, DKN etc.

### Collaborative Filtering {#collaborative-filtering}

Memory based method:

1.  Microsoft Smart Adaptive Recommendation (SAR) algorithm

Model based methods

1.  Matrix factorization methods

    1.  Singular Value decomposition
    2.  Spark ALS

2.  Neural network-based methods
    1.  Restricted Boltzmann Machine (RBM)
    2.  Neural Collaborative Filtering (NCF)

### [SAR](https://github.com/microsoft/Product-Recommendations/blob/master/doc/sar.md) ([ipynb](https://github.com/microsoft/recommenders/blob/master/notebooks/02%5Fmodel/sar%5Fdeep%5Fdive.ipynb)) {#sar--ipynb}

- Item-to-item similarity matrix via co-occurence
- User-to-item affinity matrix via co-occurence of user-item interactions
  - weighted by interaction type and time decay:

\begin{equation}

\end{equation}

- Free from machine learning and feature collection
- Explainable results

### Neural Collaborative Filtering (NCF) {#neural-collaborative-filtering--ncf}

- Neural network based architecture to model latent features
- Generalization of MF based method

### Content-based Filtering {#content-based-filtering}

- "Content" can be user/item features, review comments, knowledge
  graph etc.
- Mitigates cold-start issue
- Feature vector can be highly sparse

e.g. Factorization machines

\begin{equation}
\hat{y}(\mathbf{x}) = w_0 + \sum\_{i=1}^{n} w_i x_i +
\sum\_{i=1}^{n}\sum\_{j=i+1}^n \langle v_i, v_j \rangle x_i x_j
\end{equation}

<!--list-separator-->

- <span class="org-todo todo TODO">TODO</span> xDeepFM

  ([Guo et al., n.d.](#org3f1dd65); [Lian et al., n.d.](#org5050647))

### <span class="org-todo todo TODO">TODO</span> Deep Knowledge-aware Network ([Wang et al., n.d.](#org1eaf79d)) {#deep-knowledge-aware-network--wang-et-al-dot-n-dot-d-dot--org1eaf79d}

Multi-channel word-entity aligned knowledge aware CNN

### Operationalizing a real-time recommender {#operationalizing-a-real-time-recommender}

- containerize model serving, use Kubernetes to autoscale

## Scaling Data Science Teams - Miguel Rios (Twitter) {#scaling-data-science-teams-miguel-rios--twitter}

- 9-year longitudinal study of scaling data science at Twitter

2 models of DS teams in engineering-driven organizations:

embedded model
: data scientists part of a smaller team, with other
engineers - Pros: - Dedicated data science resourcing - Alignment between DS and the rest of the team - One roadmap, fewer dependencies - Data science has a more natural "seat at the table" - Cons: - Rigid resourcing (harder to move DS between teams) - Barriers for collaboration between data scientists - Manager may not have domain knowledge (typically an EM) - Risk of Data Science being a support or service to eng. team

centralized model
: data scientists manageed by a data science
manager, supporting the product teams - Pros: - Data scientists working together (collaboration and knowledge sharing) - DS manager has domain knowledge (between career dev) - Resources can be rebalanced to meet customer demand - Advocacy for better and consistent tech (tooling, datasets,
etc.) - Cons: - Coordiantion between teams (DS and stakeholder) becomes more complicated - In eng. centric orgs the DS teams need to influence org roadmap - Risk of data science work not being aligned with product - Company needs to support one more function

Best of both worlds: centralized org with embedded teams

E.g.

- Growth Eng (with centralized DS)
- Product Eng (with centralized DS)
- Health Eng (with centralized DS)

- Centralized proceses, common resources

Challenges:

1.  Everyone has at least 2 teams - centralized DS team, and part of the
    product team
    1.  Risk of meeting and planning overload
    2.  Which is their main team?
2.  Risk of mismatch of expectation between DS leadership and product leadership

How to scale this hybrid org structure to ~100 Data Scientists?

~ Create more layers of abstraction:

- Split teams into pillars

"A product as a system":

```text
Growth DS -> Product DS -> Revenue Science
                ^^^
Insights, metrics, data enigneering, data visualization
```

Twitter organizes into:

- Growth
- Product
- Health
- Foundational DS

team charters
Swimlanes - clear differentiation between teams
Working agreement - what to expect from other teams? (e.g.
interactions between data engineering & notifications ds team)

- How does the data eng team receive requests?
- What is the SLA of a dataset request?
- What would be the ownership structure for the request?
- On what basis this request will be prioritized?

**Create clear communication channels**

- Have team meetings at all levels
- Have recurrent sessions to review ongoing projects
- Have fun with each other - quarterly offsites and other activities

**Build and strengthen your leadership team**

- Leadership team is their **first team**
- Have staff meeting, and keep an open standing agenda
- Do leadership offsites and working sessions (twitter does it monthly
  on a specific topic)
- Make this reponsible for managing your org's relationship with
  stakeholders

TLDR: align teams with objectives, build structures of your teams:
team charters, working agreements, swimlanes, and strong leadership
team

### Questions: Thoughts on self-servicing (end-to-end) data scientists {#questions-thoughts-on-self-servicing--end-to-end--data-scientists}

- Moving away from end-to-end

### Question: How to bridge gap in understanding between data eng and data scientists {#question-how-to-bridge-gap-in-understanding-between-data-eng-and-data-scientists}

- strong overlap in skill set between data eng and scientists e.g.
  engineers are taught to build data pipelines early when joining
  Twitter
- job of the DS manager

## Argo: Kubernetes Native Workflows and Pipelines - Greg Roodt, Canva {#argo-kubernetes-native-workflows-and-pipelines-greg-roodt-canva}

[Github project](https://github.com/argoproj/argo)

- Similar to airflow
- runs on top of kubernetes

[Machine Learning as Code - Youtube](https://www.youtube.com/watch?v=VXrGp5er1ZE&t=0s&index=135&list=PLj6h78yzYM2PZf9eA7bhWnIh%5FmK1vyOfU) - How Kubeflow uses Argo Workflows
as its core workflow engine and Argo CD to declaratively deploy ML
pipelines and models.

Argo's DAG UI looks nice!

## Data Architecture 101 for Your Business - Bence Faludi, Independent Consultant {#data-architecture-101-for-your-business-bence-faludi-independent-consultant}

{{< figure src="/ox-hugo/screenshot_2019-07-17_12-06-32.png" >}}

- How to handle unclean data?
- How quick will the transforms be?

- Transitioning into a data-driven company
  - Centralized existing datasets

### Data Collection {#data-collection}

- ownership and access of data
- near-real time raw data : access to unfiltered data in minutes
- no data sampling : ensure access to full dataset
- ad blockers : responsible for many lost events
- personal identification information : turn off PII scraping
- data model : custom events can be sent in nested format
- SDKs with persistent layer: collected logs stored on the offline
  device

### Storage and Flow {#storage-and-flow}

- schedulable pipelines with dependencies
  - notifications, SLAs, extendibility
- Collected data transformation
- Raw-level data stored on the storage, accessible on query engine

### Database Query Engine {#database-query-engine}

- read benchmarks
- look at distributed query engines
- star schema better for analytics
- flat truth tables
- store aggregations as cubes

### Visualization {#visualization}

- self-hosted vs hosted
- native SQL execution
- interactive query builder

E.g. stack Kinesis Data Firehose, S3, Airflow, EMR-Presto (Athena for
large jobs), [Apache Superset](https://superset.incubator.apache.org/)

## {#}

## Bibliography {#bibliography}

<a id="org3f1dd65"></a>Guo, Huifeng, Ruiming Tang, Yunming Ye, Zhenguo Li, and Xiuqiang He. n.d. “Deepfm: A Factorization-Machine Based Neural Network for Ctr Prediction.” <http://arxiv.org/abs/1703.04247v1>.

<a id="org5050647"></a>Lian, Jianxun, Xiaohuan Zhou, Fuzheng Zhang, Zhongxia Chen, Xing Xie, and Guangzhong Sun. n.d. “Xdeepfm: Combining Explicit and Implicit Feature Interactions for Recommender Systems.” <http://arxiv.org/abs/1803.05170v3>.

<a id="org1eaf79d"></a>Wang, Hongwei, Fuzheng Zhang, Xing Xie, and Minyi Guo. n.d. “Dkn: Deep Knowledge-Aware Network for News Recommendation.” <http://arxiv.org/abs/1801.08284v2>.
