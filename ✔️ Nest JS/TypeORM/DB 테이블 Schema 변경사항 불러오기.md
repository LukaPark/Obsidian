
typeorm-model-generator 를 사용.

# entity 파일 생성 명령어

-h : host, 연결할 서버 ip

-d : database, 연결할 db 이름

-p : port, 연결할 서버 port

-u : user, db 사용자 id

-x : db 사용자 패스워드

-e : engine, db 종류 (mssql, postgres, mysql, mariadb, oracle, sqlite)

-o : out, entity 파일 생성할 폴더 경로

```cli
yarn typeorm-model-generator -h [host] -d [dbname] -p [portnumber] -u [userid] -x [password] -e [enginename] -o [directory]
```