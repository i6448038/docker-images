FROM elasticsearch:2.4

#安装smartcn分词
WORKDIR /usr/share/elasticsearch
RUN bin/plugin install analysis-smartcn
#RUN usermod -u 1000 elasticsearch

#安装ik分词
RUN mkdir plugins/ik
ADD elasticsearch-analysis-ik-1.10.1.zip .
RUN mv elasticsearch-analysis-ik-1.10.1.zip plugins/ik/
WORKDIR plugins/ik
RUN unzip elasticsearch-analysis-ik-1.10.1.zip 
WORKDIR /usr/share/elasticsearch

EXPOSE 9200 9300
CMD ["bin/elasticsearch", "-Des.insecure.allow.root=true"]