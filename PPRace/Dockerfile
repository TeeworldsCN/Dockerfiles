FROM sirius1242/bam:alpine3.4 AS builder
WORKDIR /build
RUN git clone --depth=1 --single-branch --branch DDRace https://github.com/TeeworldsCN/teeworlds-pprace.git
RUN cd teeworlds-pprace && bam config && bam server_release

FROM alpine:3.4
WORKDIR /srv
COPY --from=builder /build/teeworlds-pprace/DDRace-Server teeworlds_srv
COPY --from=builder /build/teeworlds-pprace/data/maps/ maps
COPY --from=builder /build/teeworlds-pprace/autoexec.cfg .
COPY --from=builder /usr/lib/libgcc_s.so.1 /usr/lib/libstdc++.so.6 /usr/lib/
CMD ["./teeworlds_srv"]
