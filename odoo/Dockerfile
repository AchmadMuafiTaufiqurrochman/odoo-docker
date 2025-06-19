FROM ubuntu:24.04

ENV LANG C.UTF-8
ENV LC_ALL C.UTF-8
# Set timezone
ENV TZ=Asia/Jakarta

RUN apt-get update && \
    apt-get upgrade -y && \
    apt-get install -y software-properties-common && \
    add-apt-repository ppa:deadsnakes/ppa && \
    apt-get update

# Update & install dependencies
RUN apt-get install -y \
    python3.12 \
    python3.12-venv \
    python3.12-dev \
    python3-pip \
    build-essential \
    git \
    libxml2-dev \
    libxslt1-dev \
    zlib1g-dev \
    libsasl2-dev \
    libldap2-dev \
    build-essential \
    libssl-dev \
    libffi-dev \
    libmysqlclient-dev \
    libjpeg-dev \
    libjpeg8-dev \
    libpq-dev \
    liblcms2-dev \
    libblas-dev \
    libatlas-base-dev \
    npm \
    node-less \
    wkhtmltopdf \
    postgresql-client 

# Install Node.js dependencies
RUN npm install -g less less-plugin-clean-css

# Create odoo user
RUN useradd -m -d /opt/odoo -U -r -s /bin/bash odoo

# Set working directory
WORKDIR /opt/odoo

# Copy source code (jika tidak pakai volume mount)
COPY . /opt/odoo

# Buat virtual environment dan install deps di dalamnya
RUN python3.12 -m venv /venv && \
    /venv/bin/pip install --upgrade pip setuptools wheel && \
    /venv/bin/pip install -r requirements.txt && \
    /venv/bin/pip install babel

# Set ownership
RUN chown -R odoo:odoo /opt/odoo

RUN chmod 777 -R /opt/odoo

# Set user
USER odoo

EXPOSE 8069 8072

CMD ["/venv/bin/python", "odoo-bin", "-c", "/etc/odoo/odoo.conf"]
