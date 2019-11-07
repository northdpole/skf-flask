FROM python:3.7

RUN mkdir -p /home/user_api
RUN apt update &&\
    apt install -y apt-utils python3-nltk uwsgi nginx uwsgi-plugin-python3 supervisor

ADD ./ /home/user_api/
RUN chmod a+rw /home/user_api/skf/db /home/user_api/skf/db/*

WORKDIR /home/user_api/
RUN mv /home/user_api/Docker/alpine-cloud/api/site.conf.template /etc/nginx/conf.d/site.conf
RUN mv /home/user_api/Docker/alpine-cloud/api/uwsgi.ini /etc/uwsgi/
RUN mv /home/user_api/Docker/alpine-cloud/api/supervisord.conf /etc/supervisord.conf

RUN pip3 install --upgrade pip &&\
    pip3 install --user nltk &&\
    pip3 install --user  -r requirements.txt

EXPOSE 8888

ENV FLASK_APP=/home/user_api/skf/app.py
ENV PYTHONPATH=/home/user_api
CMD ["/usr/bin/supervisord"]
#ENTRYPOINT ["python3.7", "skf/app.py"]

#First go to the main skf-flask folder and from there build the image
#docker build -f Docker/alpine-cloud/api/Dockerfile . -t skf-api --no-cache

#docker run -e "ORIGIN=localhost" -e "JWT_SECRET=change_this_super_secret_random_string" -ti -p 127.0.0.1:8888:8888 skf-api
