FROM sirius1242/bam:alpine3.4 AS builder
WORKDIR /build
RUN git clone --depth=1 --single-branch --branch master https://github.com/Siile/KillingFloor.git teeworlds
RUN cd teeworlds && bam config && bam server_release

FROM alpine:3.4
WORKDIR /srv
COPY --from=builder /build/teeworlds/teeworlds_srv /build/teeworlds/autoexec.cfg ./
COPY --from=builder /build/teeworlds/data/maps/ maps
COPY --from=builder /usr/lib/libgcc_s.so.1 /usr/lib/libstdc++.so.6 /usr/lib/
CMD ["./teeworlds_srv"]
