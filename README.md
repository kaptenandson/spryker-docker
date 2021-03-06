# Docker Images Spryker
![license](https://img.shields.io/github/license/mashape/apistatus.svg)

# Building Images
Steps before building image:
1. Copy the following files and remove extension .dist
    ```
    $ cp ./nginx/glue.template.dist ./nginx/glue.template
    $ cp ./nginx/yves.template.dist ./nginx/yves.template
    $ cp ./nginx/zed.template.dist ./nginx/zed.template
    ```
2. Prepare copied files
    - yves.templae
        ```
        ...
        # DOMAIN = STORE_CODE (stores.php)
        # ~*.*\.domain\.com DOMAIN; = yves domain to your store
        map ${ESC}http_host ${ESC}application_store {
            ~*.*\.domain\.com DOMAIN;
        }
        ...
        ```
    - glue.template
        ```
        ...
        # DOMAIN = STORE_CODE (stores.php)
        # ~*glue\..*\.domain\.com or ~*glue\.domain\.com = glue domain to your store
        map ${ESC}http_host ${ESC}application_store {
            ~*glue\..*\.domain\.com DOMAIN;
            ~*glue\.domain\.com DOMAIN;
        }
        ...
        ```
    - zed.template
        ```
        ...
        # DOMAIN = STORE_CODE (stores.php)
        # ~*zed\..*\.domain\.com or ~*zed\.domain\.com; = zed domain to your store
        map ${ESC}http_host ${ESC}application_store {
            ~*zed\..*\.domain\.com DOMAIN;
            ~*zed\.domain\.com DOMAIN;
        }
        ...
        ```
After these steps have been completed, run the following command:
    ```
    $ chmod +x build.sh
    $ ./build.sh
    ```

# Docker Compose (only for OXS now)
Steps before using Docker Compose:
1. Build docker images ([see here](#building-images))
2. Run nfs_for_native_docker.sh
    ```
    $ chmod +x nfs_for_native_docker.sh
    $ ./nfs_for_native_docker.sh
    ```
3. Copy the following files to the spryker project dir
    ```
    $ cp ./docker-compose.yml.dist /path/to/spryker/project/dir/
    $ cp ./*.env.dist /path/to/spryker/project/dir/
    ```
4. Prepare copied dist files
5. Remove .dist extension from copied files
6. Run automated Nginx Reverse Proxy for Docker
    ```
    $ docker run -d -p 80:80 -v /var/run/docker.sock:/tmp/docker.sock:ro --restart=always jwilder/nginx-proxy
    ```
7. Add entries to host file
    ```
    DOCKER_HOST_IP      dev.domain.com
    DOCKER_HOST_IP      glue.dev.domain.com
    DOCKER_HOST_IP      zed.dev.domain.com
    DOCKER_HOST_IP      jenkins.dev.domain.com
    DOCKER_HOST_IP      rabbitmq.dev.domain.com
    DOCKER_HOST_IP      elasticsearch.dev.domain.com
    ```
After these steps have been completed, run the following command in the spryker project dir:
    ```
    $ docker-compose up
    ```