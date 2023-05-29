#Fetch node image to create build artifacts
FROM node:16 as build 

#Set /build as work directory
WORKDIR /build

#Copy package file to increase image build speed
COPY package.json .
COPY yarn.lock .
RUN npm install

#Copy source code to container
COPY . .

#Build artifacts
RUN npm run build

#Fetch nginx image to server build artifacts
FROM nginx as server

#Clear nginx default directory
RUN rm /usr/share/nginx/html/*

#Copy build artifacts from previous image to default nginx directory
COPY --from=build /build/build /usr/share/nginx/html
