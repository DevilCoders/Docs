error_log nginx_error.log;
worker_processes 6;
daemon off;
pid nginx.pid;

events {
    worker_connections 131072;
    multi_accept on;
}

http {
#    access_log nginx_access.log;
    access_log off;
    tcp_nopush on;
    tcp_nodelay on;
    gzip off;
    client_body_temp_path /tmp/nginx-client-body;
    proxy_temp_path /tmp/nginx-proxy;
    fastcgi_temp_path /tmp/nginx-fastcgi;
    uwsgi_temp_path /tmp/nginx-uwsgi;
    scgi_temp_path /tmp/nginx-scgi;

    server { #200 ok
        listen 8000 reuseport;

        location / {
            echo_read_request_body;
            return 200 "OK";
        }

        location /balancer-health-check {
            echo_read_request_body;
            return 200 "PONG";
        }

        location /awacs-balancer-health-check {
            echo_read_request_body;
            return 200 "PONG";
        }

        location /slb_ping {
            echo_read_request_body;
            return 200 "PONG";
        }
    }

    server { #500 error
        listen 8001 reuseport;

        location / {
            echo_read_request_body;
            return 500 "Internal server error";
        }

        location /balancer-health-check {
            echo_read_request_body;
            return 200 "PONG";
        }

        location /awacs-balancer-health-check {
            echo_read_request_body;
            return 200 "PONG";
        }

        location /slb_ping {
            echo_read_request_body;
            return 200 "PONG";
        }
    }

    server { #laas
        listen 8002 reuseport;

        location /region {
            echo_read_request_body;
            return 200;
            more_clear_headers "Server"
            more_set_headers "X-Region-Id: 213";
            more_set_headers "X-Region-Location: 55.753960, 37.620393, 15000, 1528302650";
            more_set_headers "X-Region-Suspected-Location: 55.753960, 37.620393, 15000, 1528302650";
            more_set_headers "X-Region-City-Id: 213";
            more_set_headers "X-Region-Suspected-City: 213";
            more_set_headers "X-Region-Isp-Code-By-Ip: 0";
            more_set_headers "X-Region-By-IP: 213";
            more_set_headers "X-Region-Is-User-Choice: 0";
            more_set_headers "X-Region-Suspected: 213";
            more_set_headers "X-Region-Should-Update-Cookie: 0";
            more_set_headers "X-Region-Precision: 2";
            more_set_headers "X-Region-Suspected-Precision: 2";
            more_set_headers "X-IP-Properties: EOEBGAAgACgB";
        }

        location /balancer-health-check {
            echo_read_request_body;
            return 200 "PONG";
        }

        location /awacs-balancer-health-check {
            echo_read_request_body;
            return 200 "PONG";
        }

        location /slb_ping {
            echo_read_request_body;
            return 200 "PONG";
        }
    }

    server { #uaas
        listen 8003 reuseport;

        location / {
            echo_read_request_body;
            return 200 "USERSPLIT\n";
            more_clear_headers "Server"
            more_set_headers "X-Yandex-RandomUID: 2382054461528302136";
            more_set_headers "X-Yandex-ExpSplitParams: eyJyIjowLCJzIjoiIiwiZCI6IiIsIm0iOiIiLCJiIjoiIiwiaSI6ZmFsc2V9";
            more_set_headers "X-Yandex-LogstatUID: 2382054461528302136";
            more_set_headers "X-Yandex-ExpConfigVersion: 10566";
        }

        location /balancer-health-check {
            echo_read_request_body;
            return 200 "PONG";
        }

        location /awacs-balancer-health-check {
            echo_read_request_body;
            return 200 "PONG";
        }

        location /slb_ping {
            echo_read_request_body;
            return 200 "PONG";
        }
    }

    server { #clck
        listen 8004 reuseport;

        location /jclck {
            echo_read_request_body;
            return 200 "/* counted */";
            more_clear_headers "Server";
            more_set_headers "Content-Type: text/javascript";
            more_set_headers "Cache-Control: no-cache";
            more_set_headers "X-XSS-Protection: 1; mode=block";
            more_set_headers "X-Content-Type-Options: nosniff";
        }

        location /clck/jsredir {
            echo_read_request_body;
            return 200 "<html><head><meta name=\"referrer\" content=\"always\"/><noscript><META http-equiv=\"refresh\" content=\"0;URL='https://privetmir.ru/'\"></noscript></head><body><script>(function(e){if(/MSIE (\d+\.\d+);/.test(navigator.userAgent)){var t=document.createElement(\"a\");t.href=e;document.body.appendChild(t);t.click()}else{if (navigator.userAgent.indexOf(\"YaBrowser\") > -1) {try{window.opener=null} catch (exc){};}location.replace(e)}})(\"https://privetmir.ru/\")</script></body></html>";
            more_clear_headers "Server";
            more_set_headers "Content-Type: text/html; charset=utf-8";
            more_set_headers "Cache-Control: no-cache";
            more_set_headers "Set-Cookie: i=usFSWhOZMXlLmo0GOFh5oGPYey/zp8LNqikiCvNxotY+fXB/Sa1ASwY1kcOK5ChbRI5x9BmqjojvtlTErauINV+iNAg=; Expires=Sun, 04-Jun-2028 20:32:54 GMT; Domain=.yandex.ru; Path=/; Secure; HttpOnly";
            more_set_headers "X-Content-Type-Options: nosniff";
        }

        location /balancer-health-check {
            echo_read_request_body;
            return 200 "PONG";
        }

        location /awacs-balancer-health-check {
            echo_read_request_body;
            return 200 "PONG";
        }

        location /slb_ping {
            echo_read_request_body;
            return 200 "PONG";
        }
    }

    server { #antirobot
        listen 8005 reuseport;

        location / {
            echo_read_request_body;
            return 200;
            more_clear_headers "Server";
            more_set_headers "X-ForwardToUser-Y: 0";
            more_set_headers "X-Yandex-Internal-Request: 0";
            more_set_headers "X-Yandex-Suspected-Robot: 0";
        }

        location /balancer-health-check {
            echo_read_request_body;
            return 200 "PONG";
        }

        location /awacs-balancer-health-check {
            echo_read_request_body;
            return 200 "PONG";
        }

        location /slb_ping {
            echo_read_request_body;
            return 200 "PONG";
        }
    }
}
