# Use official Apache image
FROM httpd:latest

# Set the working directory
WORKDIR /usr/local/apache2/htdocs/

# Copy the custom index.html
COPY index.html .

# Expose port 80
EXPOSE 80

# Start Apache server
CMD ["httpd", "-D", "FOREGROUND"]
