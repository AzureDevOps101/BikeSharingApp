FROM azuredevops101.azurecr.cn/lib/golang:1.8

COPY . /go/src/app
WORKDIR /go/src/app
RUN go get -d -v
RUN go install -v

EXPOSE 80

ENTRYPOINT ["app"]