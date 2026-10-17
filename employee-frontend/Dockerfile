# Installer les dépendances + construire l'application
FROM node:14-alpine AS build
WORKDIR /app

RUN npm ci

COPY . .


ARG API_URL=http://localhost:8081/api/v1/employees
RUN sed -i "s|http://localhost:8081/api/v1/employees|${API_URL}|" src/app/employee.service.ts \
    && grep -q "${API_URL}" src/app/employee.service.ts

RUN npm run build -- --configuration production


# Mode production + serveur web
FROM nginx:1.27-alpine
COPY nginx.conf /etc/nginx/conf.d/default.conf
COPY --from=build /app/dist/angular-frontend /usr/share/nginx/html
EXPOSE 80