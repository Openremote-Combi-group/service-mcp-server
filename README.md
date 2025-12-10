# OpenRemote MCP Server
MCP Services for OpenRemote.



## Quick start guide
This guide assumes you already have an OpenRemote instance running.

1. **Create service user**

   In your OpenRemote instance, create a new service user (`settings > users > SERVICE USERS > ADD USER`) and give it the permissions you want to have.
   The MCP server will auto discover the tools that are available.

   _Note: The service user is required to have the `read:services` & `write:services` role._


2. **Setup docker service**
   Create a docker-compose.yml file and configure the service.
    ```yaml
    services:
      # Other OpenRemote services...
    
      mcp-server:
        image: openremote/mcp-server:latest
        restart: always
        depends_on:
          manager:
            condition: service_healthy
        ports:
          - "8420:8420"
        environment:
          OPENREMOTE_CLIENT_ID=<OPENREMOTE_CLIENT_ID>
          OPENREMOTE_CLIENT_SECRET=<OPENREMOTE_CLIENT_SECRET>
          OPENREMOTE_URL=<OPENREMOTE_URL>
          OPENREMOTE_VERIFY_SSL=1
    ```

4. **Run the service**

   Finally, you can run the new service by using docker compose.
    ```shell
    docker compose up
    ```
   This will run the additional service, it will auto-register to your OpenRemote instance. and you can view them in the services tab inside your OpenRemote dashboard.


## Development guide
This guide assumes you already have an OpenRemote instance running.

1. **Create service user**

   In your OpenRemote instance, create a new service user (`settings > users > SERVICE USERS > ADD USER`) and give it the permissions you want to have.
   The MCP server will auto discover the tools that are available.

   _Note: The service user is required to have the `read:services` & `write:services` role._


2. **Sync dependencies**
    ```shell
    uv sync
    ```

3. **Setup environment variables**

   Create a new file `.env` in the root of the project directory. and fill in the following variables replacing the brackets with your own values.
    ```dotenv
    OPENREMOTE_CLIENT_ID=<OPENREMOTE_CLIENT_ID>
    OPENREMOTE_CLIENT_SECRET=<OPENREMOTE_CLIENT_SECRET>
    OPENREMOTE_URL=<OPENREMOTE_URL>
    OPENREMOTE_VERIFY_SSL=1
    ```

6. **Run service**
    ```shell
    uv run uvicorn app:app
    ```