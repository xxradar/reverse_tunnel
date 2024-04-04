# reverse_tunnel
https://github.com/snsinfu/reverse-tunnel/blob/master/docker/README.md

## On the server side
```
docker run -it \
  -p 8080:8080 -p 9000:9000 -p 9090:9090 \
  -e RTUN_AGENT="8080/tcp,9090/tcp  @ samplebfeeb1356a458eabef49e7e7" \
  snsinfu/rtun-server
```
```
curl 192.168.0.157:8080
```
```
curl 192.168.0.157:9090
```
## On the agent side 
```
docker run -d -p 8080:80 nginx
```
```
docker run -d -p 9090:80 nginx
```
```
docker run -it --network host \
  -e RTUN_GATEWAY="ws://192.168.0.157:9000" \
  -e RTUN_KEY="samplebfeeb1356a458eabef49e7e7"   \
  -e RTUN_FORWARD="8080/tcp:localhost:8080,9090/tcp:localhost:9090"   \
  snsinfu/rtun
```
