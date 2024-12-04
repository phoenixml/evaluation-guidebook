# 技巧与提示
建议阅读本文之前先阅读 "Using human annotators" 页面。本文将介绍使用人工标注构建评估数据集时的一些实用建议。

## 任务设计

- **简单至上**：标注任务避免不必要的复杂。将标注员的认知负担降低到最低有助于确保他们保持专注，从而提高标注质量。

- **检查信息**：标注任务避免引入不必要的信息。仅提供任务必需的信息即可，确保不对标注员产生额外偏见。

- **内容简化**：事物的展示位置和方式差异都可能导致额外的工作量和认知负担，进而影响标注质量。例如文本和任务在同一个页面展示就能避免不必要的滚动操作，再或者多个串行任务结合时可以按顺序展示。请仔细思考你的标注工具中所有内容的展示方式，看看是否还有简化空间。

- **测试设置**：任务设计以及标注指引完成之后，确保先在少量样本上自行测试通过，再邀请整个标注团队参与，并根据需要进行迭代。

## 标注过程

- **独立标注**：为避免标注员的个人偏见在团队内传播而导致结果偏差，标注员在任务过程中应做到：不互相帮助、不借鉴答案。标注指引的对齐原则应贯穿任务始终，需使用独立数据集培训新标注员或者采用标注间一致性指标来保证整个标注团队的结果一致。

- **版本一致**：如果标注文档需要重大更新 (例如，定义或指令更改、添加或删除标签)，则要决定是否对已标注的数据进行迭代，最少也得对更改的数据集进行版本追踪，可以使用如 `guidelines-v1` 的元数据值。

## 混合人机标注

人工标注固然优势很大，但有时候标注团队会受到一些限制，如时间和资源。此时，可以部分利用模型来提高标注效率。

- **模型辅助标注**：可以使用模型的预测或生成结果作为预标注，来避免标注团队从零开始。需要注意的是这可能会引入模型偏差，例如模型的准确率较低时反而会增加标注工作量。

- **监督模型评估**：可以将模型评估 (参考 “Model as a judge” 页面) 和人工监督的方法论相结合来对结果进行验证或丢弃。需要注意引入的偏差 (参考 “人工评估的优劣势” 部分)。

- **识别边缘案例**：为使任务更加高效，可以先用一组模型初步判断，待模型意见偏差过大或正反平局时再引入人工监督员。同样需要注意引入的偏差 (参考 “人工评估的优劣势” 部分)。

## 端到端教程

如果你想完整的构建自己的评估任务，可以参考 Argilla 出品的 [实用评估教程](https://github.com/argilla-io/argilla-cookbook/tree/main/domain-eval)，文中详细介绍了使用 [Argilla](https://github.com/argilla-io/argilla/) 和 [distilabel](https://github.com/argilla-io/distilabel) 进行合成数据、人工评估等来构建特定领域的评估任务。构建完成后可以使用 [lighteval](https://github.com/huggingface/lighteval) 库进行评估。