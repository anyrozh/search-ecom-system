ЗАПУСК ПРОЕКТА
---

### 1. Запуск Qdrant в Docker

```
# 1.1. Скачивание образа
docker pull qdrant/qdrant

# 1.2. Запуск контейнера
docker run -d --name qdrant -p 6333:6333 qdrant/qdrant

# 1.3. Остановка и удаление контейнера (после тестирования)
docker rm -f qdrant
docker rmi qdrant/qdrant

# 1.4. Повторный запуск существующего контейнера
docker start qdrant
```

### 2. Запуск ноутбука для тестирования

```
jupyter notebook search_project_up.ipynb

(в скрипт добаить gpt и api-ключ для запуска)
```
