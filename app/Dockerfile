FROM python:3.8-alpine3.10

WORKDIR /app
COPY requirements.txt /requirements.txt
COPY . . 
RUN pip install -r requirements.txt

EXPOSE 80/tcp
CMD ["python", "app/main.py"]
