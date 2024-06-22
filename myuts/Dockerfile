# Use an official Python runtime as a parent image
FROM python:3.12-alpine

# Set environment variables
ENV PYTHONUNBUFFERED=1

# Install system dependencies
RUN apk add --no-cache \
    mariadb-connector-c-dev \
    gcc \
    musl-dev \
    libffi-dev \
    && pip install --upgrade pip

# Set the working directory in the container
WORKDIR /app

# Copy the requirements file into the container at /app
COPY requirements.txt .

# Install Python dependencies
RUN pip install --no-cache-dir -r requirements.txt \
    && pip install --no-cache-dir gunicorn mysqlclient

# Copy the rest of the application code into the container at /app
COPY . .

# Command to run the application
CMD ["gunicorn", "-w", "4", "-b", "0.0.0.0:8007", "myuts.wsgi:application"]
