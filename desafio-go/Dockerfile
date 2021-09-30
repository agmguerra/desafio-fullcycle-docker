## stage 1
FROM golang:1.17.1-alpine as builder

WORKDIR /app

### Copy Go application dependency files
COPY go.mod .
COPY main.go .

### CGO has to be disabled cross platform builds
### Otherwise the application won't be able to start
ENV CGO_ENABLED=0

### Build the Go app for a linux OS
### 'scratch' and 'alpine' both are Linux distributions
RUN GOOS=linux go build ./main.go

## stage 2
FROM scratch

WORKDIR /app

### Copy built binary application from 'builder' image
COPY --from=builder /app/main .

### Run the binary application
CMD ["./main"]

