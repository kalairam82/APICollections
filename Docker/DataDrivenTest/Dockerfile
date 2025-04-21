# Use the official Node.js 14 image as the base image
FROM node:22

# Set the working directory in the container
WORKDIR /app


# Install Newman globally
RUN npm install -g newman

#Install Newman html report
RUN npm install -g newman-reporter-html

#Install Newman Reporter HTMLExtra
RUN npm install -g newman-reporter-htmlextra


# Copy your Postman collection and environment files to the working directory
COPY ContactsAPIDataDriven.json .
COPY ContactsEnv.json .
COPY contacts.csv .

# Set the command to run Newman and execute your Postman collection
CMD ["newman", "run", "ContactsAPIDataDriven.json", "-e", "ContactsEnv.json", "-d", "contacts.csv", "-r", "cli,json,html,htmlextra"]

