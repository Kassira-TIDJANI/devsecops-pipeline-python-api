# Étape 1 : Builder
FROM python:3.11-slim AS builder

WORKDIR /build

RUN apt-get update && apt-get install -y \
    gcc \
    default-libmysqlclient-dev \
    pkg-config \
    && rm -rf /var/lib/apt/lists/*

COPY requirements.txt .
RUN pip install --no-cache-dir --prefix=/install -r requirements.txt

# Étape 2 : Final
FROM python:3.11-slim

WORKDIR /app

RUN apt-get update && apt-get install -y \
    default-libmysqlclient-dev \
    && rm -rf /var/lib/apt/lists/*

# Sécurité 
RUN useradd -m devsecops

# Récupération uniquement des librairies installées à l'étape précédente
COPY --from=builder --chown=devsecops:devsecops /install /usr/local
COPY --chown=devsecops:devsecops . .

USER devsecops

EXPOSE 5000

CMD [ "flask", "run", "--host=0.0.0.0"]