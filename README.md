# Docker-CI-project-for-1C

Проект предназначен для работы с CI контуром из Docker https://github.com/hoppipolla1/Docker-CI-for-1C
Полная сборочная линия для 1С на Windows с использованием CI в Linux контейнерах

Первым делом нужно создать локальный репозиторий в Gitlab, можно клонировать этот репозиторий

Установить OneScript и связать через GitSync хранилище конфигурации с репозиторием в Gitlab

Создать или отредактировать файлы AUTHORS и VERSION. В файле AUTHORS устанавливается связь между пользователями хранилища конфигурации и пользователями в Gitlab

Все файлы конфигурации должны лежать в папке src

Выполнить первичную настройку с помощью .cmd файлов prepare.cmd и build.cmd, запушить изменения в Gitlab

В папке tools выполнить административные настройки с помощью .cmd файлов git-global-init-admin.cmd и git-global-init.cmd

Заполнить настройки .json файлов для работы с Vanessa в той же папке tools в файлах vrunner.json и xUnitParams.json, остальные файлы с настройками на усмотрение

Настроить файл для SonarQube sonar-project.properties

Настройка Jenkins:

Пайплайн работает на двух нодах, мастере и Windows. Для корректной работы Vanessa необходимо создать ноду Windows с аналогичным названием лейбла
![image](https://user-images.githubusercontent.com/110767375/224963472-d7920285-70a8-4cd2-9e3a-8fc707db8155.png)
![image](https://user-images.githubusercontent.com/110767375/224963561-38550b24-6b4a-4c68-8216-3f5da304df25.png)

Как добавить Windows Node в Jenkins можно посмотреть тут - https://www.youtube.com/watch?v=tO7j6bVQir0
Как результат должен быть запущен сервис и создан каталог под сервис
![image](https://user-images.githubusercontent.com/110767375/224964103-47cb1cee-105e-4224-a437-efa89554e5fa.png)
![image](https://user-images.githubusercontent.com/110767375/224964190-ba0cc568-80dc-40eb-ba34-d01aa930a85b.png)


Полный список плагинов в Jenkins:

Allure Jenkins Plugin

Ant Plugin

Apache HttpComponents Client 4.x API

Authentication Tokens API Plugin

Blue Ocean Core JS

Bootstrap 5 API Plugin

bouncycastle API Plugin

Branch API Plugin

Build Timeout

Caffeine API Plugin

Checks API plugin

Command Agent Launcher Plugin

Common API for Blue Ocean

commons-lang3 v3.x Jenkins API Plugin

commons-text API Plugin

Config File Provider Plugin

Credentials Binding Plugin

Credentials Plugin

Design Language

Display URL API

Docker API Plugin

Docker Commons Plugin

Docker plugin

Durable Task Plugin

ECharts API Plugin

Email Extension Plugin

Favorite

Folders Plugin

Font Awesome API Plugin

Git client plugin

Git Pipeline for Blue Ocean

Git plugin

Git server Plugin

GitHub API

GitHub Branch Source Plugin

GitHub plugin

Gradle Plugin

HTML Publisher plugin

HTTP Request Plugin

Instance Identity

Ionicons API

Jackson 2 API Plugin

Jakarta Activation API

Jakarta Mail API

Java JSON Web Token (JJWT) Plugin

JavaBeans Activation Framework (JAF) API

JavaMail API

JAXB plugin

JQuery3 API Plugin

JUnit Plugin

JWT for Blue Ocean

LDAP Plugin

Mailer Plugin

Matrix Authorization Strategy Plugin

Matrix Project Plugin

Mina SSHD API :: Common

Mina SSHD API :: Core

OkHttp Plugin

Oracle Java SE Development Kit Installer Plugin

OWASP Markup Formatter

PAM Authentication plugin

Pipeline

Pipeline Aggregator View

Pipeline Graph Analysis Plugin

Pipeline implementation for Blue Ocean

Pipeline SCM API for Blue Ocean

Pipeline timeline

Pipeline Utility Steps

Pipeline: API

Pipeline: Basic Steps

Pipeline: Build Step

Pipeline: Declarative

Pipeline: Declarative Extension Points API

Pipeline: Deprecated Groovy Libraries

Pipeline: GitHub Groovy Libraries

Pipeline: Groovy

Pipeline: Groovy Libraries

Pipeline: Input Step

Pipeline: Job

Pipeline: Milestone Step

Pipeline: Model API

Pipeline: Multibranch

Pipeline: Multibranch with defaults

Pipeline: Nodes and Processes

Pipeline: REST API Plugin

Pipeline: SCM Step

Pipeline: Stage Step

Pipeline: Stage Tags Metadata

Pipeline: Stage View Plugin

Pipeline: Step API

Pipeline: Supporting APIs

Plain Credentials Plugin

Plugin Utilities API Plugin

Popper.js 2 API Plugin

Pub-Sub "light" Bus

Resource Disposer Plugin

REST API for Blue Ocean

REST Implementation for Blue Ocean

SCM API Plugin

Script Security Plugin

SnakeYAML API Plugin

SonarQube Scanner for Jenkins

SSH Build Agents

SSH Credentials Plugin

SSH server

Structs Plugin

Timestamper

Token Macro Plugin

Trilead API Plugin

Variant Plugin

Web for Blue Ocean

Workspace Cleanup Plugin

В конфигурации глобальных инструментов необходимо добавить:
SonarScanner с именем "SonarQube Scanner"
![image](https://user-images.githubusercontent.com/110767375/224956905-2f685894-266b-43df-8994-871557dba00e.png)

Allure
![image](https://user-images.githubusercontent.com/110767375/224957004-4d472f15-2d51-4c2f-81fd-ae0288a788ad.png)

Allure также необходимо установить на рабочее место, для Windows проще всего сделать через scoop: scoop install allure

В настройках системы необходимо заполнить следующие параметры:
Jenkins URL - указать адрес кроме localhost

SonarQube	servers - указать адрес SonarQube
![image](https://user-images.githubusercontent.com/110767375/224957692-ae3c2333-5be0-45ba-b725-b34c463f31e0.png)

Global pipeline libraries - указать локальный репозиторий с библиотекой или https://github.com/hoppipolla1/Jenkins-lib-for-1C
![image](https://user-images.githubusercontent.com/110767375/224962428-19261e4c-6723-4f9d-a2fd-49152a9e8b39.png)
![image](https://user-images.githubusercontent.com/110767375/224962712-8055585b-c499-4f3f-9d7c-a21449988655.png)

Создать multi-branch pipeline, в котором указать путь к репозиторию с проектом
Build Configuration - by JenkinsFile
![image](https://user-images.githubusercontent.com/110767375/224963216-d80e3918-383a-4b5c-8b29-7c77dd8aaa32.png)
![image](https://user-images.githubusercontent.com/110767375/224963291-d58d8d3e-a2ae-45fc-8615-88717edc2157.png)

После всех настроек можно запускать сборку и как результат получить отчет allure, артефакты, проверенный проект в SonarQube и детальный Stage View
![image](https://user-images.githubusercontent.com/110767375/224964708-89593546-6cb9-4caf-ad79-b9bb411ff6ff.png)
![image](https://user-images.githubusercontent.com/110767375/224964824-d2607a9f-4980-4ff4-83c0-4428b9c99ce5.png)
![image](https://user-images.githubusercontent.com/110767375/224964911-421847d5-8870-4ff3-a495-d22a2c07561e.png)
![image](https://user-images.githubusercontent.com/110767375/224965058-a1d633ff-3606-4599-a4c6-2435917d91e4.png)
![image](https://user-images.githubusercontent.com/110767375/224965160-c8752219-e674-4970-8b40-bdd29a307c86.png)

