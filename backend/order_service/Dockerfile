FROM python:3.10-slim

# Set environment variables
ENV PYTHONDONTWRITEBYTECODE=1
ENV PYTHONUNBUFFERED=1
ENV PORT=8000

# Create a non-root user for security
RUN adduser --disabled-password --gecos '' appuser

WORKDIR /code

# Install dependencies
COPY requirements.txt .
RUN pip install --upgrade pip wheel && \
    pip install --no-cache-dir -r requirements.txt

# Copy application code
COPY app /code/app

# Change ownership to non-root user
RUN chown -R appuser:appuser /code
USER appuser

# Expose the application port
EXPOSE ${PORT}

# Run the app with uvicorn
CMD ["uvicorn", "app.main:app", "--host", "0.0.0.0", "--port", "8000"]
