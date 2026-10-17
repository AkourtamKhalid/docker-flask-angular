
FROM python:3.12-slim
WORKDIR /app


COPY requirements.txt .
RUN pip install --no-cache-dir -r requirements.txt
COPY . .

ENV FLASK_APP=app.py \
    FLASK_RUN_HOST=0.0.0.0 \
    FLASK_RUN_PORT=8081 \
    PYTHONUNBUFFERED=1


RUN useradd --create-home appuser
USER appuser

EXPOSE 8081
CMD ["flask", "run"]

