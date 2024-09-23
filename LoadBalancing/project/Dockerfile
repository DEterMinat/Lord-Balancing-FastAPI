# Dockerfile
FROM python:3.9-slim

# Set the working directory inside the container
WORKDIR /app

# Copy all files from the host machine's "app" directory to the container's "/app" directory
COPY ./app /app

# Install FastAPI and Uvicorn
RUN pip install fastapi uvicorn

# Expose the port 8000
EXPOSE 8000

# Run FastAPI app with Uvicorn
CMD ["uvicorn", "app:app", "--host", "0.0.0.0", "--port", "8000"]
