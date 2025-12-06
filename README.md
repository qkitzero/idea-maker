# Idea Maker

- [Auth Service](https://github.com/qkitzero/auth-service)
- [User Service](https://github.com/qkitzero/user-service)
- [Combination Service](https://github.com/qkitzero/combination-service)
- [Logging Service](https://github.com/qkitzero/logging-service)

```mermaid
flowchart TD
    user(User)

    subgraph gcp[GCP]
        subgraph cloud_run[Cloud Run]
            idea_maker_frontend(Idea Maker Frontend)
            auth_service(Auth Service)
            auth_service_gateway(Auth Service Gateway)
            user_service(User Service)
            user_service_gateway(User Service Gateway)
            combination_service(Combination Service)
            combination_service_gateway(Combination Service Gateway)
            logging_service(Logging Service)
        end
    end

    subgraph external[External]
        auth0(Auth0)
        user_db[(User DB)]
        combination_db[(Combination DB)]
        logging_db[(Logging DB)]
    end

    user --> idea_maker_frontend

    idea_maker_frontend --> auth_service_gateway --> auth_service --> auth0
    idea_maker_frontend --> user_service_gateway --> user_service
    idea_maker_frontend --> combination_service_gateway --> combination_service
    idea_maker_frontend --> auth0

    user_service --> auth_service
    combination_service --> auth_service
    logging_service --> auth_service

    user_service --> logging_service
    combination_service --> logging_service

    user_service --> user_db
    combination_service --> combination_db
    logging_service --> logging_db
```
