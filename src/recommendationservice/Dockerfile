FROM python:3.12-alpine AS builder

RUN apk add --no-cache wget g++

COPY requirements.txt .

RUN pip install --no-cache-dir -r requirements.txt

FROM python:3.12-alpine

ENV PYTHONUNBUFFERED=1

WORKDIR /recommendationservice

COPY --from=builder /usr/local/lib/python3.12/ /usr/local/lib/python3.12/
COPY . .

ENV PORT=8080

EXPOSE 8080

ENTRYPOINT ["python", "recommendation_server.py"]