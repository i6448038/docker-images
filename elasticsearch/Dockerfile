FROM elasticsearch:5.1.2

#安装smartcn分词
WORKDIR /usr/share/elasticsearch
RUN bin/elasticsearch-plugin install analysis-smartcn
RUN usermod -u 1000 elasticsearch

#安装ik分词
ADD ik plugins/ik

#安装拼音分词
ADD pinyin plugins/pinyin


EXPOSE 9200 9300
