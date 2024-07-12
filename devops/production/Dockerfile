# Usar una imagen base con Node.js
FROM node:20-alpine AS build

# Establecer el directorio de trabajo dentro del contenedor
WORKDIR /app

# Copiar el archivo package.json y package-lock.json
COPY package*.json ./

# Instalar dependencias
RUN npm install

# Copiar el resto de la aplicación
COPY . .

# Construir la aplicación para producción
RUN npm run build

# Usar una imagen de servidor web para servir la aplicación
FROM nginx:stable-alpine

# Copiar los archivos de construcción al directorio de nginx
COPY --from=build /app/dist /usr/share/nginx/html

# Exponer el puerto en el que correrá nginx
EXPOSE 80

# Comando para iniciar nginx
CMD ["nginx", "-g", "daemon off;"]