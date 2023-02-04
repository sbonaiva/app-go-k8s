FROM golang:1.19 AS build

WORKDIR /build

COPY go.mod go.sum ./
RUN go mod download

COPY . ./
RUN go build -o app cmd/app-go-k8s/main.go

FROM gcr.io/distroless/base AS deploy

WORKDIR /

COPY --from=build /build/app ./

EXPOSE 8080

USER nonroot:nonroot

ENTRYPOINT [ "/app" ]