FROM tosc-registry:443/odoo-project:16.0-a468795-batteries
MAINTAINER The Open Source Company

RUN mkdir -p /odoo/src/odoo
COPY ./src /odoo/src/odoo
COPY ./external-src /odoo/external-src
COPY ./local-src /odoo/local-src
COPY ./data /odoo/data
COPY ./songs /odoo/songs
COPY ./setup.py /odoo/
COPY ./VERSION /odoo/
COPY ./migration.yml /odoo/

# Project's specifics packages
USER root
RUN set -x; \
        apt-get update \
        && apt-get install -y --no-install-recommends \
        git \
        python3-shapely \
	&& apt-get clean \
        && rm -rf /var/lib/apt/lists/*

COPY ./requirements.txt /odoo/
USER odoo
RUN pip install -e /odoo
RUN pip install -e /odoo/src/odoo
RUN cd /odoo && pip install -r requirements.txt