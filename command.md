## Dockerfile 문법 알아보기

| 커맨드 | 의미 |
| --- | --- |
| FROM | 베이스 이미지 지정 |
| RUN | 베이스 이미지에 새로운 레이어를 추가해 커맨드를 실행하고 결과를 빌드 이미지에 반영 |
| CMD | 컨테이너 시작시 실행할 커맨드 설정 |
| LABEL | 이미지에 레이블 지정 |
| EXPOSE | 컨테이너에서 노출하는 포트 번호 설정 |
| ENV | 환경 변수 설정 |
| ADD | 이미지에 파일 복사 |
| COPY | 이미지에 파일 복사 |
| ENTRYPOINT | 컨테이너 시작시 실행할 커맨드 설정 |
| VOLUME | 볼륨이 마운트 될 위치 설정 |
| USER | 커맨드를 실행할 때 사용자 ID 설정 |
| WORKDIR | 커맨드를 실행할 때 작업 디렉터리 설정 |
| ARG | 빌드 시에만 사용되는 변수 설정 |
| ONBUILD | 이 이미지를 베이스로 빌드할 때 커맨드가 실행되도록 하기 |
| STOPSIGNAL | 컨테이너를 중지시킬 때의 시그널 번호 설정 |
| HEALTHCHECK | 헬스 체크를 위한 커맨드 설정 |

## Docker CLI 살펴 보기

| 커맨드 | 의미 |
| --- | --- |
| docker build | Dockerfile로 이미지 빌드 |
| docker images | 이미지 리스트 보기 |
| docker image inspect | 이미지 상세 정보 보기 |
| docker pull | 레지스트리로부터 이미지 가지고 오기 |
| docker push | 레지스트리에 이미지 전송하기 |
| docker history | 이미지 생성 기록 보기 |
| docker rmi | 이미지 삭제 |
| docker import | Docker container export로 가지고 온 것으로 이미지 만들기 |
| docker save | 이미지 tar 아카이브로 출력 |
| docker load | Docker image save로 출력한 것(tar 아카이브)으로 이미지 로드 |
| docker tag | 기존의 이미지에 태그 붙이기 |
| docker ps | 컨테이너 목록 보기 |
| docker logs | 컨테이너 로그 취득 |
| docker exec | 실행 중인 컨테이너 내부에서 커맨드 실행 |
| docker container inspect | 컨테이너의 자세한 정보 보기 |
| docker port | 컨테이너 포트 맵핑 보기 |
| docker rm | 컨테이너 삭제 |
| docker run | 새로운 컨테이너로 커맨드 실행 |
| docker start | 정지 중인 컨테이너 기동 |
| docker stop | 실행 중인 컨테이너 중지 |
| docker restart | 컨테이너 다시 시작 |
| docker kill | 실행 중인 컨테이너(Docker가 만든 PID 1 프로세스)에 신호 보내기 |
