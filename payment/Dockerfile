FROM python:3.9-slim

WORKDIR /app

COPY requirements.txt .
RUN pip install --no-cache-dir -r requirements.txt

COPY payment.ini .
COPY *.py .

EXPOSE 8080

CMD ["uwsgi", "--ini", "payment.ini"]