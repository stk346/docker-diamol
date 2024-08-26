FROM diamol/maven AS builder

WORKDIR /usr/src/iotd
COPY pom.xml .
RUN mvn -B dependency:go-offline

# 루트 디렉토리의 모든 파일, 디렉토리를 워킹 디렉토리로 복사
COPY . .
# 메이븐 패키징 -> jar파일 생성
RUN mvn package

# app
FROM diamol/openjdk

# builder 레이어의 jar 파일을 현재 레이어의 워킹디렉토리로 복사
WORKDIR /app
COPY --from=builder /usr/src/iotd/target/iotd-service-0.1.0.jar .

EXPOSE 80
# 명령어: java이고 뒤의 파라미터를 실행. 컨테이너가 실행되면 해당 명령어가 항상 실행속
ENTRYPOINT ["java", "-jar", "/app/iotd-service-0.1.0.jar"]