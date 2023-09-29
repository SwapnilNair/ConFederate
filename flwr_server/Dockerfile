FROM --platform=$BUILDPLATFORM python:3.10-alpine AS builder

RUN echo "FEDERATIUM : Running server node;"

WORKDIR /app

COPY requirements.txt /app

RUN apk update && apk add --no-cache gcc g++ python3-dev unixodbc-dev

RUN apk add dig && dig pypi.org

RUN /usr/local/bin/python -m pip install --upgrade pip

RUN pip install --trusted-host pypi.org --trusted-host files.pythonhosted.org -r requirements.txt

COPY . /app

ENTRYPOINT ["python3"]
CMD ["app.py"]

FROM builder as dev-envs

RUN addgroup -S docker && adduser -S --shell /bin/bash --ingroup docker vscode
# install Docker tools (cli, buildx, compose)
COPY --from=gloursdocker/docker / /