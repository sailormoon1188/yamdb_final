FROM python:3.7-slim
WORKDIR /app
COPY . .
#если не указать api_yamdb/, то при загрузке на докерхаб ошибка, не может найти requirements.txt
RUN pip3 install -r api_yamdb/requirements.txt --no-cache-dir 
CMD ["gunicorn", "api_yamdb.wsgi:application", "--bind", "0:8000"]