FROM python:3.12-slim

WORKDIR /app

# зависимости
COPY requirements.txt .
RUN pip install --no-cache-dir -r requirements.txt

# код приложения
COPY . .

# переменные окружения
ENV FLASK_APP=flaskr
ENV FLASK_ENV=production

CMD ["flask", "run", "--host=0.0.0.0"]
