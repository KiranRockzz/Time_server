# Time_server
This repository includes the code for a Node.js time server. The time server is a backend application created with Node.js that responds to HTTP requests by providing the current date and time in JSON format.

'time-server.js'
const net = require('net');

// Function to format the current date and time
const formatDate = () => {
  const now = new Date();
  const year = now.getFullYear();
  const month = String(now.getMonth() + 1).padStart(2, '0');
  const day = String(now.getDate()).padStart(2, '0');
  const hour = String(now.getHours()).padStart(2, '0');
  const minute = String(now.getMinutes()).padStart(2, '0');
  return `${year}-${month}-${day} ${hour}:${minute}\n`;
};

const server = net.createServer((socket) => {
  socket.end(formatDate());
});

const port = process.argv[2];
server.listen(port, () => {
  console.log(`TCP server is listening on port ${port}`);
});


'http-json-api-server.js'
const http = require('http');

// Function to create JSON response with current date and time
const getCurrentTimeJson = () => {
  const now = new Date();
  return {
    year: now.getFullYear(),
    month: String(now.getMonth() + 1).padStart(2, '0'),
    date: String(now.getDate()).padStart(2, '0'),
    hour: String(now.getHours()).padStart(2, '0'),
    minute: String(now.getMinutes()).padStart(2, '0')
  };
};

const server = http.createServer((req, res) => {
  if (req.url === '/api/currenttime') {
    const jsonResponse = getCurrentTimeJson();
    res.writeHead(200, { 'Content-Type': 'application/json' });
    res.end(JSON.stringify(jsonResponse));
  } else {
    res.writeHead(404);
    res.end();
  }
});

server.listen(8000, () => {
  console.log('HTTP server is listening on port 8000');
});

[Google sldies]
(https://docs.google.com/presentation/d/1LFL3fCOebQPvj6nhIrbq-aXihaTaYkgR22Ve5n1E1cA/edit?usp=sharing)
