# ---------- Stage 1: Build React application ----------

FROM node:22-alpine AS builder

WORKDIR /app

COPY package*.json ./

RUN npm ci

COPY . .

RUN npm run build


# ---------- Stage 2: Apache ----------

FROM httpd:2.4-alpine

# Remove default Apache page
RUN rm -rf /usr/local/apache2/htdocs/*

# Copy React production build
COPY --from=builder /app/dist/ /usr/local/apache2/htdocs/

# Copy Apache configuration
COPY httpd.conf /usr/local/apache2/conf/httpd.conf

EXPOSE 80

CMD ["httpd-foreground"]