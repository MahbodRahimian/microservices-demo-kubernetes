FROM nexuss.mahbod.com:8082/base/python:3.12.6-slim AS base

FROM base AS builder

COPY requirements.txt .

RUN pip install --prefix="/install" -r requirements.txt

FROM base

WORKDIR /loadgen

COPY --from=builder /install /usr/local
COPY locustfile.py .

ENV GEVENT_SUPPORT=True

ENTRYPOINT ["sh", "-c", "locust --host=http://${FRONTEND_ADDR} --headless -u ${USERS:-10} -r ${RATE:-1}"]