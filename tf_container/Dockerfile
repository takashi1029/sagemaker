FROM python:3.5

RUN apt-get update
RUN apt-get install git -y
RUN pip install tensorflow

RUN curl -OL https://github.com/google/protobuf/releases/download/v3.3.0/protoc-3.3.0-linux-x86_64.zip;\
        apt-get install unzip;\
        unzip protoc-3.3.0-linux-x86_64.zip -d protoc3;\
        mv protoc3/bin/* /usr/local/bin/;\
        mv protoc3/include/* /usr/local/include/;\
        chown $USER /usr/local/bin/protoc;\
        chown $USER /usr/local/bin/protoc;\

RUN apt-get install python-pil python-lxml python-tk -y; \
            pip install Cython; \
            pip install jupyter; \
            pip install matplotlib; \
            pip install Cython; \
            pip install pillow; \
            pip install lxml; \
            pip install jupyter; \
            pip install matplotlib; \


ENV PYTHONUNBUFFERED=TRUE
ENV PYTHONDONTWRITEBYTECODE=TRUE
ENV PATH="/opt/program:${PATH}"

RUN mkdir /opt/program

RUN mkdir /opt/program/object_detection;\
        mkdir  /opt/program/slim
COPY train /opt/program/
COPY ssd_mobilenet_v2_coco.config /opt/program
COPY object_detection /opt/program/object_detection
COPY slim /opt/program/slim

WORKDIR /opt/program

RUN git clone https://github.com/cocodataset/cocoapi.git;\
        cd cocoapi/PythonAPI;\
        make;\
        cp -r pycocotools /opt/program/;

WORKDIR /opt/program

RUN /bin/bash -c "protoc object_detection/protos/*.proto --python_out=./"
ENV PYTHONPATH=$PYTHONPATH:/opt/program:/opt/program/slim