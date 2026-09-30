FROM nexuss.mahbod.com:8082/base/python:3.12.7-alpine AS base

FROM base AS builder

RUN apk add --no-cache wget g++

COPY requirements.txt .

RUN pip install "setuptools<81" -r requirements.txt

FROM base

ENV PYTHONUNBUFFERED=1
ENV ENABLE_PROFILER=1

WORKDIR /email_server

COPY --from=builder /usr/local/lib/python3.12/ /usr/local/lib/python3.12/
COPY . .

EXPOSE 8080

ENTRYPOINT ["python", "email_server.py"]