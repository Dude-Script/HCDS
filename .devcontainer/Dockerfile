FROM mcr.microsoft.com/devcontainers/base:debian-11

ENV PYTHONUNBUFFERED 1

RUN apt-get update && export DEBIAN_FRONTEND=noninteractive \
    && apt-get -y install --no-install-recommends postgresql-client python3-pip \
    && apt-get clean -y && rm -rf /var/lib/apt/lists/*

WORKDIR /app

COPY src/backend/pyproject.toml src/backend/requirements.txt ./
RUN pip install --upgrade pip && pip install -r requirements.txt

COPY src/backend ./

# Add main.py entrypoint wrapper
COPY src/backend/main.py ./

EXPOSE 8080

CMD ["uvicorn", "main:app", "--host", "0.0.0.0", "--port", "8080"]
