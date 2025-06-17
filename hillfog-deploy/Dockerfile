# Use OpenJDK 11 as base image
FROM openjdk:11-jre-slim

# Set working directory
WORKDIR /app

# Create a non-root user for security with home directory
RUN groupadd -r hillfog && useradd -r -g hillfog -m -d /home/hillfog hillfog

# Create necessary directories
RUN mkdir -p /home/hillfog /app/data

# Copy the JAR file
# Note: Make sure hillfog-0.4.jar is in the same directory as this Dockerfile
COPY hillfog-0.4.jar /app/hillfog.jar

# Change ownership to hillfog user
RUN chown -R hillfog:hillfog /app /home/hillfog

# Switch to non-root user
USER hillfog

# Set HOME environment variable
ENV HOME=/home/hillfog

# Expose port 8088
EXPOSE 8088

# Set JVM options and run the application
CMD ["java", "-Xmx512M", "-jar", "hillfog.jar"]

# Health check (optional)
HEALTHCHECK --interval=30s --timeout=3s --start-period=60s --retries=3 \
    CMD curl -f http://localhost:8088/ || exit 1