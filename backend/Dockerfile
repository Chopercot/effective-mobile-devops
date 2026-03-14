FROM python:3.12-slim

# создаём пользователя и группу
RUN groupadd -r appgroup && useradd -r -g appgroup appuser

# рабочая директория
WORKDIR /app

# копируем приложение
COPY app.py .

# меняем владельца файлов
RUN chown -R appuser:appgroup /app

# переключаемся на пользователя
USER appuser

# документируем порт
EXPOSE 8080

# запуск приложения
CMD ["python3", "app.py"]
