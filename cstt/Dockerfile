FROM sirius1242/bam:alpine3.4 AS builder
WORKDIR /build
RUN git clone --depth=1 --single-branch --branch master https://github.com/Siile/CSTT.git
RUN cd CSTT && bam config && bam server_release

FROM alpine:3.4
WORKDIR /srv
COPY --from=builder /build/CSTT/teeworlds_srv .
COPY --from=builder /build/CSTT/data/maps/ maps
COPY --from=builder /build/CSTT/autoexec-cstt.cfg autoexec.cfg
COPY --from=builder /usr/lib/libgcc_s.so.1 /usr/lib/libstdc++.so.6 /usr/lib/
CMD ["./teeworlds_srv"]
