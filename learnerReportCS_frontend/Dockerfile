FROM node:16

# Working directory be app
WORKDIR /usr/src/app

COPY package*.json ./

###  Installing dependencies

#RUN npm install --silent
RUN npm install --legacy-peer-deps

# copy local files to app folder
COPY . .

EXPOSE 3000

CMD ["npm","start"]
