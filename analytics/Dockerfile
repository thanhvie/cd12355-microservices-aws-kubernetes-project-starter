# Use an official Python runtime as a parent image with Python 3.10 slim
FROM python:3.10-slim

# Set the working directory in the container
WORKDIR /app

# Copy the current directory contents into the container at /app
COPY . /app

# Install any needed packages specified in requirements.txt
RUN pip install --no-cache-dir -r requirements.txt

# Set environment variables
ENV FLASK_APP=app.py
ENV FLASK_RUN_HOST=0.0.0.0

# Expose port 5153
EXPOSE 5153

# Define environment variable
ENV APP_PORT=5153

# Run the application
CMD ["python", "app.py"]