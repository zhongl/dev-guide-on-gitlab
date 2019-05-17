[TOC]

# Gitlab协同开发指南

为**高效**交付**优质**的产品或项目, 本文基于[Gitlab](https://about.gitlab.com)的核心功能, 约定若干**最佳实践**(含 **目的**), 以**指引**团队协同开发.


> **注意**
> 
> 若最佳实践的效果并不理想, 请参阅者依照 **目的** 酌情调整, 并改良实践. 目的位于标题下方的引文, 如:
> ## 最佳实践
> > 目的
 
## Issues

> **达成交付共识**

[![](http://www.projectclub.com.tw/images/article/Project%20Skill/lifesee/h.png)
](https://dotblogs.com.tw/jimmyyu/2009/09/26/10779)

上图形象的表明了交付团队不同角色之间的 **认知偏差**, 最终导致的 **交付偏差**, 这也是交付风险最大的来源. 不幸的是, **认知偏差** 是不可避免的, 我们能为之努力的是不断 **缩小偏差** 的范围.

**减少信息传递的次数, 最好能统一信息获取的来源, 是缩小偏差最有效的手段之一**. 使用 **Issues** 来记录, 讨论, 传递信息, 便可实现这一手段. 

> **为什么不用邮件或者钉钉?**
> 
> 这二者都是非常成熟和优秀的即时沟通协作工具, **Issues** 与二者并不冲突, 往往还需要二者作为即时性沟通的有力补充.
> 
> **Issues** 有二者不具备的特质:
> 1. 信息以产品或项目为核心上下文组织, 利于 **聚焦** 与 **检索**;
> 2. 沉淀的信息可以很容易的被新人所共享, 利于**经验传播**;
> 3. 无缝结合 **看板** 工具, 方便全局 **跟踪** 和 **调度** , 利于 **把控交付风险**.

同时, 围绕以下三个问题在 Issue 中讨论并明确答案, 最大程度上让 **结果靠近期望**: 

1. **为何要做?** 
1. **如何去做?**
1. **何叫做好?**

### Issue 模版参考

```markdown
# 背景

> 回答为何要做, 不做会有怎样的问题.

# 方案

> 回答如何去做, 提供参考思路或模型.

# 验证

> 回答何叫做好, 验证结果满足预期的标准有哪些, 是什么.
```

> Open 一个 Issue 必须要回答第一个问题!

### Lables

**Label** 的含义很多样, 比如 **看板** 里会用来标识交付状态, 亦或是某种事务类型, 如:

- Feature
- Bug
- Specification
- Enhancement

也正是如此, 它可以灵活组合, 让 Issue 具备多个维度的特征, 易于分类, 检索, 统计, 可视.

## Board(看板)

> **监控交付进度**

```
|  OPEN   |   TO DO  |  DOING   |  CLOSED  |
——————————+——————————+——————————+——————————+
|  [***]  |   [***]  |   [***]  |  [***]   |
|         |   [***]  |          |          |
```

Issue 被分为四种基本状态:

- **Open** - 任何**问题**, **想法**, **建议**等不确定的, 需要讨论的, 都可以 **Open** 一个Issue 并邀请相关人员参与讨论, 并明确是否要进入 **To Do** 参与到交付中;
- **To Do** - 一旦明确 Issue 需要交付, 则必须 **指明具体人** 来负责, 并由负责人根据优先级和自身工作负荷来选择进入 **Doing**;
- **Doing** - 开始实施的 Issue 必须指定明确的 **Due Date**, 这是**交付进度重要参考基准**;
- **Closed** - Issue 实施完成后, 由负责人指派给发起人, 由发起人验证交付是否满足预期, 是则关闭, 反之继续转交给负责人修正. 其它都可能因为 **放弃** 而被关闭, 即便被关闭, 也可以在需要的时候被**重新开启**.

![issue's  states](http://www.plantuml.com/plantuml/proxy?src=https://raw.githubusercontent.com/zhongl/dev-guide-on-gitlab/master/.plantuml/issue_states.txt)

> **新增状态**
> 
> Issues 原生只有 **Open** 和 **Closed** 两种状态, **To Do** 和 **Doing** 是通过 **Label** 扩展出来的, 方便直观的一览 Issues 的分布态势, 发现交付**瓶颈**, 预防进度风险. 如有需要可以扩展出更多的状态, 如 **Verifying**. 


## Milestone

> 确立交付节奏

[![](https://i1.wp.com/semi-rad.com/wp-content/uploads/2018/05/People_Pleasers_Plan_For_Climbing_A_Mountain.jpg?fit=1024%2C520&ssl=1)](https://www.outsideonline.com/2314906/people-pleasers-plan-climbing-mountain)

一蹴而就的交付, 往往是事与愿违的. 现实中登顶一座山峰, 看似是不可完成的任务, 若能将行程根据天气变幻, 难度系数, 体力分配等等因素, 合理划分为若干阶段, 每个阶段都设定可以触及目标, 在逐一达成之后, 登顶也就变为可能. 

交付亦是如此, 眼前众多的 Issues 在有限的时间里, 能否完成心里是没底. 不妨静心下来梳理它们之间的关系, 按照**优先级**, **最小可用度**, **依赖关系**等归类到若干 **Milestones** 里, 然后逐一击破. 比如:

- `v0.1` - 交付最小集成联通版本;
- `v0.2` - 交付最小功能集可测版本;
- `v0.x` - 交付最小可体验试用版本;
- `v1.0` - 交付最小可实用版本, 而后持续演进.

实施细节请注意:

- 每个 **Milestone** 的时间周期固定, 如**一周**;
- 每个 **Issue** 的 **Due Date** 不要超过一个 **Milestone** 时间周期;
- 若超过, 则建议在**可用程度**上拆分为多个 Issue, 分派到多个 **Milestone** 中, 递进交付.

## Fork & Merge Development Cycle

> 保证交付质量

![fork and merge](http://www.plantuml.com/plantuml/proxy?src=https://raw.githubusercontent.com/zhongl/dev-guide-on-gitlab/9ddbad780c09b7a40df007ca76624185b8f8aac5/.plantuml/fork_merge.txt)

> 上图语法参考 http://plantuml.com/zh/sequence-diagram .

### Initialization

1. **TechLeader** 在项目组(**G**)中创建工程代码仓库 **A**;
2. **TechLeader** 建立[最小可迭代交付](https://zhongl.github.io/2019/04/15/iterated-delivery/)的基线版本;
3. **QAer** 确保基线版本 **CICD** 可用.

> **QAer** 是质量保证(Quality Assurance)工程师的简称.

### Forking[^1] & Developing

1. **Developer** 通过 **fork** 镜像仓库 **A** 到自己名下;
2. **Developer** 按照一个特定的 **Issue** 要求进行开发实现, 直到可以合并到原始仓库 **A**;

### Merge Request[^2]

1. **Developer** 向仓库 **A** 发起 **Merge Request**;
2. **Pipeline**[^3] 自动执行正确性检查, 包括但不限于:
    1. 编译构建代码, 或静态走查代码; 
    2. 运行单元测试, 并获取测试覆盖.
3. 一旦检查不通过, 则需要 **Developer** 进行修复, 直到检查通过;
4. 检查通过后, **TechLeader** 或其他 **Developer** 进行审查代码变更, 提出改进商议(**Discussion**)[^4];
5. **Developer** 视情况解决(**Resolve**)[^5], 直到 **TechLeader** 或其他 **Developer** 评论回复**LGTM**;
6. 最终, 由 **TechLeader** 执行 **merge** 操作.

> **LGTM** 是 **Look Good To Me** 缩写, 普遍被用于 [Github](https://github.com) 的开源协作项目中, 表示项目的维护者认同外部贡献者提交的 **Pull Request** .

### Integration

1. **QAer** 创建一个新的 `tag`, 继而触发
2. **Pipeline** 对合并后的代码进行 **deploy** 及 **verify** ;
3. 一旦发现异常, **QAer** 可以**选择性 Revert**[^6],  并向 **Merge Request** 所属的 **Developer** 指派 **bug issue**, **Developer** 进行修复并发起一轮新的 **Merge Request**;
4. 若一切如预期, **QAer** 可以选择对最新版本新建一个 **Tag**, 视为**Release Candidate**.

### Issue Vs Merge Request Vs Commit

![is mr ci](http://www.plantuml.com/plantuml/proxy?src=https://raw.githubusercontent.com/zhongl/dev-guide-on-gitlab/master/.plantuml/is_mr_ci.txt)

- **代码**作为研发最主要的**交付物**, 每次 **Commit**, 都应关联到**唯一**一个 **Merge Request**, 以作为质量检查和评估的单元;
- 每一个 **Merge Request**  都应关联到 **至少** 一个 **Issue**, 以确认某个交付期望被落实.

### Branches

未交付到真正使用之前, 单分支(**master**)迭代演进, 是完全够用的. 一旦交付真正使用, 并持续交付的情况下, 新老版本共存的现象就会出现. 此时, 可以同时维护多个 **Branches**, 比如:

- **master** - 主流版本的功能演进分支
- **1.x** - 第一个正式交付版本的维护分支

### Origin & Forked & Local

刚一开始多个远程库(Remote Repository)之间的交互, 难免会混乱出错. 这里提供如下操作流程:

![origin & forked & local](http://www.plantuml.com/plantuml/proxy?src=https://raw.githubusercontent.com/zhongl/dev-guide-on-gitlab/master/.plantuml/ofl.txt)

1. 使用 `git pull -r origin master` 从 **origin/master** 同步更新到本地;
    1. `-r` 采用 `rebase` 的方式进行合并更新;
    2. 一旦冲突, 建议使用 `git reset --hard origin/master`, **local/master 永远以 origin/master 为准**.
2. 使用 `git checkout -b feature master` 从 **local/master** 检出分支进行新的开发; 
    1. 这里的 `feature` 可自由命名;
3. `feature` 一旦有提交, 则尽快使用 `git push forked feature:master`;
    1. 一旦冲突, 建议使用 `git push -f forked feature:master` 强制覆盖, **forked/master 永远以 local/feature 为准**; 
    2. `forked` 是通过 `git remote add forked http://domain/forked/project.git` 创建的, 其命名可以实际情况调整.
4. 从 `forked/project:master` 向 `origin/project:master` 发起 **Merge Request** .
    1. 若有冲突, 请执行 `步骤1` 将 **local/master** 同步至最新, 然后在 **local/feature** 上执行 `git rebase master` 根据提示解决所有冲突, 最后执行 `git push -f forked feature:master`



[^1]: https://docs.gitlab.com/ce/workflow/forking_workflow.html#project-forking-workflow
[^2]: https://docs.gitlab.com/ce/user/project/merge_requests/
[^3]: https://docs.gitlab.com/ce/ci/merge_request_pipelines/#pipelines-for-merge-requests
[^4]: https://docs.gitlab.com/ee/user/project/merge_requests/#commenting-on-any-file-line-in-merge-requests
[^5]: https://docs.gitlab.com/ee/user/project/merge_requests/#resolve-discussion-comments-in-merge-requests-reviews
[^6]: https://docs.gitlab.com/ce/user/project/merge_requests/#revert-changes
