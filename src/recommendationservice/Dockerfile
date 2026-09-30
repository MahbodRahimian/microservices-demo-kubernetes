FROM nexuss.mahbod.com:8082/base/python:3.12.8-alpine AS base

FROM base AS builder

RUN apk add --no-cache wget g++

COPY requirements.txt .

RUN pip install "setuptools<81" -r requirements.txt

FROM base

ENV PYTHONUNBUFFERED=1

WORKDIR /recommendationservice

COPY --from=builder /usr/local/lib/python3.12/ /usr/local/lib/python3.12/
COPY . .

ENV PORT=8080

EXPOSE 8080

ENTRYPOINT ["python", "recommendation_server.py"]