FROM python:3.9-slim-buster

EXPOSE 8081

COPY requirements.txt .
RUN pip install -r requirements.txt

COPY . .
WORKDIR /app

ENTRYPOINT ["streamlit", "run", "app.py", "--server.port=8081", "--server.address=54.237.47.95"]