FROM golang:1.18 as builder
ADD go/ /go/example
RUN cd /go/example && go build .

FROM scratch
COPY --from=builder /go/example/example /example

ENTRYPOINT [ "/example" ]
