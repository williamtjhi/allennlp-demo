# This is the common Dockerfile that is used to build all demos unless the demo
# overrides this with its own Dockerfile in its directory.
FROM allennlp/allennlp:v1.1.0

WORKDIR /app/

COPY requirements.txt requirements.txt
RUN pip install -r requirements.txt

RUN spacy download en_core_web_sm

RUN pip install git+git://github.com/allenai/allennlp.git@0b20f80c1ea700766fe53d2eaf1c28de764f9710
RUN pip install git+https://github.com/facebookresearch/detectron2@v0.2.1

COPY allennlp_demo/__init__.py allennlp_demo/__init__.py
COPY allennlp_demo/common allennlp_demo/common
COPY allennlp_demo/vilbert_vqa allennlp_demo/vilbert_vqa

# Ensure allennlp_demo module can be found by Python.
ENV PYTHONPATH /app/

# Ensure log messages written immediately instead of being buffered, which is
# useful if the app crashes so the logs won't get swallowed.
ENV PYTHONUNBUFFERED 1

ENTRYPOINT [ "/bin/bash" ]
CMD [ "-c", "python allennlp_demo/vilbert_vqa/api.py" ]
