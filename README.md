# ML_production_IZ2

## _Building your own image_
For building oun image of online inference for model one need to clone this branch of repository and build docker image from dockerfile. This can be done with next commands:

```
cd </path/to/your/directory>
git clone https://github.com/made-ml-in-prod-2022/ArtemPushPop.git --branch homework_2 --single-branch
cd ArtemPushPop/online_inference/
sudo docker build -t <name of your image> .
```

To run container from recently build image run:

```
docker run -dp 8000:8000 --rm <name of your image>
```

## _Loading docker inference image_

This part of homework and this branch of repository is dedicated for development of online inference of model, trained in previous homework. Solution to this task is docker image of uvicorn server, hosted on docker hub. In order to run the server on your local machine, one need to do next steps:
```
docker pull gotovtsev/ml_prod_2
docker run -dp 8000:8000 --rm gotovtsev/ml_prod_2
```

Parametrizing server inside docker container is done by environment variables, for example, to load model artifact from inside docker image, execute next command:

```
docker run -dp 8000:8000 --rm --env MODEL_LOCATION=local [--env PATH_TO_SERIALIZATION=your_path] gotovtsev/ml_prod_2
```
```PATH_TO_SERIALIZATION``` can be ommited because it has default value.

For loading another artifact of model from google disk, execute next command:
```
docker run -dp 8000:8000 --rm --env PATH_TO_SERIALIZATION=<your_path> gotovtsev/ml_prod_2
```
,where ```<your_path>``` is sha of shareble link from google disk.

For checking that server is functioning, in repository located simple script named ```test_request.py```, run it after the docker container with server is up. In output there will be clear trace.
