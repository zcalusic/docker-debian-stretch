FROM golang:buster as builder
MAINTAINER Zlatko Čalušić <zcalusic@bitsync.net>

ARG RCLONE_VERSION

ENV CGO_ENABLED 0

RUN go install --ldflags "-s -X github.com/rclone/rclone/fs.Version=$RCLONE_VERSION" "github.com/rclone/rclone@$RCLONE_VERSION"

FROM zcalusic/debian-buster
MAINTAINER Zlatko Čalušić <zcalusic@bitsync.net>

ARG URL
ARG VCS_URL
ARG VCS_REF
ARG BUILD_DATE

LABEL org.label-schema.name="Rclone in Docker" \
      org.label-schema.description="Run Rclone in a Docker container" \
      org.label-schema.vendor="Zlatko Čalušić" \
      org.label-schema.license="MIT" \
      org.label-schema.url=$URL \
      org.label-schema.vcs-url=$VCS_URL \
      org.label-schema.vcs-ref=$VCS_REF \
      org.label-schema.build-date=$BUILD_DATE \
      org.label-schema.schema-version="1.0"

COPY --from=builder /go/bin /usr/bin

CMD [ "rclone" ]
