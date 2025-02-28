Golang API Starter Kit
================
[![Build Status](https://travis-ci.org/vardius/go-api-boilerplate.svg?branch=master)](https://travis-ci.org/vardius/go-api-boilerplate)
[![Go Report Card](https://goreportcard.com/badge/github.com/vardius/go-api-boilerplate)](https://goreportcard.com/report/github.com/vardius/go-api-boilerplate)
[![codecov](https://codecov.io/gh/vardius/go-api-boilerplate/branch/master/graph/badge.svg)](https://codecov.io/gh/vardius/go-api-boilerplate)
[![](https://godoc.org/github.com/vardius/go-api-boilerplate?status.svg)](http://godoc.org/github.com/vardius/go-api-boilerplate)
[![license](https://img.shields.io/github/license/mashape/apistatus.svg)](https://github.com/vardius/go-api-boilerplate/blob/master/LICENSE.md)

Go Server/API boilerplate using best practices, DDD, CQRS, ES, gRPC.

<details>
  <summary>Table of Contents</summary>

<!-- toc -->

- [About](#about)
- [Documentation](#documentation)
- [Example](#example)
  - [Domain](#domain)
    - [Dispatching command](#dispatching-command)
  - [View](#view)
    - [Public routes](#public-routes)
    - [Protected routes](#protected-routes)
<!-- tocstop -->

</details>

ABOUT
==================================================
This repository was created for personal use and needs, may contain bugs. If found please report. If you think some things could be done better, or if this repository is missing something feel free to contribute and create pull request.

Contributors:

* [Rafał Lorenz](http://rafallorenz.com)

Want to contribute ? Feel free to send pull requests!

Have problems, bugs, feature ideas?
We are using the github [issue tracker](https://github.com/vardius/go-api-boilerplate/issues) to manage them.

![Dashboard](../master/.github/kubernetes-dashboard-overview.png)
![Dashboard](../master/.github/kubernetes-dashboard-pods.png)

Key concepts:
1. Rest API
2. [Docker](https://www.docker.com/what-docker)
3. [Kubernetes](https://kubernetes.io/)
4. [Helm chart](https://helm.sh/)
5. [gRPC](https://grpc.io/docs/)
6. [Domain Driven Design](https://en.wikipedia.org/wiki/Domain-driven_design)  (DDD)
7. [CQRS](https://martinfowler.com/bliki/CQRS.html)
8. [Event Sourcing](https://martinfowler.com/eaaDev/EventSourcing.html)
9. [Hexagonal, Onion, Clean Architecture](https://herbertograca.com/2017/11/16/explicit-architecture-01-ddd-hexagonal-onion-clean-cqrs-how-i-put-it-all-together/)
10. [oAuth2](https://github.com/go-oauth2/oauth2)

Worth getting to know packages used in this boilerplate:
1. [gorouter](https://github.com/vardius/gorouter)
2. [message-bus](https://github.com/vardius/message-bus)
3. [gollback](https://github.com/vardius/gollback)
4. [shutdown](https://github.com/vardius/shutdown)
5. [pubsub](https://github.com/vardius/pubsub)

DOCUMENTATION
==================================================

* [Wiki](https://github.com/vardius/go-api-boilerplate/wiki)
* [Package level docs](https://godoc.org/github.com/vardius/go-api-boilerplate#pkg-subdirectories)
* [Getting Started](https://github.com/vardius/go-api-boilerplate/wiki/1.-Getting-Started)
* [Installing and Setting up](https://github.com/vardius/go-api-boilerplate/wiki/2.-Installing-and-Setting-up)
* [Configuration](https://github.com/vardius/go-api-boilerplate/wiki/3.-Configuration)
* [Guides](https://github.com/vardius/go-api-boilerplate/wiki/4.-Guides)

EXAMPLE
==================================================

## Domain
### Dispatching command
Send example JSON via POST request
```sh
curl -sSL -D -d '{"email":"test@test.com"}' -H "Content-Type: application/json" -X POST https://go-api-boilerplate.local/users/dispatch/register-user-with-email -o /dev/null --insecure
```
## View
### Public routes
Get user details [https://go-api-boilerplate.local/users/34e7ed39-aa94-4ef2-9422-401bba9fc812](https://go-api-boilerplate.local/users/34e7ed39-aa94-4ef2-9422-401bba9fc812)
```json
{"id":"34e7ed39-aa94-4ef2-9422-401bba9fc812","email":"test@test.com"}
```
Get list of users [https://go-api-boilerplate.local/users?page=1&limit=10](https://go-api-boilerplate.local/users?page=1&limit=10)
```json
{"page":1,"limit":20,"total":1,"users":[{"id":"34e7ed39-aa94-4ef2-9422-401bba9fc812","email":"test@test.com"}]}
```
### Protected routes
Access protected route using auth token [https://go-api-boilerplate.local/users/me](https://go-api-boilerplate.local/users/me).
```json
{"code": "401","message": "Unauthorized"}
```
Request access token for user
```sh
curl -sSL -D -d '{"id":"34e7ed39-aa94-4ef2-9422-401bba9fc812"}' -H "Content-Type: application/json" -X POST https://go-api-boilerplate.local/users/dispatch/request-user-access-token -o /dev/null --insecure
```
Get your access token from user pod event handler logs.

Access protected route using auth token [https://go-api-boilerplate.local/users/me?authToken=eyJhbGciOiJIUzUxMiIsInR5cCI6IkpXVCJ9.eyJhdWQiOiJyXHUwMDE277-977-977-977-9IiwiZXhwIjoxNTU5NjEwOTc2LCJzdWIiOiIzNGU3ZWQzOS1hYTk0LTRlZjItOTQyMi00MDFiYmE5ZmM4MTIifQ.pEkgtDAvNh2D3Dtgfpu4tt-Atn1h6QwMkDhz4KpgFxNX8jE7fQH00J6K5V7CV063pigxWhOMMTRLmQdhzhajzQ](https://go-api-boilerplate.local/users/me?authToken=eyJhbGciOiJIUzUxMiIsInR5cCI6IkpXVCJ9.eyJhdWQiOiJyXHUwMDE277-977-977-977-9IiwiZXhwIjoxNTU5NjEwOTc2LCJzdWIiOiIzNGU3ZWQzOS1hYTk0LTRlZjItOTQyMi00MDFiYmE5ZmM4MTIifQ.pEkgtDAvNh2D3Dtgfpu4tt-Atn1h6QwMkDhz4KpgFxNX8jE7fQH00J6K5V7CV063pigxWhOMMTRLmQdhzhajzQ)
```json
{"id":"34e7ed39-aa94-4ef2-9422-401bba9fc812","email":"test@test.com"}
```
