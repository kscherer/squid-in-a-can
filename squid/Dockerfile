FROM debian:jessie
RUN apt-get -q update && \
    apt-get -qy --no-install-recommends install python squid3 curl && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/* && \
    sed -i "s/^#acl localnet/acl localnet/" /etc/squid3/squid.conf && \
    sed -i "s/^#http_access allow localnet/http_access allow localnet/" /etc/squid3/squid.conf && \
    mkdir -p /var/cache/squid3 && \
    chown -R proxy:proxy /var/cache/squid3 && \
    curl -sL --insecure -o /bin/dumb-init https://github.com/Yelp/dumb-init/releases/download/v1.0.1/dumb-init_1.0.1_amd64 && \
    chmod +x /bin/dumb-init

ADD deploy_squid.py /tmp/deploy_squid.py

ENTRYPOINT ["/bin/dumb-init"]

CMD ["python", "-u", "/tmp/deploy_squid.py"]
