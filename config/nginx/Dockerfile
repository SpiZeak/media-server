FROM ubuntu:latest

WORKDIR /src

RUN apt update && \
	apt upgrade -y

RUN apt install -y libpcre3 libpcre3-dev zlib1g zlib1g-dev openssl libssl-dev wget git gcc make libbrotli-dev

RUN wget https://nginx.org/download/nginx-1.25.1.tar.gz && tar -zxf nginx-1.25.1.tar.gz

RUN git clone https://github.com/google/ngx_brotli

RUN rm -rf /etc/nginx

RUN cd nginx-1.25.1 && ./configure \
	--add-dynamic-module=../ngx_brotli \
	--with-cc-opt='-g -O2 -ffile-prefix-map=/build/nginx-quic-fF80uJ/nginx-quic-1.25.1=. -flto=auto -ffat-lto-objects -flto=auto -ffat-lto-objects -fstack-protector-strong -Wformat -Werror=format-security -fPIC -Wdate-time -D_FORTIFY_SOURCE=2' \
	--with-ld-opt='-Wl,-Bsymbolic-functions -flto=auto -ffat-lto-objects -flto=auto -Wl,-z,relro -Wl,-z,now -fPIC' \
	--with-ld-opt='/usr/lib/aarch64-linux-gnu/libssl.a /usr/lib/aarch64-linux-gnu/libcrypto.a' \
	--prefix=/usr/share/nginx \
	--conf-path=/etc/nginx/nginx.conf \
	--http-log-path=/var/log/nginx/access.log \
	--error-log-path=/var/log/nginx/error.log \
	--lock-path=/var/lock/nginx.lock \
	--pid-path=/run/nginx.pid \
	--modules-path=/usr/lib/nginx/modules \
	--http-client-body-temp-path=/var/lib/nginx/body \
	--http-fastcgi-temp-path=/var/lib/nginx/fastcgi \
	--http-proxy-temp-path=/var/lib/nginx/proxy \
	--http-scgi-temp-path=/var/lib/nginx/scgi \
	--http-uwsgi-temp-path=/var/lib/nginx/uwsgi \
	--with-debug \
	--with-pcre-jit \
	--with-http_ssl_module \
	--with-http_stub_status_module \
	--with-http_realip_module \
	--with-http_auth_request_module \
	--with-http_v2_module \
	--with-http_v3_module \
	--with-http_dav_module \
	--with-http_slice_module \
	--with-threads \
	--with-file-aio \
	--with-http_addition_module \
	--with-http_gunzip_module \
	--with-http_gzip_static_module \
	--with-http_sub_module \
	&& make && make install

COPY ./dhparam2048.pem /etc/nginx

RUN mkdir -p /var/lib/nginx/{body,fastcgi}

ENV PATH="$PATH:/usr/share/nginx/sbin"
