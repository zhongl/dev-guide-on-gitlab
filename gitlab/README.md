# Gitlab 最佳实践

## Include CICD

在尝试根据不同工程类型进行 **Pipeline** 标准化中, 发现 Gitlab 内置的 `.gitlab-ci.yml` 的模版达不到 **统一简化** 的目的. 转而借由 **Include** [^1], 细节相见 [cicd/includes](./gitlab/cicd/includes/).

## Delivery Group

Gitlab 的 Group 具有灵活的命名空间机制. 微服务架构风格的实践中, 将一个业务方向(线)的若干微服务工程编组在同一个交付 Group 下是个不错的选择.

### Issues Project

一个 Group 一般存在多个交付的 Project, 而且是同一个研发团队. 整个团队日常的 Issues 管理放在任何一个交付的 Project 中都觉得不合适, 因此每个 Group 需要创建一个 **Issues Project** 来专门管理 Issues. 此时, 实际的交付项目中, 则不在需要加载 Issue 功能, 仅留下 **Merge Requests** 即可.

### Integration Project

> 简称 **it**. 

微服务架构下, 多 Projects 同时研发推进是必然的. 配合着持续集成交付, 则要求集成环境不光是稳定, 而且能够及时响应变化. 创建一个专门的 **Integration Project** 是非常有必要的:

1. 环境配置统一共享维护, 不在是某个OPS电脑里的乱七八糟的脚本;
2. 利用 **Merge Requests** 有效建立 **Review** 机制, 有助于保持环境稳定;
3. 利用 **Pipeline** 自动执行环境部署, 有记录, 可重复, 可回滚.


[^1]: https://docs.gitlab.com/ce/ci/yaml/README.html#include