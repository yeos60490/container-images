FROM django:1.10.4-python2

ENV container docker

RUN apt-get update \
    && apt-get install -y --no-install-recommends \
        postgresql-client \
    && rm -rf /var/lib/apt/lists/*

WORKDIR /root/
COPY requirements.txt .
RUN pip install -r requirements.txt \
        && pip install django-mathfilters \
        && pip install python-dateutil \
        && pip install pymongo \
        && pip install django-excel

WORKDIR /root/web/

CMD ["python", "manage.py", "runserver", "0.0.0.0:80"]
CMD ["python", "manage.py", "runserver", "0.0.0.0:443"]
