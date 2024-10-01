# Stage 1: Build the Go application
FROM golang:1.20 AS builder

WORKDIR /app

# Copy go mod and sum files
COPY go.mod go.sum ./

# Download all dependencies
RUN go mod download

# Copy the source code into the container
COPY hello_world.go .

# Build the application
RUN CGO_ENABLED=0 GOOS=linux go build -a -installsuffix cgo -o hello_world .

# Stage 2: Create the final, minimal image
FROM alpine:3.14

WORKDIR /root/

# Copy the binary from the builder stage
COPY --from=builder /app/hello_world .

# Command to run the executable
CMD ["./hello_world"]
