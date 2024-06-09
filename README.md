# Multi-agent-system-for-legal-judgment_
我搭建了一个争对于法律判决任务的muti_agent框架，框架包含三个角色以及一个查询资料的角色，原告律师，被告律师，法官以及一个法律字典角色（这里是使用山东大学夫子明察司法模型），法律判决预测（LJP）旨在根据案件事实描述预测案件的法律判决。法律判决通常包括法律条文、罪名和监禁期。I have constructed a multi-agent framework tailored for legal judgment task
### 话先说在前面，非常可惜，这是我23年10月至24年2月份做的工作，由于评测时间比较长，于是错过了ACL投稿日期
本来打算投EMNLP，结果看见Arxiv上5月多挂了一篇于我idea几乎完全相同的工作，这让我有点难过
这是属于同期工作，但是我测评完后没有抓紧时间写论文，所以现在相同的idea已经被挂在Arxiv了，为了显示我的确是做了相关项目，
于是我决定把code开源，这是基于多智能体的法律判决任务
## 项目背景：
法律判决预测（LJP）旨在根据案件事实描述预测案件的法律判决。法律判决通常包括法律条文、罪名和监禁期。在国家法律体系中，先例是指具有类似事实描述的先前案例，它在法律体系中占据着至关重要的位置（Guillaume，2011）,一个案例的事实描述，我们往往从三个方面对其进行总结：主观动机、客观行为和事后情况 
      在法律判决任务中，LLMs展现了卓越的广泛知识建模能力以及推理能力。然而，这些模型面临一个关键挑战，即它们在特定法律领域的专业知识理解不够准确，从而导致在法律推理任务以及判决任务中的表现不佳。此外，LLMs容易受到推理过程中逻辑偏差和幻觉的影响，可能导致不准确的结论，从而降低了在法律领域的可用性。
      为了克服这些限制，我们基于Muti-agents批判性推理框架提出了一组专业法律agents。agent具有个体的自主性，因此我们可以赋予它们行使意志、做出选择和采取行动的能力，而不是被动地对外部刺激做出反应，从而可以模仿现实中的真实角色，更好的完成任务，贴近现实生活。该框架的核心是模拟辩护律师和控诉律师的角色，他们通过对话进行批判性思考，深入挖掘和理解犯罪事实。在这个对话过程中，律师们执行一系列关键步骤，包括提取论点、分析论点以确定假设、评估相关证据、进行逻辑推理并最终得出结论。这一过程模拟了法庭上律师辩论和推理的情景，旨在纠正大模型在法律领域的知识缺陷和逻辑幻觉。
## 设计目标：
 通过模拟法庭审判过程，引入对话中的模拟辩护律师和控诉律师的互动，并引入专业法律模型--夫子·明察司法模型，从而解决LLMs在法律领域的两大主要问题：首先，大型模型在广泛知识建模方面表现卓越，但在特定法律领域的知识不足，导致在法律案例中的应用效果不佳。其次，大型模型在推理过程中容易产生幻觉，可能导致不准确的结论，影响其可用性。
      在这个框架中，模拟辩护律师和控诉律师扮演了关键角色。在他们的对话中，他们通过批判性思考深入挖掘和理解涉及犯罪事实的论点。这个过程包括提取论点、分析论点以确定假设、评估相关证据、进行逻辑推理并最终得出结论。这一系列步骤模仿了人类律师在法庭上的推理和辩论过程，并通过与专业微调出的法律模型--夫子·明察司法模型进行交互，使得能够运用专业的法律知识，进而纠正大模型在法律推理中的知识缺陷和逻辑幻觉。
      最终，法官基于对犯罪事实的深刻理解，考虑律师们的论点和证据，给出最终的判决结果。这一框架的独特之处在于提高了模型在法律领域的性能，并增加了可解释性。通过模拟人类法庭过程，这个框架使得模型更能够理解案件的复杂性，并以更加明晰的方式进行论证和推理。这为法律领域的智能系统提供了一个更可靠、深入和全面的方法。
      然而，这个框架也存在一些潜在的挑战和局限性。框架的效果可能受到律师模型性能的影响，如果模型对于批判性思考和逻辑推理的表现不佳，可能会影响整个框架的性能。因此，在使用这一框架时，需要不断优化和提升模型的能力，以确保在法律判决任务中的可行性和有效性。
## agent基础框架的选择：
现有的agent框架很多，我经过对比后选择了https://github.com/aiwaves-cn/agents框架，该框架具有以下优势：
1.可以自定义agents角色性格，职业，以及阶段性任务
2.可以清晰明了的定义阶段过程，使得代码整体逻辑非常清晰
3.可以自定义参数显示，并添加环境变量以及提示
## 主推理模型框架选择：
GPT-3.5
作为法律智能代理的主推理框架是出于对其卓越性能和适应性的认可。GPT-3.5以其庞大的1750亿个参数构建，为法律智能领域提供了强大的推理能力。本论文旨在详细阐述选择GPT-3.5的合理性，并突显其在法律智能代理构建中的独特优势。
GPT-3.5拥有广泛的知识覆盖，经过大规模互联网文本的预训练，使其在法律领域具备深厚的知识背景。这为代理提供了处理各类法律问题的丰富知识基础，包括法规、案例法等。其广泛的知识覆盖为代理提供了更全面、准确的法律分析和解决方案。
GPT-3.5的灵活性和通用性使其在不同法律任务中均表现卓越。

综合考虑GPT-3.5在上下文理解、多模态适应性、广泛知识覆盖、通用性以及持续改进等方面的优势，选择其作为法律智能代理的主推理框架是合理而明智的决策。
专业法律领域模型选择：
夫子•明察司法大模型是由山东大学、浪潮云、中国政法大学联合研发，以 ChatGLM 为大模型底座，基于海量中文无监督司法语料（包括各类判决文书、法律法规等）与有监督司法微调数据（包括法律问答、类案检索）训练的中文司法大模型。该模型支持法条检索、案例分析、三段论推理判决以及司法对话等功能，旨在为用户提供全方位、高精准的法律咨询与解答服务
在 2023 年 9 月份由上海AI实验室联合南京大学推出的大语言模型司法能力评估体系LawBench中 (见下图)，fuzi模型在法律专精模型 (Law Specific LLMs) 中 Zero-Shot 表现出色，取得了第一名，与未经法律专业知识训练的 ChatGLM 相比有了较大提升
## 前后端网页展示选择：
gradio
早期框架选择（Vue.js + Flask）：
在项目初期，我们选择使用Vue.js（前端框架）和Flask（后端框架）搭建网页应用。尽管Vue.js提供了很好的前端交互性，而Flask也具备灵活的后端处理能力，但在实现多agent对话界面时，我们面临了一些困难。
主要问题包括：
1. 状态管理： 多个agent的对话状态管理变得复杂，尤其是当涉及到异步交互和动态界面更新时。
2. 实时性： 对话的实时性要求较高，需要频繁地更新页面内容以反映多个agent之间的动态交互。
3. 性能问题： 随着对话数量和复杂性的增加，前端性能逐渐变得不尽如人意，导致页面加载和响应速度下降。
基于以上问题，我们决定寻找更适合多agent对话界面这一需求的解决方案。在经过一番调研后，我们选择了Gradio框架。
## Gradio介绍：
Gradio是一个开源的Python库，专注于简化机器学习模型的部署和构建交互性应用。它提供了直观的界面，使得用户能够轻松创建、测试和共享模型。Gradio支持各种类型的输入（文本、图像、音频等）和输出，使其成为处理多agent对话场景的理想选择。
Gradio的优势：
1. 交互性强： Gradio使用户可以快速构建具有高度交互性的应用，适用于我们的多agent对话界面。
2. 简单易用：只需要几行代码就可以创建界面。无需前端开发经验。
3. 支持丰富的交互组件：如滑块、单选框、文本框等。可以快速构建复杂的界面。
通过使用Gradio框架，我们成功解决了在前期框架中遇到的多agent对话界面的问题，提高了系统的实时性和性能，为用户提供了更好的交互体验。
# 系统设计：
## 初版系统设计
![GitHub Logo](https://raw.githubusercontent.com/your-username/your-repo/master/images/your-image.png](https://github.com/ZhouZiai/Multi-agent-system-for-legal-judgment_/blob/master/figure1.png)
## 最终设计图初稿（我1月画的图，结果和人5月挂在Arxiv上的论文的图都相似，彻底绝望了，嘤嘤嘤）
![GitHub Logo](https://raw.githubusercontent.com/your-username/your-repo/master/images/your-image.png](https://github.com/ZhouZiai/Multi-agent-system-for-legal-judgment_/blob/master/figure2.png)
# 使用效果
![GitHub Logo](https://raw.githubusercontent.com/your-username/your-repo/master/images/your-image.png](https://github.com/ZhouZiai/Multi-agent-system-for-legal-judgment_/blob/master/figure3.png)
![GitHub Logo](https://raw.githubusercontent.com/your-username/your-repo/master/images/your-image.png](https://github.com/ZhouZiai/Multi-agent-system-for-legal-judgment_/blob/master/figure4.png)
![GitHub Logo](https://raw.githubusercontent.com/your-username/your-repo/master/images/your-image.png](https://github.com/ZhouZiai/Multi-agent-system-for-legal-judgment_/blob/master/figure5.png)
![GitHub Logo](https://raw.githubusercontent.com/your-username/your-repo/master/images/your-image.png](https://github.com/ZhouZiai/Multi-agent-system-for-legal-judgment_/blob/master/figure6.png)




