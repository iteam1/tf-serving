- Download the TensorFlow Serving Docker image `docker pull tensorflow/serving` or GPU image`docker pull tensorflow/serving:latest-gpu`


- to start docker container: `sudo docker run -it -v $PWD:/tf_serving -p 8601:8601 --entrypoint /bin/bash tensorflow/serving`

- To serve only latest model(*Inside contained*): `tensorflow_model_server --rest_api_port=8601 --model_name=spam_model --model_base_path=/tf_serving/saved_models/`

- Check your serving on browser: `http://localhost:8601/v1/models/spam_model`

- Predict a instances:

    curl -d '{"instances": ["This is a spam or NOT?"]}' \
        -X POST http://localhost:8601/v1/models/spam_model:predict

- To serve models using model config file: `tensorflow_model_server --rest_api_port=8601 --allow_version_labels_for_unavailable_models --model_config_file=/tf_serving/configs/model.config.c`

**REST Usage**

If you're using the REST API surface to make inference requests, instead of using

    /v1/models/<model name>/versions/<version number>

Example:

    curl -d '{"instances": ["This is a spam or NOT?"]}' \
        -X POST http://localhost:8601/v1/models/spam_model/versions/1:predict

simply request a version using a label by structuring your request path like so

    /v1/models/<model name>/labels/<version label>.

Example:

    curl -d '{"instances": ["This is a spam or NOT?"]}' \
        -X POST http://localhost:8601/v1/models/spam_model/labels/beta:predict


Note that version label is restricted to a sequence of Word characters, composed of alphanumeral characters and underscores (i.e. [a-zA-Z0-9_]+).