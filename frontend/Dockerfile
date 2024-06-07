From nginx
WORKDIR /opt
COPY . .
RUN npm install
RUN npm run build 
EXPOSE 30080
CMD ["npm", "start"]