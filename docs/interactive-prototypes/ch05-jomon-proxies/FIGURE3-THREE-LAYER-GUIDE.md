# 第五章绳文人口史 Figure 3：三层教学与复现指南 V1

状态：独立原型，尚未完成本地R运行/图形验收，不等于原论文全流程复现。

## 原始依据

Crema & Kobayashi (2020), *Journal of Archaeological Science* 117:105136，DOI 10.1016/j.jas.2020.105136；作者GitHub固定标签 [v.3.0](https://github.com/ercrema/jomonPhasesAndPopulation/tree/v.3.0)，commit a9608543856c3bf22fd94a682ea47e2952c6e1bd。作者Figure 3原图与绘图代码分别位于 manuscript/figures/figure3.pdf 与 figurelog.R 第93–134行。原图用Base R绘制，并非ggplot2。仓库README写CC-BY 3.0，第三方Suzuki（2006）住宅表的再分发范围仍须核查。

## 第一层：无代码（必做）

打开独立原型index.html的任务三，依次选择a住宅数量、b放射性碳测年SPD、c 1000年滚动相关。读原图，回答：三者观察单位是否相同？哪幅包含年代模拟不确定范围？为什么c的相关性不能独立证明人口增长的原因？提供静态原图和解释，即使没有R也可完成。按钮改变阅读说明，不改变作者模型结果。

## 第二层：ggplot2（选做，可运行脚本）

在本地安装R和ggplot2；获取作者固定v3.0仓库（含R_images缓存）。执行：

```bash
git clone --branch v.3.0 --depth 1 https://github.com/ercrema/jomonPhasesAndPopulation.git /tmp/jomon-v3-audit
Rscript -e 'if (!requireNamespace("ggplot2",quietly=TRUE)) install.packages("ggplot2",repos="https://cloud.r-project.org")'
Rscript interactive-prototypes/ch05-jomon-proxies/figure3-ggplot2.R /tmp/jomon-v3-audit /tmp/jomon-figure3-output
```

运行命令中的脚本路径相对于教材仓库根目录；请先切换回教材根目录再执行。脚本加载作者缓存：
- simdatesPithouses.RData：tblocks.trap（50个100年区间×模拟次数），tbs2（51个边界）；panel a均值、2.5%和97.5%分位数。
- spdRes.RData：spdDataSPD_blocks$sumblock；panel b作者已经计算的SPD。
- comp.RData：tblockRoll10.trap；panel c滚动相关均值、2.5%和97.5%分位数（忽略NA）。

脚本用相邻时间边界中点作为100年箱的ggplot x位置（例如7950、7850…3050 cal BP），x轴由老到新逆向显示；输出三个CSV、三个PNG和三面板PDF。脚本会在缓存对象缺失、区间长度不符或100年箱宽不符时停止，不能自行补造结果。

**重要：** panel a/c阴影或误差线是模拟结果的经验分位数，不可未经论证称为独立样本的频率学置信区间；panel b是作者的校正SPD，不是未经校正的CRA直方图。ggplot2重绘是**作者缓存结果的可视化复算**，不是OxCal后验的重新估计。新版ggplot的图形外观不必逐像素等同原Base R图，但数值与轴单位必须相符。

### 第二层验收

在Mac运行后检查：脚本输出PASS；三个CSV均为50行、时间中心从7950到3050 cal BP且步长100；panel a有均值及上下分位数；panel b的SPD与作者Figure 3中约5000 cal BP附近的峰值相符；panel c相关范围在[-1,1]，并与作者Figure 3的变化趋势相符。需人工并排检查原PDF和新PDF；在这一步完成前不得声称图形已验证。

## 第三层：研究级复现（进阶）

作者README与log.R给出研究级工作流：
1. 从data/c14dates.csv（2132行）读取测年记录；对CombineGroup运行outlierExcluder筛选；缓存c14data.RData保留2120行，12条差额已逐条比对。
2. 用OxCal v4.4及IntCal20/Marine20进行阶段建模，生成多种阶段内分布假设的OxCal脚本；比较agreement并进行第二轮处理。原作者README说明这一阶段耗时较长（log.R中提及约70–90小时），不作为本科必做。
3. 从data/suzuki五县CSV汇总233行Counts=9612，再通过orgTable展开为住宅记录；按阶段归属、阶段边界及阶段内不确定性进行5000次模拟。
4. 使用rcarbon构建SPD及5000次随机日历日期抽样，按100年区间汇总，计算两种代理的相关与1000年滚动相关；输出RData。
5. 运行manuscript/figures/figurelog.R复现作者Base R原图，再用本课程ggplot2脚本绘制同一缓存的教学版本。

研究级复现需要锁定R及依赖版本、OxCal执行方式、校正曲线、随机种子/随机抽样条件与输出hash。不能把作者缓存加载成功称为完整分析重跑，也不能保证跨版本随机模拟逐点一致。数据与版权核查完成前，不将全部作者原始文件复制到教材公开仓库。

## 尚待验收

ggplot2脚本尚未在用户Mac运行，真实缓存对象的维度及生成图形需本地验证。原型尚未完成公开HTTPS、Quarto嵌入、registry与第三方许可审查；第五章正式正文未修改。
