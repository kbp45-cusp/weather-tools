# Copyright 2023 Google LLC
#
# Licensed under the Apache License, Version 2.0 (the "License");
# you may not use this file except in compliance with the License.
# You may obtain a copy of the License at
#
#     https://www.apache.org/licenses/LICENSE-2.0
#
# Unless required by applicable law or agreed to in writing, software
# distributed under the License is distributed on an "AS IS" BASIS,
# WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
# See the License for the specific language governing permissions and
# limitations under the License.


FROM continuumio/miniconda3:latest

# Update miniconda
RUN conda update conda -y

# Add the mamba solver for faster builds
RUN conda install -n base conda-libmamba-solver
RUN conda config --set solver libmamba

COPY . .
# Create conda env using environment.yml
RUN conda env create -f environment.yml --debug

# Activate the conda env and update the PATH
ARG CONDA_ENV_NAME=weather-dl-v2-license-dep
RUN echo "source activate ${CONDA_ENV_NAME}" >> ~/.bashrc
ENV PATH /opt/conda/envs/${CONDA_ENV_NAME}/bin:$PATH

ENTRYPOINT ["python", "-u", "fetch.py"]
