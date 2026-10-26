# 第一编真实学习材料：来源与核验说明

整理日期：2026-10-19。教材资料整理与只读核验由《AI考古学导论》编写组完成。以下文件来自原作者公开附件，保留原字节；本目录没有复制真实数据的课堂模拟版本。

## 1. A4 Tusayan White Ware

### 来源与许可

- 原研究：Pawlowicz, L. M., & Downum, C. E. (2021). Applications of deep learning to decorated ceramic typology and classification: A case study using Tusayan White Ware from Northeast Arizona. *Journal of Archaeological Science*, 130, 105375. [DOI: 10.1016/j.jas.2021.105375](https://doi.org/10.1016/j.jas.2021.105375)。
- 原始存档：[Zenodo record 4625156](https://zenodo.org/records/4625156)，DOI：10.5281/zenodo.4625156；作者Leszek Pawlowicz、Christian Downum；版本1.0；发布日期2021-04-25。
- 原始小包：[CNN-Models-Supplement.zip](https://zenodo.org/records/4625156/files/CNN-Models-Supplement.zip?download=1)。
- [官方API元数据](https://zenodo.org/api/records/4625156)于本轮实际读取，`metadata.license.id`为`cc-by-4.0`，`access_right`为`open`。本目录依据这项存档许可再分发原工作簿和补充说明PDF；本目录不包含期刊主文PDF。完整许可归属见[A4许可说明](a4/LICENSE-data.md)。

### 字节核验与文件名称

本轮已下载小包并解出原始附件；小包MD5与官方元数据一致。只更改本地存放路径和补充PDF文件名，文件内部内容保持原样。

| 文件 | 原包中的路径或文件名 | 字节数 | SHA-256 |
|---|---|---:|---|
| 原始小包（未在本目录重复收录） | CNN-Models-Supplement.zip | 667462 | `cd05d4d6ff43bebf7ff5de03b1d7c653c226aa5b875b089448f61048218bbe78` |
| [工作簿](a4/TWW_data.xlsx) | CNN-Models-Supplement/TWW_data.xlsx | 308518 | `abbf6c6c10ef9f2324c2fb17dc4337afdb06b8eaf0f7ce57595cc69edeaedc11` |
| [补充PDF](a4/CNN-Models-Supplement.pdf) | CNN-Models-Supplement/Supplement to Applications of Deep Learning to Decorated Ceramic Typology and Classification.pdf | 418465 | `5426290081aa72831978f1777cc0d11f0ade3f1f4404c596b4bc9190fb65bf0c` |

小包MD5：`7614e259418126ad29d4614c4fbfd64b`。本轮没有下载另一个855082252字节的`Single_Sherd_8_Type_Analyzer.zip`，未核验其中全部图像、权重和逐折文件，也未运行CNN训练或预测。

### 记录单位与原始列

工作表`2407_5_fold_Set_1_ensemble_clas`包含2407条数据记录；2407个`image_file`非空且唯一。原始字段对应如下：

| Excel列 | 原始列名 | 读表时的含义 |
|---|---|---|
| A | image_file | 图像文件名，是本表行定位依据 |
| B | Human consensus | 原作者按规则形成的专家共识标签 |
| C | CNN model prediction | 已发表工作簿记录的CNN预测类型 |
| D–G | A、B、C、D | 四名匿名专家的原始分类 |
| H | CNN confidences (on the right) | 方向提示与分隔列；其下2407格空白属于表格布局 |
| I–P | Kanaa、Wepo、Black_Mesa、Sosi、Dogoszhi、Flagstaff、Tusayan、Kayenta | 8个类型的模型置信度 |
| Q–T | Top_type、Top_confidence、Second_type、Second_confidence | 最高、次高置信度及对应类型 |

补充PDF§1.1（PDF第1–2页）说明作者从照片中裁切单片陶片图像并放到方形白底，筛选约3250张照片中的3064张供专家分类。§1.3（PDF第6–8页）说明其中2407条按作者规则形成共识标签。教材据此采用“陶片图像分类记录”的行单位。工作簿没有独立器物ID、同器关联或重复拍摄字段，图像名唯一不等于已经证明所有物理对象独立，也不等于已排除同片多图泄漏。

所有实际数据列均非空。原表中的`Indeterminate`、`Other`及带斜线的专家分类有各自的研究含义，不能作为空白删除或任意合并。模型置信度中的0是原表保存的模型数值；不能把它解释成“这种陶器在考古上不存在”。

### 共识、训练评价与结果的边界

PDF§1.3规定单一类型投票计1、分合类型计0.5；一般以2.5票或至少2票且优于其他类别形成共识。Wepo因为数量较少采用了单独规则，包括在与Kana’a或Black Mesa平票时优先Wepo。共识是研究者依据这些规则建立的标签，并非脱离分类过程的客观真值。

PDF§2.2（第10–12页）及Fig S-3（第15页）说明，2407条资料按类别分成5折，每次4折训练、1折评估；每折训练3个VGG16和3个ResNet50模型，再集成并汇总各评估折的结果。第11页步骤3还说明，每个epoch后用其称为“test”的资料检查准确率并保存最佳checkpoint。因此，这些资料参与了模型选择，不能将汇总结果介绍为另一个完全独立的最终测试集。

本轮对工作簿B、C两列逐行比较，1985/2407条字符串一致，约82.47%。如使用这一汇总，应明确称为“该工作簿中CNN预测与作者共识标签的一致率”，不称为古代类型或工匠身份的真实准确率。本轮没有重新训练模型，不能把此项只读汇总称为原论文复现。

### PDF示例与工作簿存在数值差异

本轮同时读取原工作簿，并将补充PDF第13页Table S-VI渲染核对。下列两项来自同一存档包，但数值不同：

| image_file | PDF第13页Table S-VI | 工作簿 |
|---|---|---|
| 23346_42.jpg | 预测Kanaa，最高置信度0.310 | Excel第217行：预测Wepo，最高置信度0.781 |
| 23360_02.jpg | 预测Kanaa，最高置信度0.456 | Excel第432行：预测Wepo，最高置信度0.590 |

本轮没有查到作者对差异原因的说明。教材读表练习固定使用本目录的工作簿结果，不能把PDF示例和工作簿列值混成一条新记录。PDF用于阅读作者的方法说明；两个文件均保留原样。

## 2. A6 黎凡特象牙雕刻属性

### 来源与许可

- 原研究：Gansell, A. R., van de Meent, J.-W., Zairis, S., & Wiggins, C. H. (2014). Stylistic clusters and the Syrian/South Syrian tradition of first-millennium BCE Levantine ivory carving: A machine learning approach. *Journal of Archaeological Science*, 44, 194–205. [DOI: 10.1016/j.jas.2013.11.005](https://doi.org/10.1016/j.jas.2013.11.005)。
- [作者保存的论文全文](https://www.robots.ox.ac.uk/~jwvdm/assets/pdf/gansell_jas_2014.pdf)，本目录不复制该期刊PDF。
- 官方仓库：`aneic/aneic-core`；固定commit：`43a394f3a2409f2918d38f9d3cfc6dd5472970c1`。
- [原始CSV](https://raw.githubusercontent.com/aneic/aneic-core/43a394f3a2409f2918d38f9d3cfc6dd5472970c1/data/levantine_corpus_gansell.csv)；原路径`data/levantine_corpus_gansell.csv`；本目录只更名存为[a6/levantine_ivories.csv](a6/levantine_ivories.csv)，未修改文件内部字节。
- [官方独立数据许可](https://github.com/aneic/aneic-core/blob/43a394f3a2409f2918d38f9d3cfc6dd5472970c1/data/levantine_corpus_gansell_cc_by_sa_license.txt)：Amy Gansell ©2013，CC BY-SA 3.0 Unported。原文与适用范围见[A6许可说明](a6/LICENSE-data.md)。
- 作者仓库的[图像声明](https://github.com/aneic/aneic-core/blob/43a394f3a2409f2918d38f9d3cfc6dd5472970c1/data/images_copyright.txt)另列机构和艺术家的图像来源。该CSV的CC BY-SA许可不能代替照片或绘图的具体许可。

CSV大小22846字节；Git blob SHA-1为`872b73195836fc8558f317b7be9fc9441aec30ad`；下载字节SHA-256为`d52ed8033ad7304024e207e02117d2cc1b425da8799e582858dac8a6b0b90941`。本轮保存后重新计算Git blob并与官方登记值核对一致。Git blob SHA-1与普通文件SHA-256是不同校验值。

### 记录单位与字段范围

CSV有162条数据记录、34列；`Key`非空且唯一，`Site`为地点标签。其余32列是12项候选数值属性和20项候选类别属性。原论文§2.1–2.2（PDF第4–5页，期刊pp197–198）说明研究选择女性形象，包括女首斯芬克斯、窗口女像和残片等，采用直接测量及类别记录。

一行应理解为以`Key`标识的雕刻形象观察记录，不能把162条直接称为162件完整器物。例如`52.23.2Fig1_Met`、`52.23.2_Fig2_Met`、`52.23.2._Fig3_Met`、`52.23.2_Fig4_Met`各占一行；原论文Fig5（PDF第3页，期刊p196）展示的是带四名女性形象的一件器柄或家具构件。§3.3（PDF第7页，期刊p200）也明确讨论同一器物上的多个形象。

[中文入门字段说明](a6/field-guide.md)仅解释第一编实际使用的少量字段。未重新定义全部作者变量，也未向原CSV加入中文列或自行补充单位。

### 空白、空格与0

本轮使用原始CSV逐格解析，确认：

- 严格的空字符串共1929处。
- 另有2格只含一个空格：`BM118251_C17`的`frontlength`，以及`52.23.2_Fig4_Met`的`border`。
- 将首尾空白去除后，空白计数为1931。既有汇总中的1931应按这一口径理解，不能同时说它们全是严格空字符串。
- 数值字段有一个保存为`0`的值：`1962.7Ash`的`eyefullmeanht_eyefullmeanL`。本轮没有查明该值形成原因，保留原值，不将其自动改成空白或判定为录入错误。

原论文§2.3（PDF第5页，期刊p198）指出许多雕刻残缺或表面受损，致使部分特征无法记录。这解释总体上的数据稀疏，却没有为每个空白提供具体原因。该CSV没有把“未记录”“未保存”和“不适用”逐格区分，不能为教学便利补造这些事实。`no`是原研究明确填写的类别，不能同空白或数值0互换。

## 3. 本轮整理与后续使用

文件内容层面，三份原始资料保持原字节：A4工作簿、A4补充PDF、A6 CSV。改动仅为本目录的组织和两项文件的本地名称；README、来源说明、许可说明和中文字段说明为教材编写组新增。

本轮已经完成官方小包/固定CSV取得、校验与所述只读结构核查。尚未进行实际学生试测、重新训练A4模型或对真实A6属性进行EM聚类。以后如制作清洗后的表、子集或图表，应另存派生结果，并说明来源版本、选取规则、转换步骤、统计单位和适用许可。
