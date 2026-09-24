FROM python:3.12-alpine AS builder

COPY requirements.txt .

RUN pip install --prefix="/install" --no-cache-dir -r requirements.txt

FROM python:3.12-alpine

WORKDIR /loadgen

COPY --from=builder /install /usr/local
COPY locustfile.py .

ENV GEVENT_SUPPORT=True

ENTRYPOINT ["sh", "-c", "locust --host=http://${FRONTEND_ADDR} --headless -u ${USERS:-10} -r ${RATE:-1}"]