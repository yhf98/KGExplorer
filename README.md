

<p align="center">
  <br/>
  <img width="300px" src="./asset/logo.png"/>
  <br>&emsp; &emsp; 本项目旨在结合知识图谱技术和先进的大语言模型，构建一个智能问答系统。它将利用知识图谱的结构化信息和大语言模型的自然语言理解能力，深入理解用户提出的问题，并提供准确、有逻辑性的回答。通过整合两大技术，我们将构建一个功能强大、垂直领域适用的智能问答系统，为用户提供卓越的体验。

### 0 项目模型框架

- 知识图谱是一种有向图，将实体、属性和它们之间的关系表示为节点和边。它能够为系统提供结构化的知识，从而提高问题理解的准确性。知识图谱的建设和维护是项目成功的基础。要考虑如何收集、整理、更新和扩展知识图谱以满足用户需求。
- 大语言模型具备出色的自然语言理解能力，能够识别和理解用户提出的问题，包括复杂的句法和语义结构。这有助于确保系统准确理解用户的意图。大语言模型为项目提供了强大的自然语言处理能力，使系统能够深入理解用户问题并生成高质量的答案，从而实现了一个智能问答系统的关键功能。

​	**模型框架图如下所示**：

<img src=".\asset\模型框架.png" width="600px" align="center" />

### 1 数据&模型

#### 1.1 数据

**知识图谱三元组:**三元组是知识图谱的一种通用表示方式，即 $G \in (E,R, S)$ ，其中 $E= \{e_1 ,e_2 ,...,e_{|E|} \}$ 是知识库中的实体集合，共包含 $| E |$ 种不同实体； $R= \{r_1 ,r_2 ,...,r_{|R|} \}$ 是知识库中的关系集合，共包含 $| R |$ 种不同关系； $S \subseteq E \times R\times E$  代表知识库中的三元组集合。

*具体实现:*

1. 实体-关系-实体
2. 实体-属性-属性值

**知识图谱数据**：[[Data]](data/medical/medical.json) 需要导入neo4j图数据库，导入[代码](./build/build_kg)

#### 1.2 模型

本项目根据[bert-base-chinese](https://huggingface.co/bert-base-chinese)模型进行微调分别得到两个模型：**命名实体识别（NER）**和**意图检测识别（IR）**

对应模型框架图中的意图检测识别（Intent Recoginition）与命名实体识别（Slot Filling）

- **数据集**：[命名实体识别模型数据集](./data/chinese_biomedical_NER_dataset) 、 [意图检测识别模型数据集](./data/intent-recognition-biomedical)

- **模型训练代码：**[命名实体识别模型](./build/ner_model.py)、 [意图检测识别模型](./build/intent_dection_model.py)

### 2 WEB设计

构建一个智能问答系统，结合知识图谱技术和大语言模型，需要一个综合性的前后端解决方案。本项目使用Python的Flask框架来构建后端，同时使用Vue.js来构建前端。以下是一个基本的项目设计方案：

#### 2.1 后端设计（Flask）

1. **选择技术栈**：
   - 使用Flask作为后端框架，因为它轻量级且易于扩展。
   - 使用Gunicorn或uWSGI作为应用服务器来提高性能和并发处理能力。
   - 使用Python的Flask-CORS扩展来处理跨域请求，以允许前端与后端通信。
2. **构建RESTful API**：
   - 设计API端点，包括用户认证、问题检索、答案生成等。
   - 使用Flask-RESTful扩展来帮助构建API。
3. **知识图谱集成**：
   - 集成知识图谱技术，例如使用RDF数据库或图数据库存储和检索结构化数据。
   - 编写查询接口，使前端可以向知识图谱查询相关信息。
4. **大语言模型集成**：
   - 集成先进的大语言模型，例如GPT-4（如果可用）或其他开源的NLP模型。
   - 创建一个接口，将用户问题传递给模型并获取生成的答案。

#### 2.2 前端设计（Vue）

1. **选择技术栈**：
   - 使用Vue.js作为前端框架，因为它提供了灵活性和可维护性。
   - 使用Vue Router来处理前端路由。
2. **用户界面设计**：
   - 设计用户友好的界面，包括搜索框、问题显示区域、答案区域等。
   - 使用Vue组件来组织UI元素，以便重用和维护。
3. **与后端通信**：
   - 使用Axios或Fetch API来与后端的RESTful API进行通信。
   - 实现错误处理和加载指示器，以提供良好的用户体验。
4. **实时搜索**：
   - 集成实时搜索功能，使用户能够在输入问题时动态获取建议。
   - 使用Vue的双向绑定来实现实时更新。
5. **用户认证**：
   - 如果需要用户认证，实施用户登录和注册功能。
   - 使用Vue Router来管理用户的身份验证状态。
