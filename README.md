This repo shows a simple demonstration of using [ytt](https://carvel.dev/ytt/) and [yq](https://mikefarah.gitbook.io/yq) to generate docker compose file targeting multiple environments, but using real example of building a highly available rabbitmq cluster together with haproxy.

### What is [ytt](https://carvel.dev/ytt/)?

It is a simple tool helps in shaping and templating YAML content, including, Kubernetes configuration, Concourse pipelines, Docker Compose files, etc. This is maintained by [CNCF](https://www.cncf.io/sandbox-projects/)

For documentation, refer [here](https://carvel.dev/ytt/docs/v0.46.x/), there are lot of samples with playground, which can be found [here](https://carvel.dev/ytt/#playground)

### Getting Started

 - Navigate into [demo1](./demo1/README.md) and [demo2](./demo2/README.md), then follow the readme. Both shows different ways of using [ytt](https://carvel.dev/ytt/). Important differentiator here is `demo1` requires [yq](https://mikefarah.gitbook.io/yq/) whereas `demo2` is not.

### Additional References

- Documentation from **Tanzu Development Center**, [Getting Started with ytt](https://tanzu.vmware.com/developer/guides/ytt-gs/)
- Refer this [docker-compose](https://github.com/UKP-SQuARE/square-core/blob/master/docker-compose.ytt.yaml) file for usage of [ytt](https://carvel.dev/ytt/) extensively.
- Yaml Comparison tool [dyff](https://github.com/homeport/dyff) can be used to compare your generated file against a base, using below command syntax.

    ```sh
    dyff between <file1.yml> <file2.yml>
    ```
