# Project Information

## Project Name

nginx-flask-mysql


## Repository URL

https://github.com/docker/awesome-compose/tree/master/nginx-flask-mysql


## Description

A multi-container web application example using Docker Compose.

The project contains:

- Nginx reverse proxy
- Flask backend application
- MariaDB database


## Technologies

| Component | Technology |
|---|---|
| Reverse Proxy | Nginx |
| Backend Framework | Flask |
| Programming Language | Python |
| Database | MariaDB |
| Container Platform | Docker |
| Orchestration | Docker Compose |


## Services

### Proxy

Purpose:
Reverse Proxy

Port:
80


### Backend

Purpose:
Flask Web Application

Port:
8000


Dependencies:

- Flask 2.0.1
- mysql-connector 2.2.9


### Database

Purpose:
Data Storage

Technology:

MariaDB 10-focal

Internal Ports:

- 3306
- 33060


## Docker Files

Backend:

backend/Dockerfile

Proxy:

proxy/Dockerfile


## Compose File

compose.yaml


## Networks

frontnet:

Proxy and Backend communication


backnet:

Backend and Database communication


## Volumes

db-data:

MariaDB persistent storage


## Deployment Notes

This project will be deployed using Docker Compose
and automated using Ansible.

Nginx runs as a Docker container and acts as the
external reverse proxy.
