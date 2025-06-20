FROM ubuntu:24.04

ENV LANG C.UTF-8
ENV LC_ALL C.UTF-8
# Set timezone
ENV TZ=Asia/Jakarta

RUN apt-get update && \
    apt-get install -y software-properties-common && \
    add-apt-repository ppa:deadsnakes/ppa && \
    apt-get update &&\
    apt-get install -y \
    python3.12 \
    python3.12-venv \
    python3.12-dev \
    python3-pip \
    git \
    libxml2-dev \
    libxslt1-dev \
    zlib1g-dev \
    libsasl2-dev \
    libldap2-dev \
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
    postgresql-client \
    build-essential && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/*


# Install Node.js dependencies
RUN npm install -g less less-plugin-clean-css

# Install pip dependencies (harus dipasang ulang saat ada perubahan requirements)
WORKDIR /opt/odoo
COPY requirements.txt ./

RUN python3.12 -m venv /venv && \
    /venv/bin/pip install --upgrade pip setuptools wheel && \
    /venv/bin/pip install -r requirements.txt && \
    /venv/bin/pip install babel

# Expose port Odoo
EXPOSE 8069 8072

CMD ["/venv/bin/python", "odoo-bin", "-c", "/etc/odoo/odoo.conf", "--dev=all"]