# Construction Documentation DevOps

Il est important de co-construire et de partager la docummentation dans nos projets. Ce lab présente MKDocs qui est un générateur de documentation statique, souvent utilisé pour créer des sites Web de documentation à partir de fichiers au format Markdown. Il est dépend de technologie Python.

#### Vérifier que python et pip sont bien installés

```
python --version
pip --version
```

#### Installer mkdocs: 

```
pip install mkdocs
```

#### Créer votre projet mkdocs 
```
mkdocs new kubernetes-training 
```

#### Executer votre projet
```
cd kubernetes-training
mkdocs run
```
Accéder au browser et vérifier: http://0.0.0.0:8000/ 

#### Dockerizer la documentation

```
cp ../Dockerfile .
docker buildx build -t doc-app .
```

## Execution du container

```
docker run --name myawesome-doc -d -p 8088:8000 doc-app
```

## Vérification de l'état du container

```
docker ps -a -f name=myawesome-doc
```

## Affichage des logs en mode streaming

```
docker logs myawesome-doc -f
```