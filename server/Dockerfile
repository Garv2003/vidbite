FROM python:3.12-slim
WORKDIR /app
COPY requirements.txt .
RUN pip install --no-cache-dir -r requirements.txt
COPY . .
# Bind to $PORT (hosts like Render/Fly inject it); default 8907 for local.
ENV PORT=8907
EXPOSE 8907
CMD ["sh", "-c", "gunicorn --bind 0.0.0.0:${PORT} 'app:create_app()'"]
