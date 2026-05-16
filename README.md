## Запуск проекта

### 1. Необходимый файл для тестирования

Для проверки работы используйте ноутбук:  
**`search_project_up.ipynb`**

### 2. Запуск Qdrant в Docker

```bash
2.1. Скачивание образа 
docker pull qdrant/qdrant

2.2. Запуск контейнера

docker run -d --name qdrant -p 6333:6333 qdrant/qdrant

ПРОЕКТ МОЖНО ТЕСТИРОВАТЬ ПОСЛЕ П.2.1 и 2.2

2.3. Остановка и удаление контейнера (после тестирования)

docker rm -f qdrant
docker rmi qdrant/qdrant

2.4. Повторный запуск существующего контейнера
Если контейнер уже создан, но остановлен:

docker start qdrant
