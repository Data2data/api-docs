# Data 2 data API documentation

This repository contains a high-level overview of the public Data 2 data API, as well as links to the detailed specification.

## Terminology

Data 2 data has two types of services.

### Infrastructural services
Infrastructural services perform a supporting role. With their help, you can upload and download files, register users, monitor the status of tasks, etc.

### Data conversion services
Data conversion services process user-uploaded content, perform transformations taking into account user settings, and transmit the result to infrastructure services through which the user receives it.

In other words data conversion services are the key services of the project.

### Task
A task is an entity that describes a task for a data conversion service; it contains a set of service parameters, information about files uploaded by the user, status, time of creation and completion of the task, etc.

The task is registered by the user, then executed by the target service and ends with success or failure.

## Algorithm for interaction between the user and services

The interaction between users and services follows a defined algorithm:

1. Users register an account through the auth service.
Registration is not publicly available. If you need to implement it, please contact us via the [feedback form](https://data2data.ru/suggestions/).

2. Users obtain a token from the auth service for accessing other services.
3. Users register the task in the uploads service.
4. The uploads service checks the service parameters, creates a task and awaits for user files.
5. The uploads service accepts user files to a separate endpoint, then downloads files by URL if specified.
6. Status of the task is set to queued, and the wait for the resources of the data conversion service requested by the user begins.
7. Once the service is ready for processing, the task status changes to execution, and the conversion service starts processing user data.
8. The service processes the task, updating the task status (text description and progress percentage).
9. Users receive status updates via websocket.
10. Upon successful execution, the service sets the task status to success.
11. Users download the resulting file through the downloads service.

## API documentation
The above is only a brief description of the entire project as a whole, which should make it easier to get started with the API.

The Data 2 Data API documentation, available in OpenAPI format, features SwaggerUI and redoc viewers by default.

Documentation links follows the pattern:

`https://beta.data2data.ru/api/{version}/{service}/{path}`

Where:

- version is the API version, currently version v1 is available.
- service - service name, see first column in the table below.
- path - doc for viewing in swagger, redoc for viewing in redoc, and openapi.json - the original specification.

| service | Swagger | Redoc | OpenAPI |
| --- | --- | --- | --- |
| Auth | [Swagger](https://beta.data2data.ru/api/v1/auth/docs) | [Redoc](https://beta.data2data.ru/api/v1/auth/redoc) | [OpenAPI](https://beta.data2data.ru/api/v1/auth/openapi.json) |
| uploads | [Swagger](https://beta.data2data.ru/api/v1/uploads/docs) | [Redoc](https://beta.data2data.ru/api/v1/uploads/redoc) | [OpenAPI](https://beta.data2data.ru/api/v1/uploads/openapi.json) |
| ocr | [Swagger](https://beta.data2data.ru/api/v1/ocr/docs) | [Redoc](https://beta.data2data.ru/api/v1/ocr/redoc) | [OpenAPI](https://beta.data2data.ru/api/v1/ocr/openapi.json) |
| tasks | [Swagger](https://beta.data2data.ru/api/v1/tasks/docs) | [Redoc](https://beta.data2data.ru/api/v1/tasks/redoc) | [OpenAPI](https://beta.data2data.ru/api/v1/tasks/openapi.json) |
| downloads | [Swagger](https://beta.data2data.ru/api/v1/downloads/docs) | [Redoc](https://beta.data2data.ru/api/v1/downloads/redoc) | [OpenAPI](https://beta.data2data.ru/api/v1/downloads/openapi.json) |

## Where to begin?

You can read the documentation in the order corresponding to the arrangement of services in the table above.
