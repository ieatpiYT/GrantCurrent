FROM nginx:1.27-alpine

# Defaults for Railway. Override them in the Railway Variables tab if needed.
ENV PORT=80
ENV BACKEND_URL=http://grantcurrent.railway.internal:8000
ENV DNS_RESOLVER=[fd12::10]
# Only these three variables get filled into the nginx template
ENV NGINX_ENVSUBST_FILTER=PORT|BACKEND_URL|DNS_RESOLVER

COPY frontend/index.html /usr/share/nginx/html/index.html
COPY frontend/app.js /usr/share/nginx/html/app.js
COPY frontend/styles.css /usr/share/nginx/html/styles.css

# Files in /etc/nginx/templates/*.template are auto-filled with the variables
# above when the container starts, and saved as /etc/nginx/conf.d/default.conf
COPY frontend/nginx.conf /etc/nginx/templates/default.conf.template

EXPOSE 80
