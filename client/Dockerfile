# the builder phase
FROM node:alpine as builder
WORKDIR '/app'
COPY package.json ./
RUN npm install
COPY . .
RUN npm run build

# built code is now in /app/build

# second phase of build
FROM nginx
EXPOSE 3000
COPY ./nginx/default.conf /etc/nginx/conf.d/default.conf
#copy the build folder from the builder phase 
# into the standard nginx content directory
COPY --from=builder /app/build /usr/share/nginx/html