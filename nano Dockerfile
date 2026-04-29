FROM python:3.12-slim

# Install system deps for nmap, scapy, crypto
RUN apt-get update && apt-get install -y \
    nmap \
    gcc \
    libssl-dev \
    && rm -rf /var/lib/apt/lists/*

WORKDIR /app

# Copy requirements first (for caching)
COPY requirements.txt .
RUN pip install --no-cache-dir -r requirements.txt

# Copy everything else
COPY . .

# Create model directory
RUN mkdir -p /app/models/gangster

# HF Spaces runs on port 7860
ENV PORT=7860
EXPOSE 7860

# Start the web app
CMD ["python", "web/app.py"]
