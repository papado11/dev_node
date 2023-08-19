# Dockerfile

```
FROM node:latest
WORKDIR /app
COPY ./build /app
EXPOSE 8000
CMD ["node","start"]
```

```shell
docker build -t my/sd:1.0 -f dockerfile build
```