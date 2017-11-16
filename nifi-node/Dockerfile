FROM apache/nifi:1.4.0

LABEL maintainer="Truoc Pham <https://hub.docker.com/u/truocpham/>"

ADD ./nifi.properties conf
ADD ./start-nifi.sh .

CMD ["./start-nifi.sh"]
