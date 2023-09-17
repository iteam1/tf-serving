# tf_serving
tf serving example

# quickstart

    # Download the TensorFlow Serving Docker image and repo
    docker pull tensorflow/serving

    git clone https://github.com/tensorflow/serving
    # Location of demo models
    TESTDATA="$(pwd)/serving/tensorflow_serving/servables/tensorflow/testdata"

    # Start TensorFlow Serving container and open the REST API port
    docker run -t --rm -p 8501:8501 \
        -v "$TESTDATA/saved_model_half_plus_two_cpu:/models/half_plus_two" \
        -e MODEL_NAME=half_plus_two \
        tensorflow/serving &

    # Query the model using the predict API
    curl -d '{"instances": [1.0, 2.0, 5.0]}' \
        -X POST http://localhost:8501/v1/models/half_plus_two:predict

    # Returns => { "predictions": [2.5, 3.0, 4.5] }

# references

[TensorFlow Serving](https://www.tensorflow.org/tfx/guide/serving)

[48_tf_serving](https://github.com/codebasics/deep-learning-keras-tf-tutorial/tree/master/48_tf_serving)

[tf serving tutorial | tensorflow serving tutorial | Deep Learning Tutorial 48 (Tensorflow, Python)](https://www.youtube.com/watch?v=P-5sMcpTE0g)

[Tự học Tensorflow | Bài 2 | Giới thiệu Tensorflow Serving](https://www.youtube.com/watch?v=5kVBAD2Cbj8)