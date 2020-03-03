# Nginx를 이용한 간단한 Port Forwarding 구성


## Nginx 설치 (ubuntu 16.04 or 18.04)
```
sudo apt-get update
sudo apt install nginx
```

## Nginx config 수정
/etc/nginx/nginx.conf에 아래 내용을 추가합니다.
```
stream {
        server {
                listen      YOUR_LISTEN_PORT;
                proxy_pass  DESTINATION_IP:PORT;
        }
}
```
- YOUR_LISTEN_PORT는 proxy에서 listen할 port로 수정합니다.
- DESTINATION_IP:PORT는 proxy에서 forwarding할 ip와 port로 수정합니다.

## Nginx 실행
```
sudo systemctl restart nginx
```

## 예시
Nginx의 10022 포트로 ssh 접속 시, 리모트 서버(10.10.10.10)의 ssh 서비스로 접근하도록 설정하는 예시입니다.
```
stream {
        server {
                listen      10022;
                proxy_pass  10.10.10.10:22;
        }
}
```
아래와 같이 테스트 합니다.
```
ssh NGINX_SERVER_IP -p 10022 -l DEST_USER_NAME
```
