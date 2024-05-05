FROM python:alpine3.19
COPY mkdocs.yml /app/
COPY docs/ app/docs
RUN pip install mkdocs
WORKDIR /app
EXPOSE 8000
CMD ["mkdocs", "serve", "-a", "0.0.0.0:8000"]