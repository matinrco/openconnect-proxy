# openconnect-proxy docker image

Packages an OpenConnect VPN client with an authenticating HTTP proxy to provide 
access to the VPN via the proxy. 

Example usage:
```bash
# docker run --privileged -it -p 8123:8123 -v /tmp/oc.pw:/tmp/oc.pw -e OPENCONNECT_PASSWORD_FILE=/tmp/oc.pw -e OPENCONNECT_USERNAME=oc_user -e OPENCONNECT_GROUP=oc_group -e OPENCONNECT_HOST=vpn.example.com -e PROXY_USERNAME=puser -e PROXY_PASSWORD=secret matinrco/openconnect-proxy
```

Substitute the real values for your AnyConnect VPN credentials in place of oc_user, oc_group, and vpn.example.com; and create a file (in this case `/tmp/oc.pw`) containing the associated password.

While the above container is running, you should be able to use the docker host an http proxy to access resources via the VPN. 

For example, you could set an http_proxy environment variable and use wget:
```bash
# export http_proxy=http://puser:secret@dockerhost.example.com:8123/
# wget http://protectedhost.example.com/
```

Available environment variables :
```bash
PROXY_USERNAME
PROXY_PASSWORD

OPENCONNECT_PASSWORD
OPENCONNECT_PASSWORD_FILE
OPENCONNECT_USERNAME
OPENCONNECT_GROUP
OPENCONNECT_HOST
OPENCONNECT_NO_CERT_CHECK
```

<i>Note 
* Proxy authentication is optional . if you don't want any authentication just don't pass username/password.
* You need to provide openconnect password with just one method . In a file or fill the related env var.
* If your openconnect server doesn't provide valid certificate , pass `OPENCONNECT_NO_CERT_CHECK=true` to ignore certificate check.
* `OPENCONNECT_GROUP` is also optional.
</i>