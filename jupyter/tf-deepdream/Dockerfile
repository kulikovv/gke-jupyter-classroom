# Copyright 2016 Google Inc. All rights reserved.
#
# Licensed under the Apache License, Version 2.0 (the "License");
# you may not use this file except in compliance with the License.
# You may obtain a copy of the License at
#
#     http://www.apache.org/licenses/LICENSE-2.0
#
# Unless required by applicable law or agreed to in writing, software
# distributed under the License is distributed on an "AS IS" BASIS,
# WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
# See the License for the specific language governing permissions and
# limitations under the License.
#
# Description: this image extends basic tensorFlow and adds the DeepDream 
#              and JupyterHub related components
#
# TODO: the JupyterHub singleuser script has moved recently in a pre-release version
#       this will require a pip3 install JupyterHub which is totally overkill for one script

FROM gcr.io/tensorflow/tensorflow-sdca:latest

WORKDIR "/notebooks"

RUN apt-get -qq update && apt-get install -y zip wget python3-pip nfs-common \
	&& pip install --upgrade pip\
	&& pip install scikit-image\
	&& pip install --upgrade numpy \
    && mkdir -p /mnt/notebooks \
	&& wget -q https://raw.githubusercontent.com/tensorflow/tensorflow/master/tensorflow/examples/tutorials/deepdream/deepdream.ipynb \
    && wget -q https://raw.githubusercontent.com/tensorflow/tensorflow/master/tensorflow/examples/tutorials/deepdream/pilatus800.jpg \
	&& apt-get clean && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*
	

COPY jupyter_notebook_config.py /root/.jupyter/
COPY docker-entrypoint.sh /docker-entrypoint.sh
RUN chmod a+rx /docker-entrypoint.sh 

ENTRYPOINT ["/docker-entrypoint.sh"]
CMD [""]
