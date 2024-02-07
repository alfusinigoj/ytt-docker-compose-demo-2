This repo shows a simple demonstration of using [ytt](https://carvel.dev/ytt/) and [yq](https://mikefarah.gitbook.io/yq) to generate docker compose file for for Rabbitmq HA, targeting multiple environments.

### What is [ytt](https://carvel.dev/ytt/)?

It is a simple tool helps in shaping and templating YAML content, including, Kubernetes configuration, Concourse pipelines, Docker Compose files, etc. This is maintained by [CNCF](https://www.cncf.io/sandbox-projects/)

For documentation, refer [here](https://carvel.dev/ytt/docs/v0.46.x/), there are lot of samples with playground, which can be found [here](https://carvel.dev/ytt/#playground)

### Getting Started

> Note: This demonstration just uses very few of the features of [ytt](https://carvel.dev/ytt/), like data values, overlay, etc. in combination with [yq eval - command](https://mikefarah.gitbook.io/yq/commands/evaluate). There are lot of powerful feature that [ytt](https://carvel.dev/ytt/) tool contributes, to make use of. 

- Install [ytt](https://carvel.dev/ytt/) command line tool from [here](https://carvel.dev/ytt/docs/v0.46.x/install/)

- Install [yq](https://mikefarah.gitbook.io/yq/) command line tool from [here](https://github.com/mikefarah/yq/#install)

> Note: The number `x_` prefix on the folder name is very important for the order of applying in the [ytt](https://carvel.dev/ytt/) command.

- The `1_default_schema` folder here contains the [ytt](https://carvel.dev/ytt/) template and values-schema. 

- The `2_default_values` folder here contains the [ytt](https://carvel.dev/ytt/) default values. 

- The `3_default_overlays` folder here contains the [ytt](https://carvel.dev/ytt/) overlays. 

- The environment folder contains `local`, `shuttle`, etc. which represents the target environments where it contains values and overlays as needed.

- To demonstrate the example, to create `docker-compose.yml` for `local` environment, execute below code from the root. 

    ```sh
    ytt -f ./1_default_schema  -f ./2_default_values -f ./3_default_overlays -f ./environment/local/1_values -f ./environment/local/2_overlays | yq eval '.services |= with_entries(.key = .value.container_name)' | yq eval '.networks |= with_entries(.key = .value.name)' > docker-compose.yml
    ```

- To demonstrate the example, to create `docker-compose.yml` for `shuttle` environment, execute below code from the root. 

    ```sh
    ytt -f ./1_default_schema  -f ./2_default_values -f ./3_default_overlays -f ./environment/shuttle/1_values -f ./environment/shuttle/2_overlays | yq eval '.services |= with_entries(.key = .value.container_name)' | yq eval '.networks |= with_entries(.key = .value.name)' > docker-compose.yml
    ```

- To execute `docker compose up` from the produced output inline, execute the below command. This command targets the local environment.
    
    ```sh
    ytt -f ./1_default_schema  -f ./2_default_values -f ./3_default_overlays -f ./environment/local/1_values -f ./environment/local/2_overlays | yq eval '.services |= with_entries(.key = .value.container_name)' | yq eval '.networks |= with_entries(.key = .value.name)' | docker compose -f- up
    ```

### Additional References

- Documentation from **Tanzu Development Center**, [Getting Started with ytt](https://tanzu.vmware.com/developer/guides/ytt-gs/)
- Refer this [docker-compose](https://github.com/UKP-SQuARE/square-core/blob/master/docker-compose.ytt.yaml) file for usage of [ytt](https://carvel.dev/ytt/) extensively.
