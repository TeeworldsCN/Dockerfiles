FROM sirius1242/bam:alpine3.4 AS builder
WORKDIR /build
RUN sed -i 's/dl-cdn.alpinelinux.org/mirrors.ustc.edu.cn/g' /etc/apk/repositories
RUN apk update && apk upgrade
RUN apk add --no-cache libmaxminddb-dev
RUN git clone --depth=1 --single-branch --branch custom https://github.com/sirius1242/teeworlds-infclassR.git teeworlds
RUN git clone --depth=1 --single-branch --branch master https://github.com/necropotame/teeworlds-infclass.git oldinf
RUN cd teeworlds && bam config && bam server_release

FROM alpine:3.4
WORKDIR /srv
COPY --from=builder /build/teeworlds/bin/server teeworlds_srv
COPY --from=builder /build/teeworlds/bin/data/maps/ /build/oldinf/data/maps/ maps/
COPY --from=builder /build/teeworlds/bin/data/languages/ languages/
COPY --from=builder /build/teeworlds/autoexec.cfg /build/teeworlds/bin/GeoLite2-Country.mmdb ./
COPY --from=builder /usr/lib/libgcc_s.so.1 /usr/lib/libstdc++.so.6 /usr/lib/libicui18n.so.57 /usr/lib/libicuuc.so.57 /usr/lib/libicudata.so.57 /usr/lib/libmaxminddb.so.0 /usr/lib/
CMD ["./teeworlds_srv"]
