
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
            container_name: mc # 컨테이너 이름을 'mc'로 설정
            image: itzg/minecraft-server:java8-multiarch # Java 8을 사용하도록 설정된 Minecraft 서버 이미지
            ports: - 25565:25565 # 호스트의 포트 25565를 컨테이너의 포트 25565로 매핑
            tty: true # 터미널 할당 (`-t` 옵션)
            stdin_open: true # 표준 입력 스트림 열기 (`-i` 옵션)
        environment:
            MEMORY: 16G # 서버에 할당할 메모리 양
            ENABLE_ROLLING_LOGS: "TRUE" # 롤링 로그를 활성화
            TYPE: CURSEFORGE # 서버 유형을 CurseForge로 설정
            CF_SERVER_MOD: "<MOD.zip>" # 사용할 모드 파일을 지정 (./data 폴더 내에 모드 파일을 위치)
            EULA: "TRUE" # Minecraft EULA에 동의
            VERSION: "1.12.2" # Minecraft 서버 버전을 1.12.2로 설정
            MOTD: "The World of Moded Server" # 서버의 모티브 (Message of the Day)
            MAX_PLAYERS: 10 # 최대 플레이어 수를 10명으로 설정
            MAX_WORLD_SIZE: 10000 # 월드 최대 크기를 10000으로 설정
            ENABLE_COMMAND_BLOCK: "TRUE" # 커맨드 블록을 활성화
            VIEW_DISTANCE: 12 # 뷰 거리 설정
            MODE: "SURVIVAL" # 게임 모드를 서바이벌로 설정
            PVP: "FALSE" # 플레이어 간 전투를 비활성화
            STOP_SERVER_ANNOUNCE_DELAY: 20 # 서버 중지 알림 지연 시간을 20초로 설정
            GUI: "FALSE" # 서버 GUI를 비활성화
            GENERATE_STRUCTURES: "TRUE" # 구조물 생성을 활성화
            SPAWN_PROTECTION: 10 # 스폰 보호 크기를 10으로 설정
            USE_AIKAR_FLAGS: "TRUE" # Aikar 플래그 사용
        volumes:
            - ./data:/data # 호스트의 ./data 디렉토리를 컨테이너의 /data 디렉토리로 마운트
            - ./downloads:/downloads # 호스트의 ./downloads 디렉토리를 컨테이너의 /downloads 디렉토리로 마운트
    restart: unless-stopped # 컨테이너가 중지될 때 자동으로 재시작 (명시적으로 중지할 때까지)

    ```

2. Docker Compose를 사용하여 서버를 실행합니다:

    ```sh
    docker compose up -d
    ```

3. 서버가 실행되면, `localhost:25565` 등으로 접속해 보시기 바랍니다.

---

이 초안을 기반으로 필요에 따라 내용을 추가하거나 수정할 수 있습니다. 추가로 필요한 사항이나 수정할 부분이 있으면 말씀해 주세요!