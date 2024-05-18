# Use the official Python image from the Docker Hub
FROM python:3.8

# Set the working directory to /app
WORKDIR /app

# Copy the contents of the backend directory into /app
COPY . /app

#Requirements
RUN pip freeze > requirements.txt

# Install any needed packages specified in requirements.txt
RUN pip3 install -r requirements.txt

# Run database migrations
RUN python manage.py makemigrations
RUN python manage.py migrate

# Make port 8000 available to the world outside this container
EXPOSE 8000

# Run the application
CMD ["gunicorn", "-b", "0.0.0.0:8000", "--worker-class=gevent", "--worker-connections=1000", "--workers=5", "backend.wsgi"]
