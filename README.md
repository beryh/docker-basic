# Docker basics
여러분은 컨테이너가 소프트웨어 조직의 주요 업무인 소프트웨어 빌드, 테스트 및 배포하는 방식을 어떻게 혁신하고 있는지 배웠습니다. 또한 Docker라는 컨테이너 런타임에 대해서도 배웠는데, 이는 소프트웨어를 컨테이너에 패키징하고 하나 이상의 다양한 플랫폼에 배포할 수 있는 편리한 인터페이스를 제공합니다.

본 실습에서는 Docker의 기본 사항과 단일 머신의 Local 환경에서 Docker를 사용하는 방법에 대해 알아보겠습니다. AWS의 개발용 워크스페이스인 Cloud9 내에서 진행하겠습니다.

## Docker 알아가기
먼저 AWS Cloud9 워크스페이스에 Docker가 설치되어 있는지 확인하고, 웹 서버 `nginx`의 표준 컨테이너 이미지를 다운로드하고 실행합니다.

1. `docker --version` 명령어를 실행하여 클라이언트와 서버가 모두 있고 작동하는지 확인합니다.
```bash
$ docker --version
```

2. Docker 컨테이너는 이미지를 사용하여 빌드됩니다. 먼저 `docker pull nginx:latest` 명령어를 실행하여 Docker Hub에서 `nginx`의 신뢰할 수 있는 최신 이미지를 다운로드합니다.
```bash
$ docker pull nginx:latest
```

3. 이미지가 로컬 머신의 Docker 캐시에 있는지 확인하기 위해 `docker images` 명령어를 실행합니다. 이미지가 있으면 컨테이너를 시작할 때 첫 번째로 Docker Hub에서 다운로드할 필요가 없습니다.
```bash
$ docker images
```

4. 이제 `docker run -d -p 8080:80 --name nginx nginx:latest` 명령어를 실행하여 `nginx` 이미지를 백그라운드 데몬으로 인스턴스화합니다. 이 명령어는 호스트의 포트 8080를 컨테이너의 포트 80으로 전달하는 백그라운드 데몬으로 실행됩니다.
```bash
$ docker run -d -p 8080:80 --name nginx nginx:latest
```

5. `docker images` 명령어를 실행하여 이미지가 로컬 머신의 Docker 캐시에 있는지 확인합니다.
```bash
$ docker images
```

6. `docker ps` 명령어를 실행하여 `nginx` 컨테이너가 실행 중인지 확인합니다.
```bash
$ docker ps
```

7. `curl http://localhost:8080` 명령어를 실행하여 `nginx` 컨테이너를 사용하고 기본 `index.html`이 작동하는지 확인합니다.
```bash
$ curl http://localhost:8080
```

8. `docker logs nginx` 명령어를 실행하여 `nginx`에서 생성된 로그를 확인합니다. 몇 차례 `curl` 요청을 보내면 로그가 생성됩니다.
```bash
$ docker logs nginx
```

9. `docker exec -it nginx /bin/bash` 명령어를 실행하여 컨테이너의 파일 시스템에 대한 대화형 쉘을 시작합니다.
```bash
$ docker exec -it nginx /bin/bash
```

10. 컨테이너 내에서 `cd /usr/share/nginx/html` 명령어를 실행하고 `cat index.html` 명령어를 실행하여 `nginx`가 제공하는 컨테이너의 내용을 확인합니다.
```bash
$ cd /usr/share/nginx/html
$ cat index.html
```

11. `exit` 명령어를 실행하여 쉘을 종료합니다.
```bash
$ exit
```

12. `docker stop nginx` 명령어를 실행하여 컨테이너를 중지합니다.
```bash
$ docker stop nginx
```

13. `docker ps -a` 명령어를 실행하여 컨테이너가 여전히 있는지 확인합니다.
```bash
$ docker ps -a
```

14. `docker rm nginx` 명령어를 실행하여 컨테이너를 삭제합니다.
```bash
$ docker rm nginx
```

15. `docker rmi nginx:latest` 명령어를 실행하여 Local 캐시에서 `nginx` 이미지를 삭제합니다.
```bash
$ docker rmi nginx:latest
```

## Building a container image
이 단계에서는 `Dockerfile`을 사용하여 인스턴스에 컨테이너 이미지를 빌드합니다. 이 샘플은 `nginx` 웹 서버가 포함된 이미지를 사용하여 간단한 HTML 페이지를 제공합니다.

1. 먼저 컨테이너 이미지를 위한 작업 디렉토리를 만듭니다.
```bash
$ mkdir ~/environment/container-image
```

2. 해당 폴더로 이동합니다.
```bash
$ cd ~/environment/container-image
```

3. `touch Dockerfile` 명령어를 실행하여 빈 `Dockerfile`을 만듭니다. 이 파일에는 컨테이너 이미지를 빌드하는 데 필요한 일련의 단계가 포함됩니다.
```bash
touch Dockerfile
```

4. 아래 명령어를 실행하여 `Dockerfile` 내용을 업데이트합니다.
```bash
cat <<EOF > Dockerfile
FROM nginx:latest
COPY index.html /usr/share/nginx/html
EOF
```

5. `touch index.html` 명령어를 실행하여 빈 HTML 파일을 만듭니다. 이 파일에는 간단한 메시지가 포함됩니다.
```bash
$ touch index.html
```

6. `echo` 명령어를 사용하여 간단한 메시지를 `index.html` 파일에 입력합니다.
```bash
echo "We've added our own custom content into the container" >> index.html
```

7. `docker build -t nginx:1.0 .` 명령어를 실행하여 `Dockerfile`에서 `nginx` 컨테이너 이미지를 빌드합니다.
```bash
$ docker build -t nginx:1.0 .
```

8. `docker history nginx:1.0` 명령어를 실행하여 `nginx:1.0`이 빌드되는 모든 단계와 기본 컨테이너를 확인합니다. 우리의 변경 사항은 하나의 작은 레이어에 불과하다는 것을 주목하세요.
```bash
$ docker history nginx:1.0
```

9. `docker run -p 8080:80 --name nginx nginx:1.0` 명령어를 실행하여 새로운 컨테이너를 실행합니다. 이번에는 `-d` 옵션을 입력하지 않아 터미널을 통해 컨테이너의 로그를 출력되므로 디버깅에 유용합니다.
```bash
$ docker run -p 8080:80 --name nginx nginx:1.0
```

10. 다른 터미널 탭을 엽니다. (Window -> New Terminal)

11. 다른 터미널 탭에서 `curl http://localhost:8080` 명령어를 실행하여 새로운 컨테이너의 내용을 확인합니다.
```bash
$ curl http://localhost:8080
```

12. 첫 번째 터미널 탭으로 돌아가서 로그 출력(STDOUT)을 확인합니다.

13. 이제 Docker Hub 또는 Amazon ECR과 같은 프라이빗 레지스트리에 푸시할 수 있습니다. 이에 대해서는 나중에 더 자세히 알아보겠습니다.

14. `Ctrl-C` 명령어를 실행하여 로그 출력을 종료합니다. 컨테이너가 중지되었지만 `docker ps -a` 명령어를 실행하여 여전히 있는지 확인합니다.
```bash
$ docker ps -a
```

15. `sudo docker inspect nginx` 명령어를 실행하여 중지된 컨테이너에 대한 많은 정보를 확인합니다.
```bash
$ sudo docker inspect nginx
```

16. 이전과 마찬가지로 `docker rm nginx` 명령어를 실행하여 컨테이너를 삭제합니다.
```bash
$ docker rm nginx
```

17. 이번엔 파일을 이미지에 포함시키는 대신 호스트에서 파일을 마운트하여 컨테이너에 탑재합니다.
```bash
$ docker run -d -p 8080:80 -v /home/ec2-user/environment/container-image/index.html:/usr/share/nginx/html/index.html\:ro --name nginx nginx:latest
```

18. 이제 `curl http://localhost:8080` 명령어를 실행하여 컨테이너의 내용을 확인합니다. 이번에는 이미지가 Docker Hub에서 제공하는 기본 `nginx` 이미지이지만 컨테이너의 내용이 있습니다.
```bash
$ curl http://localhost:8080
```

19. `index.html` 파일을 편집하고 몇 가지 추가 사항을 추가합니다.
```bash
echo "This is another line I've added to my container" >> index.html
```

20. 다른 터미널 탭에서 `curl http://localhost:8080` 명령어를 실행하여 컨테이너의 내용을 확인합니다. 이미지 재실행 없이 변경 사항이 반영된 것을 확인할 수 있습니다.
```bash
$ curl http://localhost:8080
```

21. 마지막으로, `docker stop nginx` 명령어와 `docker rm nginx` 명령어를 실행하여 마지막 컨테이너를 중지하고 삭제합니다.
```bash
$ docker stop nginx && docker rm nginx
```