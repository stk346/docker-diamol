### ch6.1 컨테이너 속 데이터가 사라지는 이유
  * 컨테이너 두 개 실행
    * docker container run --name rn1 diamol/ch06-random-number
    * docker container run --name rn2 diamol/ch06-random-number
  * 위 두 컨테이너에서 무작위 숫자가 쓰인 파일 복사 -> 두 파일의 내용이 다름
    * docker container cp rn1:/random/number.txt number1.txt
    * docker container cp rn2:/random/number.txt number2.txt    

### ch6.2 도커 볼륨을 사용하는 컨테이너 실행하기
  * 타겟 디렉터리로 이동
    * cd doto-list  
  
  * todo-list 애플리케이션 이미지로 컨테이너를 실행해 컨테이너와 연결된 볼륨 살펴보기
    * docker container run --name todo1 -d -p 8010:80 diamol/ch06-todo-list
    * docker container inspect --format '{{.Mounts}}' todo1
    * docker volume ls  
  
  * to-do 애플리케이션의 두 번째 컨테이너 실행하고 todo1과 볼륨 공유
    * docker container run --name todo2 -d diamol/ch06-todo-list
    * docker container exec todo2 ls /data
    * docker container run -d --name t3 --volumes-from todo1 diamol/ch06-todo-list
    * docker container exec t3 ls /data  
  
  * 특정 컨테이너만 접근할 수 있는 볼륨 만들기
    * target='/data'
    * docker volume create todo-list
      * 데이터를 저장할 볼륨 생성
    * docker container run -d -p 8011:80 -v todo-list:$target --name todo-v1 diamol/ch06-todo-list
      * 볼륨을 연결해 v1 애플리케이션 실행
    * http://localhost:8081에서 데이터 몇 건 추가
    * docker container rm -f todo-v1
      * v1 애플리케이션이 실행 중인 컨테이너 삭제
    * docker container run -d -p 8011:80 -v todo-list$target --name todo-v2 diamol/ch06-todo-list
      * 같은 볼륨을 사용하도록 v2 애플리케이션 컨테이너 실행

### ch6.3 파일 시스템 마운트를 사용하는 컨테이너 실행하기 
  * 호스트 컴퓨터의 로컬 디렉터리를 컨테이너에 바인드 마운트하기
    * source="$(pwd)/databases" && target='/data'
    * mkdir ./databases
    * docker container run --mount type=bind,source=$source,target=$target -d -p 8012:80 diamol/ch06-todo-list
    * curl http://localhost:8012
      * 요청을 보내면 애플리케이션이 시작되며 데이터베이스 파일이 생성됨
    * ls ./databases