### Getting Started

> Note: This demonstration just uses very few of the features of [ytt](https://carvel.dev/ytt/), like data values, overlay, etc. in combination with [yq eval - command](https://mikefarah.gitbook.io/yq/commands/evaluate). There are lot of powerful feature that [ytt](https://carvel.dev/ytt/) tool contributes, to make use of. 

- Install [ytt](https://carvel.dev/ytt/) command line tool from [here](https://carvel.dev/ytt/docs/v0.46.x/install/)

- Install [yq](https://mikefarah.gitbook.io/yq/) command line tool from [here](https://github.com/mikefarah/yq/#install)

> Note: The number `x_` prefix on the folder name (shared --> environment) is very important for the order of applying in the [ytt](https://carvel.dev/ytt/) command.

- The `1_shared` folder here contains the shared [ytt](https://carvel.dev/ytt/) template, values-schema, values, overlays, etc. 

- The `2_environment` folder here contains the environment specific [ytt](https://carvel.dev/ytt/) template, values-schema, values, overlays, etc.

- The environment folder contains `local`, `shuttle`, etc. which represents the target environments where it contains **values and overlays only** as needed.

- To demonstrate the example, to create `docker-compose.yml` for `local` environment, execute below code from the root. 

    ```sh
    ytt -f ./demo1/1_shared -f ./demo1/2_environment/local | yq eval '.services |= with_entries(.key = .value.container_name)' | yq eval '.networks |= with_entries(.key = .value.name)' > docker-compose-demo1-local.yml
    ```

- To demonstrate the example, to create `docker-compose.yml` for `shuttle` environment, execute below code from the root. 

    ```sh
    ytt -f ./demo1/1_shared -f ./demo1/2_environment/shuttle | yq eval '.services |= with_entries(.key = .value.container_name)' | yq eval '.networks |= with_entries(.key = .value.name)' > docker-compose-demo1-shuttle.yml
    ```

- To execute `docker compose up` from the produced output inline, execute the below command. This command targets the local environment.
    
    ```sh
    ytt -f ./demo1/1_shared -f ./demo1/2_environment/shuttle | yq eval '.services |= with_entries(.key = .value.container_name)' | yq eval '.networks |= with_entries(.key = .value.name)' | docker compose -f- up
    ```

