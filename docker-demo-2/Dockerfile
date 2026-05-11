FROM node:20-alpine

# Create a non-root user and group
RUN addgroup -S appgroup && adduser -S appuser -G appgroup

RUN mkdir -p /home/app

COPY ./app /home/app

WORKDIR /home/app

# Install deps as root, then lock down
RUN npm ci --omit=dev && \
    npm cache clean --force && \
    chown -R appuser:appgroup /home/app

# Switch to non-root user
USER appuser

# Explicit port documentation
EXPOSE 3000

CMD ["node", "server.js"]