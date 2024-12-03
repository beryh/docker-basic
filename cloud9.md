# AWS Cloud9 워크스페이스 생성 및 설정
AWS Cloud9은 브라우저만으로 코드를 작성, 실행 및 디버깅할 수 있는 클라우드 기반 IDE(통합 개발 환경)입니다.
> [!CAUTION]
> 현재 AWS Cloud9은 신규 사용자에게 제공되지 않습니다. 해당 서비스는 기존 사용자 및 AWS 실습 참가자에게만 제공됩니다.

## Cloud9 워크스페이스 생성하기

1. AWS Management Console에서 Cloud9으로 이동합니다.

2. "Create environment"를 클릭합니다.

3. 다음과 같이 설정합니다:
   - Name: docker-workspace
   - Environment type: New EC2 instance
   - Instance type: t3.small
   - Platform: Amazon Linux 2
   - Cost-saving setting: After 30 minutes
   - Network settings: Default VPC 사용

4. "Create"를 클릭하여 워크스페이스를 생성합니다.

## Cloud9 워크스페이스 설정하기

1. 워크스페이스가 생성되면 터미널을 엽니다.

2. Docker가 설치되어 있는지 확인합니다:
```bash
docker --version
``` 