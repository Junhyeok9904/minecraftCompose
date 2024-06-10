
---

# Minecraft Server Docker Project

## 개요

이 프로젝트는 Docker를 사용하여 어떤 환경에서도 Minecraft 서버를 실행할 수 있도록 설계되었습니다. 특히, 모드 서버를 가동할 수 있으며, 1.18 버전 미만의 모드팩을 구동할 수 있도록 제작되었습니다.

## 특징

- **모드 서버 지원**: Minecraft의 다양한 모드 서버를 실행할 수 있습니다.
- **1.18 버전 미만 모드팩 지원**: 1.18 버전 미만의 모드팩을 CurseForge에서 다운로드하여 사용할 수 있습니다.
- **서버 전용 모드 파일 필요**: 클라이언트용 모드가 아닌 서버용 모드의 zip 파일이 필요합니다.

## 전제 지식

이 프로젝트를 사용하려면 다음과 같은 기본적인 지식이 필요합니다:
- Docker의 기본적인 가동 지식
- 네트워크 관련 지식
- Docker 및 Minecraft에 대한 기본 지식 (예: 컨테이너 마운트, Docker Compose, Minecraft 서버 설정 등)

이 프로젝트는 Docker 또는 Minecraft에 대한 지식을 제공하지 않습니다. 따라서, 이 프로젝트를 사용하기 전에 해당 지식을 습득하셔야 합니다.

## 가동 조건

이 프로젝트를 실행하기 위해서는 다음이 필요합니다:
1. Docker 설치
2. Docker Compose 설치 (Windows나 Mac 이외의 OS에서 필요)

## 가동 방법

1. Docker Compose 파일을 작성합니다. 예제 파일은 다음과 같습니다:

    ```yaml
    services:
      minecraft:
        container_name: mc
        image: itzg/minecraft-server:java8-multiarch
        ports:
          - 25564:25565
        tty: true        
        stdin_open: true  
        environment:
          MEMORY: 16G
          ENABLE_ROLLING_LOGS: "TRUE"
          TYPE: CURSEFORGE
          CF_SERVER_MOD: "<MOD.zip형식의 모드 파일이 필요 path는./data폴더 안에 넣을것>"
          EULA: "TRUE"
          VERSION: "1.12.2"
          MOTD: "The World of Moded Server"
          MAX_PLAYERS: 10
          MAX_WORLD_SIZE: 10000
          ENABLE_COMMAND_BLOCK: "TRUE"
          VIEW_DISTANCE: 12
          MODE: "SURVIVAL"
          PVP: "FALSE"
          STOP_SERVER_ANNOUNCE_DELAY: 20
          GUI: "FALSE"
        volumes:
          - ./data:/data
          - ./downloads:/downloads
        restart: unless-stopped
    ```

2. Docker Compose를 사용하여 서버를 실행합니다:

    ```sh
    docker compose up -d
    ```

3. 서버가 실행되면, `localhost:25565` 등으로 접속해 보시기 바랍니다.

---

이 초안을 기반으로 필요에 따라 내용을 추가하거나 수정할 수 있습니다. 추가로 필요한 사항이나 수정할 부분이 있으면 말씀해 주세요!