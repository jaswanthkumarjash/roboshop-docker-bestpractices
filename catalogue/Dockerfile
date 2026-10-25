FROM node:20.19.5-alpine3.21 AS build
WORKDIR /opt/server
COPY package*.json ./
RUN npm install
COPY . .



FROM node:20.19.5-alpine3.21
WORKDIR /opt/server
RUN addgroup -S roboshop && adduser -S roboshop -G roboshop
LABEL com.project="roboshop" \
      com.version="1.0" \
      com.description="Roboshop Catalogue Service" \
      com.author="Jaswanth" \
      com.environment="dev"
ENV MONGO="true" \
    MONGO_URL="mongodb://mongodb:27017/catalogue"
COPY --from=build --chown=roboshop:roboshop /opt/server /opt/server
USER roboshop
CMD ["server.js"]
ENTRYPOINT ["node"]