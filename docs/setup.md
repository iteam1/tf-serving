- to start docker container:

    sudo docker run -t --rm -p 8501:8501 \
        --gpus all \
        --name serving \
        -v $PWD:/tf_serving \
        -e MODEL_NAME=half_plus_two \
        --entrypoint /bin/bash tensorflow/serving