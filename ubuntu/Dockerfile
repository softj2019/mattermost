# Ubuntu Jammy 22.04 LTS 또는 Noble 24.04 LTS를 기반으로 사용
FROM ubuntu:22.04

# 환경 변수 설정
ENV DEBIAN_FRONTEND=noninteractive

# 필수 패키지 설치
RUN apt-get update && apt-get install -y \
    curl \
    wget \
    gnupg \
    software-properties-common \
    apt-transport-https \
    ca-certificates \
    build-essential \
    jq \
    net-tools \
    postgresql-client \
    && apt-get clean \
    && rm -rf /var/lib/apt/lists/*

# Mattermost 설치
WORKDIR /opt
RUN curl -o mattermost.tar.gz https://releases.mattermost.com/7.10.2/mattermost-7.10.2-linux-amd64.tar.gz && \
    tar -xvzf mattermost.tar.gz && \
    rm mattermost.tar.gz && \
    mkdir -p /opt/mattermost/data

# 데이터 및 로그 디렉토리 생성
VOLUME /opt/mattermost/data
VOLUME /opt/mattermost/logs

# Mattermost 설정
COPY ./config.json /opt/mattermost/config/config.json

# 포트 노출
EXPOSE 8065

# Mattermost 실행
WORKDIR /opt/mattermost
USER root
CMD ["./bin/mattermost"]
