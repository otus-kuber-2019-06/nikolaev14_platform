FROM python:3.6.0-alpine
COPY app/homework.html /var/www/
WORKDIR /var/www/
EXPOSE 8000
USER 1001
CMD ["python3", "-m", "http.server", "8000"]
