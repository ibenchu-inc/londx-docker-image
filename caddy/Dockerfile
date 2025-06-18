#
# Build stage
#
FROM golang:1.22-alpine AS builder

RUN apk add --no-cache git
RUN go install github.com/caddyserver/xcaddy/cmd/xcaddy@latest

RUN xcaddy build v2.7.6 \
    --with github.com/greenpau/caddy-auth-portal \
    --with github.com/abiosoft/caddy-git \
    --with github.com/filebrowser/caddy@v2.0.3

#
# Final stage
#
FROM caddy:2

COPY --from=builder /go/caddy /usr/bin/caddy
COPY Caddyfile /etc/caddy/Caddyfile
COPY index.html /srv/index.html

EXPOSE 80 443

