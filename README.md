# Commands

1. Start a Consul server:

    ```shell
    # consul agent -server -bootstrap-expect 1 -data-dir /var/lib/consul -config-dir /etc/consul/conf.d -bind 0.0.0.0 -advertise 192.168.33.10 -client 0.0.0.0 -ui
    ```

2. Start a Consul agent:

    ```shell
    # consul agent -retry-join 192.168.33.10 -client 0.0.0.0 -bind 0.0.0.0 -data-dir /var/lib/consul -datacenter qlapa-prod -config-dir /etc/consul/conf.d -enable-script-checks -advertise <vagrant box ip address>
    ```

3. Render nginx template:

    ```shell
    # consul-template -template "/etc/consul-template.d/nginx-vhost.conf.ctmpl:/etc/nginx/sites-enabled/default:nginx -s reload" -once
    ```

    ```shell
    # consul-template -template "/etc/consul-template.d/nginx-vhost.conf.ctmpl:/etc/nginx/sites-enabled/default:nginx -s reload"
    ```

# Project Structure

```
.
├── consul-vagrant						> vagrant box as consul server
│   └── Vagrantfile
├── nginx-vagrant
│   ├── Vagrantfile
│   └── nginx-vhost.conf.ctmpl 			> nginx configuration template will render by consul-template
└── nodes
    ├── Vagrantfile 					> create 5 vagrant boxes with 512m each box
    └── webserver.json 					> service definition and health check
```