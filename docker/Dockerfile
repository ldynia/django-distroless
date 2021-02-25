FROM python:3.7.9-alpine AS BUILDER

WORKDIR /app
COPY . /app

RUN pip install -r requirements.txt
RUN rm -f requirements.txt

# Distroless python3
FROM gcr.io/distroless/python3-debian10

ARG PORT=8000
ENV PORT=$PORT

ENV HOME=/app
ENV PYTHONUNBUFFERED=True
ENV PYTHONPATH=/usr/lib/python3.7/site-packages

COPY --from=BUILDER /app /app
COPY --from=BUILDER /usr/local/lib/python3.7/site-packages /usr/lib/python3.7/site-packages

WORKDIR /app

EXPOSE ${PORT}
VOLUME /app

CMD ["/app/manage.py", "runserver", "0.0.0.0:8000"]