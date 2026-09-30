FROM nexuss.mahbod.com:8082/online-boutique/emailservice-deps:1.0

ENV PYTHONUNBUFFERED=1
ENV ENABLE_PROFILER=1

WORKDIR /email_server

COPY . .

EXPOSE 8080

ENTRYPOINT ["python", "email_server.py"]