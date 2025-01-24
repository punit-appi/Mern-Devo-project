# Use an official Node.js runtime as a parent image
FROM node:14

# Set the working directory in the container
WORKDIR /app

# Copy package.json and install dependencies
COPY package*.json ./
RUN npm install

# Copy the rest of the frontend code
COPY . .

# Expose port for the frontend server
EXPOSE 80

# Command to run the app (e.g., with React, if that's the frontend framework)
CMD ["npm", "start"]
