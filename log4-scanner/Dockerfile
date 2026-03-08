FROM python:3.11-alpine AS builder

WORKDIR /app

COPY requirements.txt requirements.txt

RUN apk add --no-cache gcc g++ make libffi-dev openssl-dev \
    && pip3 install --no-cache-dir -r requirements.txt

FROM python:3.11-alpine

WORKDIR /app

RUN adduser -D scanner
COPY --from=builder /usr/local/lib/python3.11/site-packages /usr/local/lib/python3.11/site-packages
COPY . .

USER scanner

ENTRYPOINT ["python", "log4j-scan.py" ]
