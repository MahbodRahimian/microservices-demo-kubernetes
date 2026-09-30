FROM nexuss.mahbod.com:8082/online-boutique/shoppingassistant-deps:3.0

ENV PYTHONUNBUFFERED=1

WORKDIR /shoppingassistantservice

COPY . .

ENV PORT=8080

EXPOSE 8080

ENTRYPOINT ["python", "shoppingassistantservice.py"]