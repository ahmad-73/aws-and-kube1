#Dockerfile for rdicidr-0.1.0
FROM node:15-apline AS builder

WORKDIR /app

COPY package*.json ./

RUN npm install --only=production --ignore-engines

COPY . .

RUN npm run build

FROM nginx:alpine

WORKDIR /usr/share/nginx/html

COPY --from=builder /app/build .

COPY nginx.conf /etc/nginx/nginx.conf

EXPOSE 80

ENRTYPOINT ["nginx", "-g", "daemon off"]