# Multi-stage build : le premier stage installe tout et lance les tests,
# le second ne garde que le strict nécessaire pour la prod.
# Intérêt sécurité : les devDependencies (jest, supertest) et les outils
# de build ne se retrouvent pas dans l'image finale, ce qui réduit la
# surface d'attaque. Intérêt taille : l'image finale basée sur Alpine
# pèse ~50-80 Mo au lieu de ~400 Mo avec une image node complète.

# ---- Stage 1 : build & test ----
FROM node:20-alpine AS build

WORKDIR /app

COPY package*.json ./
RUN npm install

COPY . .
RUN npm test

# ---- Stage 2 : production ----
FROM node:20-alpine

WORKDIR /app

COPY package*.json ./
RUN npm install --only=production

COPY --from=build /app/server.js .

EXPOSE 3000

CMD ["node", "server.js"]