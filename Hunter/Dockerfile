FROM sirius1242/bam:alpine3.4 AS builder
WORKDIR /build
RUN git clone --depth=1 --single-branch --branch 0.6.4-hunter https://github.com/yangfl/teeworlds-hunter.git teeworlds
RUN cd teeworlds && bam config && bam server_release

FROM alpine:3.4
WORKDIR /srv
RUN echo -en 'sv_name unamed hunter server\nsv_map hunter1\nsv_gametype hunter' > autoexec.cfg
COPY --from=builder /build/teeworlds/hunter_srv teeworlds_srv
COPY --from=builder /build/teeworlds/data/maps/ maps
COPY --from=builder /usr/lib/libgcc_s.so.1 /usr/lib/libstdc++.so.6 /usr/lib/
CMD ["./teeworlds_srv"]
