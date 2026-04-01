FROM nginx:stable-alpine

# Supprime la config par défaut de Nginx
RUN rm /etc/nginx/conf.d/default.conf

# Copie notre config personnalisée
COPY nginx.conf /etc/nginx/conf.d/

# Copie le fichier HTML
COPY index.html /usr/share/nginx/html/

EXPOSE 80

CMD ["nginx", "-g", "daemon off;"]