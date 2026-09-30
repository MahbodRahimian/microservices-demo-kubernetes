FROM nexuss.mahbod.com:8082/online-boutique/recommendationservice-deps:1.0

ENV PYTHONUNBUFFERED=1

WORKDIR /recommendationservice

COPY . .

ENV PORT=8080

EXPOSE 8080

ENTRYPOINT ["python", "recommendation_server.py"]