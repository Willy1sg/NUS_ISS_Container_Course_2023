FROM golang:1.21-bookworm AS Builder
WORKDIR /app

COPY go.mod .
COPY go.sum .
COPY main.go .

RUN CGO_ENABLED=true go build -o main ./...

fROM debian:bookworm
WORKDIR /app
COPY --from=builder /app/main .
COPY public public
COPY templates templates

ENV PORT=3000 INSTANCE_NAME="GO Dov Bear" INSTANCE_HASH=abc123

HEALTHCHECK --interval=30s --timeout=5s --retries=3
CMD curl -s htp://localhost:${PORT}/healthz || exit 1