FROM python:3.12-alpine AS builder

RUN apk add --no-cache wget g++

COPY requirements.txt .

RUN pip install --no-cache-dir -r requirements.txt

FROM python:3.12-alpine

ENV PYTHONUNBUFFERED=1
ENV ENABLE_PROFILER=1

WORKDIR /email_server

COPY --from=builder /usr/local/lib/python3.12/ /usr/local/lib/python3.12/
COPY . .

EXPOSE 8080

ENTRYPOINT ["python", "email_server.py"]