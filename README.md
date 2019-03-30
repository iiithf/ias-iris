Generate Tensorflow serving model for Iris dataset.

```bash
# build model
python3 dev.py

# deploy with tensorflow serving
docker pull tensorflow/serving
docker run -p 8501:8501 \
  --mount type=bind,source=$PWD/build,target=/models/model \
  -e MODEL_NAME=model -t tensorflow/serving

# host dataset as input service
python3 input.py

# use input service and model for inference
# <input address> <model address>
./inference.sh :1992 :8501
```
