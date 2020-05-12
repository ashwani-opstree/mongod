```
docker rm -f ccm-web-app
docker exec -it ccm-web-app bash
docker run -d -p 8089:8080 --name ccm-web-app --link mongo-ccm-web --link mysql-ccm-web ccm-web-test:v1
docker run -d -p 8089:8080 --name ccm-web-app --link mongo-ccm-web --link mysql-ccm-web ccm-web-test:v1
docker run --name mysql-ccm-web -p 3306:3306 -e MYSQL_DATABASE=stratus -e MYSQL_USER=stratus -e MYSQL_PASSWORD=test -e MYSQL_ROOT_PASSWORD=ccm-web -d mysql:community-server-minimal-5.6.47
docker run -d --name mongo-ccm-web -p 27017:27017 -e MONGODB_ADMIN_PASSWORD=ccm-web -e MONGODB_USER=stratus -e MONGODB_PASSWORD=test -e MONGODB_DATABASE=stratus mongo:3.6
docker run --link mongo-ccm-web -it mongo:3.6 mongo --host mongo-ccm-web -u admin -p ccm-web --authenticationDatabase admin	  
docker run --link mongo-ccm-web -it mongo:3.6 mongo --host mongo-ccm-web -u stratus -p test --authenticationDatabase stratus stratus
```