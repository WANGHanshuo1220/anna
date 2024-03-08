#  Copyright 2018 U.C. Berkeley RISE Lab
# 
#  Licensed under the Apache License, Version 2.0 (the "License");
#  you may not use this file except in compliance with the License.
#  You may obtain a copy of the License at
# 
#      http://www.apache.org/licenses/LICENSE-2.0
# 
#  Unless required by applicable law or agreed to in writing, software
#  distributed under the License is distributed on an "AS IS" BASIS,
#  WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
#  See the License for the specific language governing permissions and
#  limitations under the License.

FROM ubuntu:20.04

MAINTAINER Vikram Sreekanti <vsreekanti@gmail..com> version: 0.1

ARG repo_org=WANGHanshuo1220
ARG source_branch=master
ARG build_branch=docker-build

RUN apt-get update
RUN apt-get upgrade
RUN apt-get install -y python3-pip
RUN apt-get install -y git
RUN apt-get install net-tools
RUN apt-get install vim --yes

USER root
RUN mkdir /hydro
ENV HYDRO_HOME /hydro

# Check out to the appropriate branch on the appropriate fork of the repository
# and build Anna.
WORKDIR $HYDRO_HOME
RUN git clone --recurse-submodules https://github.com/$repo_org/anna
WORKDIR $HYDRO_HOME/anna
RUN git submodule update --init --recursive
RUN ./common/scripts/install-dependencies.sh
RUN bash scripts/build.sh -j4 -bRelease
WORKDIR /

COPY start-anna.sh /
# CMD bash start-anna.sh $SERVER_TYPE