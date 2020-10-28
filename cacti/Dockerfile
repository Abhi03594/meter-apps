FROM python:3.8-alpine3.10
COPY . /chart
COPY requirements.txt /requirements.txt 
RUN pip install -r requirements.txt
WORKDIR /app
EXPOSE 80/tcp
CMD ["python", "main.py"]
