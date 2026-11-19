FROM python:3.14-slim AS builder

ENV PYTHONDONTWRITEBYTECODE=1

ENV PYTHONUNBUFFERED=1

WORKDIR /

RUN python3 -m venv env
RUN . env/bin/activate

RUN pip install -r requirements.txt


FROM python:3.14-slim

ENV PYTHONUNBUFFERED=1

WORKDIR /

# Copy the pre-built virtual environment and application source code.
COPY --from=builder /env /env
RUN . env/bin/activate

COPY . .

EXPOSE 8000

CMD ["gunicorn", "pixora.wsgi:application", "--bind", "0.0.0.0:8000"]
