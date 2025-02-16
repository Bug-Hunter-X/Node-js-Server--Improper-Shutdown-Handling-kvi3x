# Node.js Server: Improper Shutdown Handling

This repository demonstrates a common issue in Node.js servers: improper handling of termination signals.  When a server receives a termination signal (e.g., SIGTERM from `pm2 stop` or `kill`), it should gracefully shut down to ensure all active requests are processed and resources are released cleanly.

The `bug.js` file showcases a server that doesn't handle shutdown gracefully.  The `bugSolution.js` provides a corrected implementation.

## Setup and Reproduction

1. Clone this repository.
2. Run `npm install` (if you encounter any dependencies issue, install 'http' package).
3. Run `node bug.js` to start the server.
4. Send some requests to `http://localhost:8080/`.
5. Terminate the server using `Ctrl+C` or `kill <pid>`, where <pid> is the process ID.
6. Observe the behavior (incomplete responses, resource leaks, etc.).
7. Run `node bugSolution.js` to see the improved, graceful shutdown.

## Solution

The solution utilizes the `process.on('SIGTERM', ...)` and `process.on('SIGINT', ...)` handlers to gracefully manage the termination of the server.  This allows for outstanding requests to be processed and the server to cleanly close.