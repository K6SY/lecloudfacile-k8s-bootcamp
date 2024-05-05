# Utilisation d'une image de base python
FROM python:3.10.14-alpine

ENV HOME=/app

# Définition de variable d'environnement
ENV PYTHONDONTWRITEBYTECODE 1
ENV PYTHONUNBUFFERED 1

# Set the working directory in the container
WORKDIR ${HOME}

COPY requirements.txt ${HOME}/requirements.txt
RUN pip3 install -r ${HOME}/requirements.txt
COPY app/ ${HOME}/

EXPOSE 8000
CMD ["gunicorn","--workers=1" ,"--timeout=3600", "--bind", "0.0.0.0:8000","app:app"]