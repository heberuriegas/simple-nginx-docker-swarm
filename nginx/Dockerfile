FROM nginx
RUN rm /etc/nginx/nginx.conf /etc/nginx/conf.d/default.conf
RUN mkdir -p /etc/letsencrypt
COPY nginx.conf /etc/nginx/nginx.conf
COPY production /etc/nginx/conf.d