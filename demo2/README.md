### Getting Started

> Note: This demonstration just uses very few of the features of [ytt](https://carvel.dev/ytt/), like data values, overlay, etc. There are lot of powerful feature that [ytt](https://carvel.dev/ytt/) tool contributes, to make use of. 

- Install [ytt](https://carvel.dev/ytt/) command line tool from [here](https://carvel.dev/ytt/docs/v0.46.x/install/)

> Note: The number `x_` prefix on the folder name (shared --> environment) is for understanding saying that its better to use them in order while using in the command.

- The `1_shared` folder here contains the shared [ytt](https://carvel.dev/ytt/) template, values-schema, values, overlays, etc. 

- The `2_environment` folder here contains the environment specific [ytt](https://carvel.dev/ytt/) template, values-schema, values, overlays, etc.

- The environment folder contains `local`, `shuttle`, etc. which represents the target environments where it contains **template, values-schema, values, overlays, etc** as needed.

- To demonstrate the example, to create `docker-compose.yml` for `local` environment, execute below code from the root. 

    ```sh
    ytt -f ./demo2/1_shared -f ./demo2/2_environment/local > docker-compose-demo2-local.yml
    ```

- To demonstrate the example, to create `docker-compose.yml` for `shuttle` environment, execute below code from the root. 

    ```sh
    ytt -f ./demo2/1_shared -f ./demo2/2_environment/shuttle > docker-compose-demo2-shuttle.yml
    ```

- To execute `docker compose up` from the produced output inline, execute the below command. This command targets the local environment.
    
    ```sh
    ytt -f ./demo2/1_shared -f ./demo2/2_environment/shuttle | docker compose -f- up
    ```
