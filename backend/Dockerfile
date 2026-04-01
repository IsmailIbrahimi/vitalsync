# Multi-stage build : le premier stage installe les dépendances et exécute les tests
# dans un environnement complet. Le second stage produit une image légère de production
# en ne copiant que le strict nécessaire. Cela réduit la taille de l'image finale et
# évite d'embarquer les outils de dev et de test en production, limitant la surface d'attaque.

# Stage 1 : installation et tests
FROM node:20-alpine AS builder
WORKDIR /app
COPY package.json .
RUN npm install
COPY . .
RUN npm test

# Stage 2 : image de production légère
FROM node:20-alpine AS production
WORKDIR /app
COPY package.json .
RUN npm install --omit=dev
COPY server.js .
EXPOSE 3000
CMD ["node", "server.js"]