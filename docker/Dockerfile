FROM python:3.12-alpine

ENV PYTHONDONTWRITEBYTECODE=1 \
    PYTHONUNBUFFERED=1

WORKDIR /app

RUN addgroup -S -g 10001 appgroup && \
    adduser -S -u 10001 -G appgroup -h /app -s /sbin/nologin appuser

COPY requirements/ requirements/
RUN pip install --no-cache-dir -r requirements/prod.txt

COPY --chown=appuser:appgroup app.py .

USER appuser

EXPOSE 8080

CMD ["gunicorn", "--bind", "0.0.0.0:8080", "--workers", "2", "--threads", "2", "--timeout", "30", "--access-logfile", "-", "--error-logfile", "-", "app:app"]
