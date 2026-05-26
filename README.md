РЕШАЕМАЯ ПРОБЛЕМА
---

<img width="2752" height="1536" alt="telegram-cloud-document-2-5229078998767671885" src="https://github.com/user-attachments/assets/e799a6b1-9c33-401a-9621-a5484788520b" />


ФУНКЦИОНАЛЬНОСТЬ
---

### Скрипт настраивается и запускается при разных параметрах. На данный момент на git загружен скрипт при запуске которого выводятся наиболее релевантные товары. 

## Эксперименты с настройкой параметров конфигурации

ДАТАСЕТ ДОСТУПЕН ПО ССЫЛКЕ: https://drive.google.com/uc?id=1cDIVIuZjxqEVuqWz_ue0M1CiXrF9UlPx 
ДАТАСЕТ ДЛЯ ТЕСТИРОВАНИЯ ОПРЕДЕЛЁННЫХ ЗАПРОСОВ ДОСТУПЕН ПО ССЫЛКЕ: https://github.com/amazon-science/esci-data/tree/main/shopping_queries_dataset 

В ходе исследования проводились эксперименты с различными значениями параметров конфигурации для оценки их влияния на качество и скорость поиска.

### Параметры конфигурации, которые большего всего влияют на качество проводимых экспериментов

| Параметр | Суть параметра | Вариации настройки |
|----------|----------------|-------------------|
| `max_products` | Максимальное количество товаров из датасета | непрерывное значение (10к - 1 млн строк данных,но будет страдать качество |
| `force_rebuild` | Принудительное перестроение эмбеддингов | `True` (полный пересчёт), `False` (кэш) |
| `clip_model` | Модель CLIP для кодирования изображений | `ViT-B/32`, `ViT-B/16`, `RN50` |
| `st_model` | Sentence Transformer для текста | `clip-ViT-B-32-multilingual-v1`, `all-MiniLM-L6-v2` |
| `rerank_model` | Cross-encoder для переранжирования | `ms-marco-MiniLM-L-6-v2`, `ms-marco-MiniLM-L-12-v2` |
| `sparse_model` | Модель для разреженного поиска BM25 | `Qdrant/bm25` |
| `search_limit` | top-k товаров | непрервыное значение (от 5-10) |
| `taxonomy_limit` | Максимум категорий таксономии | непрервыне значение (от 0-10) |
| `use_reranking` | Включение переранжирования | `True`, `False` |
| `fusion_alpha` | Вес текстового поиска (0-1) | 0.5-0.9 |
| `use_llm` | Использование LLM для расширения запросов | `True`, `False` |
| `temperature` | Разнообразие ответов | 0.0-1 |
| `fusion_dim` | Размерность fusion пространства | 512, 768 |
| `batch_size` | Размер батча при обучении | 16, 32, 64, 128 |
| `epochs` | Количество эпох обучения |  5, 7, 10 |
| `learning_rate` | Скорость обучения | 1e-6, 5e-6, 1e-5, 2e-5, 5e-5 |
| `taxonomy_validation` | Валидация категорий | `True`, `False` |



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



(в скрипт добавить gpt и api-ключ для запуска)
```

НАГЛЯДНЫЕ РЕЗУЛЬТАТЫ ПРОГОНА В РАЗРЕЗЕ КАЖДОГО АЛГОРИТМА. ЛОГИ.
---

папка search_results - logs по неопределённым запросам

ПРИМЕР ПРОГОНА СКРИПТА ПО ОДНОМУ ЗАПРОСУ 
---
Вывод релевантных топов 
<img width="1371" height="546" alt="image" src="https://github.com/user-attachments/assets/c1f1f54e-2891-47c7-8cfc-9ddb73f01245" />


Вывод оценок по релевантным товарам 

<img width="1370" height="557" alt="image" src="https://github.com/user-attachments/assets/ed406dda-d81c-4153-a6da-3bbd67001129" />

Логи метрик

<img width="1156" height="228" alt="image" src="https://github.com/user-attachments/assets/91c4cfcb-e15a-4dce-aa79-caed7193c87b" />



