# Usage

Make a copy of this directory to your private Gitlab repository, eg: `https://your.gitlab.com/ci/includes`. Then include the files in other `.gitlab-ci.yml`, just like:

```yml
inlcude:
  - project: 'ci/includes'
    file: '/maven/predef.yml'
  - project: 'ci/includes'
    file: '/maven/lib.yml'
  # file: '/maven/docker.yml'  
```

# Reference

- https://docs.gitlab.com/11.8/ce/ci/yaml/README.html#include