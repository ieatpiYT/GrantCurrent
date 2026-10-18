FROM python:3.13-slim AS runtime
WORKDIR /app
ENV PYTHONDONTWRITEBYTECODE=1 PYTHONUNBUFFERED=1

COPY backend/requirements.txt ./requirements.txt
RUN pip install --no-cache-dir -r requirements.txt

# The app code lands in /app/app  (so the import path is "app.main:app")
COPY backend/app ./app
# The data files land in /challenge_pack (config.py looks for them there)
COPY challenge_pack /challenge_pack

# Folder for the SQLite database (a Railway Volume gets mounted here)
RUN mkdir -p /data

ENV PYTHONPATH=/app
# Railway overrides PORT at runtime if it sets one; 8000 is the fallback
ENV PORT=8000
EXPOSE 8000

# "--host ::" lets the server be reached over Railway's private (IPv6) network.
# "--proxy-headers" makes the rate limiter see each visitor's real IP
# instead of the nginx container's IP.
CMD ["sh", "-c", "uvicorn app.main:app --host :: --port ${PORT:-8000} --proxy-headers --forwarded-allow-ips='*'"]
