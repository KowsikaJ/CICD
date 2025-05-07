# Stage 1: Build the Vite app
FROM node:18-alpine as build
WORKDIR /app
COPY . .
RUN npm install
RUN npm run build

#RUN npm audit fix
# or if you want to force fixing breaking changes
# RUN npm audit fix --force


# Stage 2: Serve the built app
FROM node:18-alpine
WORKDIR /app
RUN npm install -g serve
COPY --from=build /app/dist ./dist
EXPOSE 3000
CMD ["serve", "-s", "dist", "-l", "3000"]
