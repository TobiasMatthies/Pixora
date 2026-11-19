FROM python:3.14-slim AS builder

ENV PYTHONDONTWRITEBYTECODE=1

ENV PYTHONUNBUFFERED=1

WORKDIR /app

RUN python -m venv env
ENV PATH="env/bin/:$PATH"

COPY ./requirements.txt /app/requirements.txt
RUN pip install -r requirements.txt


FROM python:3.14-slim

ENV PYTHONUNBUFFERED=1

WORKDIR /app

# Copy the pre-built virtual environment and application source code.
COPY --from=builder /app/env /app/env
ENV PATH="env/bin/:$PATH"

COPY . .

RUN chmod +x ./entrypoint.sh

EXPOSE 8000

ENTRYPOINT ["/app/entrypoint.sh"]
