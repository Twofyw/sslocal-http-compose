# sslocal-http-compose
A docker-compose.yml that quickly starts a shadowsocks client with a socks5-to-http proxy converter.
Useful for deploying to a new server or a personal Linux desktop.

This is my first step to dockerizing everything. What's in the queue:
- Jekyll (write a blog)
- Vim (take vim everywhere)
- Borg (automate backup)
- Transmission (steal some resources (\~‾▿‾)\~)
- Firefox with VNC (open a jupypter window on the server so training history is preserved)
- Further projects ([useful?](http://jasonwilder.com/blog/2014/10/13/a-simple-way-to-dockerize-applications/))

## Quick start
Firstly, you need a shadowsocks server :). 

Once you've got that, all you need to do is placing the configuration file under this folder and `docker-compose up -d`. Then the http proxy should be already listening on port 8118 on host XD.

## Components

### Networks
Creates a new docker network _docker\_shadowsocks_.

### Services

#### shadowsocks
Based on shadowsocks/shadowsocks-libev. But instead of starting a shadowsocks server, the CMD is overridden so ss-local is started.

For convenience, the configuration file is bound from a local file as a volume. You should place the configuration file under the same folder and rename it to `config.json`. Note: You should set local listening port to 1080 in config.json.

See the [config file documentation](https://github.com/shadowsocks/shadowsocks/wiki/Configuration-via-Config-File) for reference.

Exposes port 1080 on docker network.

#### privoxy
Converts socks5 proxy to http proxy for compatibility. Exposes port 8118 on host.

