# 이미지의 시작점 diamol/node 이미지로부터 시작
FROM diamol/node

ENV TARGET="blog.sixeyed.com"
ENV METHOD="HEAD"
ENV INTERVAL="3000"

WORKDIR /web-ping

# [원본경로] [복사경로] -> app.js 파일을 WORKDIR로 복사
COPY app.js .

# 컨테이너를 실행했을 때 실행할 명령을 지정. node런타임이 애플리케이션을 시작하도록 지정
CMD ["node", "/web-ping/app.js"]