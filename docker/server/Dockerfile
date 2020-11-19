FROM golang:1.14-alpine as build

WORKDIR /app

# Copy go mod and sum files
COPY go.mod ./

# Download all dependencies. Dependencies will be cached if the go.mod and go.sum files are not changed
RUN go mod download
RUN go mod verify

# Copy the source from the current directory to the Working Directory inside the container
COPY . .

RUN go build -o main github.com/savvailyin/changeme/cmd

#
# STAGE 3: run
#
FROM alpine:latest

RUN apk update && apk add tzdata

COPY --from=build /app/main .

COPY config.yml .

EXPOSE 8097

ENTRYPOINT ["/main", "RECPRICE"]