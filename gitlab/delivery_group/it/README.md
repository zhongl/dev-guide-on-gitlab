# 说明

本库配置定义了项目 **D** 的日常集成环境, 其中基础服务有:

- **gateway** - 环境内各服务的 **HTTP** 访问网关;
- **dns** - 供自定义的域名解析服务;
- **hub** - 供环境部署 Docker 镜像的私库.

```plantuml

actor Browser as B
boundary ":80/tcp" as H
boundary ":53/upd" as D

cloud SWARM {
    node dns

    together {
        node gateway
        node hub
        node "???" as N
    }

}

B -right-> D: query: hub.d.it
B --> H: http://hub.d.it
dns -left- D
dns -[hidden]-> gateway

gateway -left- H
gateway -right-> hub
gateway -> N

hub -[hidden]-> N
```

## 新增服务

请参考 [docker-compose.yml](./docker-compose.yml), 并遵照 [Fork & Merge](https://github.com/icongtai/dev-guide-on-gitlab/blob/master/GUIDE.md#fork--merge-development-cycle) 流程发起 **Merge Request** .

## 部署服务

通过在服务所属库中的 `.gitlab-ci.yml` 添加 **Trigger** 任务[^1]实现.

[^1]: https://docs.gitlab.com/ce/ci/triggers/README.html#triggering-a-pipeline
