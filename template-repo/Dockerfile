FROM python:3.11-slim

WORKDIR /app

# System deps（地理 / DB driver 常用到）
RUN apt-get update && apt-get install -y --no-install-recommends \
    build-essential \
    libpq-dev \
    libgeos-dev \
    && rm -rf /var/lib/apt/lists/*

# Python deps（先 copy requirements 利用 cache）
COPY requirements.txt .
RUN pip install --no-cache-dir -r requirements.txt

# 程式碼
COPY . .

EXPOSE 8501 8000

# Default：跑 streamlit（依需要改）
CMD ["streamlit", "run", "src/serve/dashboard.py", "--server.port=8501", "--server.address=0.0.0.0"]
