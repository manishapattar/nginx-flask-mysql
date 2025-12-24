# backend/Dockerfile

FROM python:3.10-alpine AS builder

# Set working directory
WORKDIR /code

# Copy requirements and install dependencies
COPY requirements.txt /code
RUN pip3 install -r requirements.txt

# Copy the rest of the backend code
COPY . .

# Set environment variables for Flask
ENV FLASK_APP=hello.py
ENV FLASK_ENV=development
ENV FLASK_RUN_PORT=8000
ENV FLASK_RUN_HOST=0.0.0.0

# Expose Flask port
EXPOSE 8000

# Default command to run Flask
CMD ["flask", "run"]

# Optional dev environment
FROM builder AS dev-envs

# Install git
RUN apk update && apk add git

# Create user for dev
RUN addgroup -S docker && adduser -S --shell /bin/bash --ingroup docker vscode

# Copy Docker tools from a prebuilt image (optional)
# COPY --from=gloursdocker/docker / /

# Default command
CMD ["flask", "run"]

