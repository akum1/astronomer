#
# Copyright 2019 Astronomer Inc.
#
# Licensed under the Apache License, Version 2.0 (the "License");
# you may not use this file except in compliance with the License.
# You may obtain a copy of the License at
#
# http://www.apache.org/licenses/LICENSE-2.0
#
# Unless required by applicable law or agreed to in writing, software
# distributed under the License is distributed on an "AS IS" BASIS,
# WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
# See the License for the specific language governing permissions and
# limitations under the License.

FROM astronomerinc/ap-airflow:0.10.3-alpha.6-debian-1.10.5
LABEL maintainer="Astronomer <humans@astronomer.io>"

LABEL io.astronomer.docker=true
LABEL io.astronomer.docker.airflow.onbuild=true

ONBUILD COPY packages.txt .
ONBUILD USER root
ONBUILD RUN if [[ -s packages.txt ]]; then \
    apt-get update && cat packages.txt | xargs apt-get install -y --no-install-recommends \
    && apt-get clean \
    && rm -rf /var/lib/apt/lists/*; \
  fi
# Install python packages
ONBUILD COPY requirements.txt .
ONBUILD RUN pip install --no-cache-dir -q -r requirements.txt
ONBUILD USER astro
# Copy entire project directory
ONBUILD COPY . .
