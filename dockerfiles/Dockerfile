
# Base image
FROM nginx:latest

# Set labels
LABEL owner="Subhabrata Panda"
LABEL gmail="panda.subhabarata2003@gmail.com"

# Install Git and update the OS
RUN apt-get update && \
    apt-get install -y git

# Set the environment variable for the repository URL
ENV REPO_URL=https://github.com/Subhabrata2468/project1.git

# Clone the GitHub repository
RUN git clone $REPO_URL /app

# Copy the contents of /app to Nginx's HTML directory
RUN cp -r /app/* /usr/share/nginx/html/

# Remove default Nginx configuration
RUN rm /etc/nginx/conf.d/default.conf

# Expose port 80 for HTTP traffic
EXPOSE 80

# Start Nginx when the container launches
CMD ["nginx", "-g", "daemon off;"]

