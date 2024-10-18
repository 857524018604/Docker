FROM ubuntu

WORKDIR /app

COPY requirements.txt /app
COPY devops /app

# Fix common dpkg and apt-get issues
RUN apt-get update && \
    apt-get install -y --no-install-recommends software-properties-common && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/* && \
    dpkg --configure -a && \
    apt-get update && \
    apt-get install -f && \
    DEBIAN_FRONTEND=noninteractive apt-get install -y python3 python3-pip python3-venv && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/*

# Create and activate virtual environment
RUN python3 -m venv /app/venv && \
    /app/venv/bin/pip install --no-cache-dir -r requirements.txt

ENTRYPOINT ["/app/venv/bin/python"]
CMD ["manage.py", "runserver", "0.0.0.0:8000"]





