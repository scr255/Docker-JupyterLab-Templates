FROM jupyter/scipy-notebook:latest

USER root
WORKDIR /tmp

RUN apt-get update && apt-get install -y gnupg curl fonts-ipafont fonts-ipaexfont

RUN wget https://dl.google.com/linux/linux_signing_key.pub \
 && apt-key add linux_signing_key.pub \
 && echo 'deb [arch=amd64] http://dl.google.com/linux/chrome/deb/ stable main' | tee /etc/apt/sources.list.d/google-chrome.list \
 && apt-get update \
 && apt-get install -y google-chrome-stable \
 && google-chrome --version

RUN CHROMEDRIVER_VERSION=`curl -sS chromedriver.storage.googleapis.com/LATEST_RELEASE` \
 && curl -sS -o /tmp/chromedriver_linux64.zip http://chromedriver.storage.googleapis.com/$CHROMEDRIVER_VERSION/chromedriver_linux64.zip \
 && unzip /tmp/chromedriver_linux64.zip \
 && mv chromedriver /usr/local/bin/

RUN chown -R ${NB_USER} /home/${NB_USER}/.local

USER ${NB_USER}
WORKDIR ${HOME}

COPY requirements.txt /tmp
RUN pip install -r /tmp/requirements.txt