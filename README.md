# docker-jupyter-s3

Password protected Jupyter Lab environment with access to S3. Usage example:

```
docker run -p 8888:8888 -p 6006:6006 \
    -e AWS_ACCESS_KEY_ID="key" \
    -e AWS_SECRET_ACCESS_KEY="secret" \
    -e ROOT_BUCKET="bucket" \
    -e PROJECT_DIR="project name" \
    -e JUPYTER_PASSWORD="password" \
    jupyter-s3-tensorflow-notebook:0.1.0
```