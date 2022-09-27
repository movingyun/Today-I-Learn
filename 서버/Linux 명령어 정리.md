# Linux 명령어 정리

## 디렉토리 조회
```
# 현재 디렉토리 위치
pwd

# 디렉토리로 이동
cd 디렉토리

# 현재 디렉토리 조회
ls 

# 현재 디렉토리 조회 (숨김 파일 포함)
ls -a

# 현재 디렉토리 상세 조회 (숨김 파일 포함)
ls -l

# 현재 디렉토리 수정시간순(내림차순) 상세조회
ls -alt

# 현재 디렉토리 수정시간순(오름차순) 상세조회
ls -alrt

# home 디렉토리의 숨긴파일 찾기
ls -a /home | grep '^\.'
```

## 파일 & 디렉토리 - Create Delete Copy Move Edit
```
# 파일 삭제
rm 파일이름

# 파일 강제 삭제
rm -f 파일이름

# 디렉토리 삭제
rm -r 디렉토리이름

# 디렉토리 강제 삭제
rm -rf 디렉토리이름

# 파일 : test.sh 를 real.sh 이라는 이름으로 복사
ex) cp test.sh real.sh

# 디렉토리 : test 를 real 이라는 이름으로 복사
cp -r test real

# 파일 & 디렉토리 이동 : test.sh 파일을 /home/real 디렉토리로 이동
mv test.sh /home/real

# 파일 & 디렉토리 이름 변경 : test 디렉토리를 real 디렉토리로 변경
mv test real

# test 디렉토리 생성
mkdir test

# test 디렉토리가 비어있다면 삭제
rmdir test
```

## 압축
```
# test 디렉토리를 tar 파일로 압축
tar -cvf test.tar test

# test 디렉토리를 tar.gz 파일로 압축
tar -zcvf test.tar.gz test

# tar 파일 압축 해제
tar -xvf test.tar

#  tar.gz 파일 압축 해제
tar -zxvf test.tar.gz

# zip 파일 압축 해제
unzip test.zip 
```

## 네트워크
```
## netstat

# established 상태만 출력
netstat

# 모든 네트워크 출력
netstat -a

# 도메인주소를 숫자로로 출력
netstat -n

# tcp 프로토콜만 출력
netstat -t

# pid 출력
netstat -p

# 연결 대기 시간 출력
netstat -o

# 가장 자주 쓰는 netstat 옵션...
netstat -antp

#  listen 중인 포트를 찾고자 할때
netstat –anp | grep -i listen

#  80포트를 찾고자 할때
netstat -anp | grep :80

# 2182 와 9092 포트를 한번에 찾을때
netstat -anp | grep -E ":2181|:9092"

# 현재 80포트의 동시 접속자 수
netstat -nap | grep :80 | grep -i establishged | wc -l

# 네트워크 인터페이스 확인
ifconfig
```

## 탐색
```
#  현재 디렉토리에서 탐색
find .

# 현재 디렉토리에서 이름이 test 인 것을 탐색
find . -name test 

# home 디렉토리에서 대소문자 구별없이 test 가 포함된 것에 대한 탐색
find /home -iname  '*test*'

# home 디렉토리에서 test.png 으로 끝나는 파일을 탐색
find /home -name '*test.png' -type f

# home 디렉토리에서 test로 시작하는 디렉토리를 탐색
find /home -name 'test*' -type d

# home 디렉토리에서 test가 들어간 디렉토리를 찾고, 하위 디렉토리는 출력하지 않는다.
find /home -name '*test*' -prune
```

## 기타
```
# Nginx 상태 확인
systemctl status nginx.service

# 8080포트 죽이기
sudo kill $(sudo lsof -t -i:8080)

# pid에 해당하는 프로세스 정상 종료 ( 데몬 프로세스를 종료할때 사용 ) 
kill -15 pid

# BackEnd 파일 빌드
./gradlew clean build

# 빌드된 Back end파일 실행
nohup java -jar [jar파일이름].jar &

#  pid에 해당하는 프로세스 강제 종료 ( graceful 하지 못한 방식이기에 선호하지 않는다... )
kill -9 pid
```