# Étape 1 : Builder
FROM python:3.11-slim AS builder

WORKDIR /build

RUN apt-get update && apt-get install -y \
    gcc \
    default-libmysqlclient-dev \
    pkg-config \
    && rm -rf /var/lib/apt/lists/*

# Installation des dépendances de compilation si nécessaire
COPY api/requirements.txt .
RUN pip install --user --no-cache-dir -r requirements.txt

# Étape 2 : Final
FROM python:3.11-slim

WORKDIR /app

# Récupération uniquement des librairies installées à l'étape précédente
COPY --from=builder /root/.local /root/.local
COPY api/ .

# Sécurité : On ne lance jamais l'app en tant que "root"
RUN useradd -m devsecops
USER devsecops

# Variable d'environnement pour que Python trouve les librairies
ENV PATH=/root/.local/bin:$PATH

EXPOSE 5000

CMD ["python", "app.py"]