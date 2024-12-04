FROM golang:1.23-alpine AS builder

WORKDIR /app

COPY go.mod go.sum ./

RUN go mod download && go mod verify && go mod tidy

COPY . .

RUN go build -v -o /go-app ./cmd/server/main.go

RUN ls -l /app

FROM alpine:latest

WORKDIR /app

COPY --from=builder /go-app /go-app

EXPOSE 8080

CMD ["/go-app"]
