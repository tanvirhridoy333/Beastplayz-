# Beastplayz

**Beastplayz** is an interactive gaming platform where users can enjoy multiplayer games, brain games, and earn coins through gameplay.

## Features

- **Multiplayer Chess**
- **Multiplayer Ludo**
- **Carrom Disc Game**
- **Car Racing**
- **Single Player Brain Games**
- Clean dark-themed UI
- User login and registration system (Coming soon)
- Reward system using ad revenue (Coming later)

## Project Status

- [x] GitHub Repository Created  
- [x] Website UI Design  
- [ ] Multiplayer Chess  
- [ ] User Login System  
- [ ] Netlify Deployment  

## Tech Stack

- HTML, CSS, JavaScript
- React.js (Frontend)
- Firebase or Supabase (for Auth)
- Node.js + Express (if backend is used later)

## Contributors

- Tanvir Rahman Hridoy (Owner & Lead Dev)
- ChatGPT (AI Assistant & Collaborator)

## License

This project is licensed under the MIT License - see the LICENSE file for details.
import React from "react"; import { Button } from "@/components/ui/button"; import { Card, CardContent } from "@/components/ui/card"; import { motion } from "framer-motion";

const games = [ { name: "Chess", mode: "Single / Multiplayer" }, { name: "Ludo", mode: "Single / Multiplayer" }, { name: "Carrom", mode: "Single / Multiplayer" }, { name: "Car Racing", mode: "Single" }, { name: "Brain Games", mode: "Single" }, ];

##website ui design

export default function BeastplayzUI() { return ( <div className="min-h-screen bg-gradient-to-b from-[#0f0f0f] to-[#1a1a1a] text-white px-4 py-8"> {/* Navbar */} <nav className="flex justify-between items-center mb-8"> <h1 className="text-2xl font-bold text-green-400">Beastplayz</h1> <div className="space-x-4"> <Button variant="ghost">Home</Button> <Button variant="ghost">Games</Button> <Button variant="ghost">Leaderboard</Button> <Button className="rounded-full bg-green-500 text-black">Login</Button> </div> </nav>

{/* Hero Section */}
  <section className="text-center mb-12">
    <motion.h2
      className="text-4xl md:text-5xl font-bold mb-4"
      initial={{ opacity: 0, y: -20 }}
      animate={{ opacity: 1, y: 0 }}
    >
      Play. Win. Rule the Beastplayz Arena.
    </motion.h2>
    <p className="text-lg text-gray-400 mb-6">
      Multiplayer fun, single player challenge, and soon… real rewards!
    </p>
    <Button className="bg-green-500 text-black px-6 py-2 rounded-full text-lg">
      Start Playing
    </Button>
  </section>

  {/* Games Grid */}
  <section className="grid grid-cols-1 sm:grid-cols-2 md:grid-cols-3 gap-6">
    {games.map((game, index) => (
      <Card key={index} className="bg-[#1f1f1f] border border-gray-700">
        <CardContent className="p-6">
          <h3 className="text-xl font-semibold mb-2">{game.name}</h3>
          <p className="text-sm text-gray-400 mb-4">Mode: {game.mode}</p>
          <Button className="bg-green-500 text-black w-full">Play Now</Button>
        </CardContent>
      </Card>
    ))}
  </section>

  {/* Footer */}
  <footer className="mt-16 text-center text-sm text-gray-500">
    <p>About | Contact | Privacy</p>
    <p className="mt-2">Beastplayz — Fun has a new face.</p>
  </footer>
</div>

); }
##Multiplayer chess 
 project structure 
 
multiplayer-chess/
├── client/         <-- React Frontend
│   └── src/
│       └── ChessGame.jsx
├── server/         <-- Node.js Backend
│   └── server.js
├── package.json
backend 
// server/server.js
const express = require('express');
const http = require('http');
const socketIo = require('socket.io');
const cors = require('cors');

const app = express();
app.use(cors());

const server = http.createServer(app);
const io = socketIo(server, {
  cors: {
    origin: "*"
  }
});

let players = {};

io.on('connection', (socket) => {
  console.log('User connected:', socket.id);

  if (Object.keys(players).length < 2) {
    players[socket.id] = Object.keys(players).length === 0 ? 'white' : 'black';
    socket.emit('player-color', players[socket.id]);
  } else {
    socket.emit('room-full');
    return;
  }

  socket.on('move', (data) => {
    socket.broadcast.emit('opponent-move', data);
  });

  socket.on('disconnect', () => {
    console.log('User disconnected:', socket.id);
    delete players[socket.id];
    io.emit('opponent-left');
  });
});

server.listen(4000, () => {
  console.log('Server listening on port 4000');
});

fortend
// client/src/ChessGame.jsx
import React, { useEffect, useState } from 'react';
import Chessboard from 'chessboardjsx';
import { Chess } from 'chess.js';
import io from 'socket.io-client';

const socket = io('http://localhost:4000');
const game = new Chess();

export default function ChessGame() {
  const [fen, setFen] = useState('start');
  const [color, setColor] = useState('white');

  useEffect(() => {
    socket.on('player-color', (assignedColor) => {
      setColor(assignedColor);
    });

    socket.on('opponent-move', (move) => {
      game.move(move);
      setFen(game.fen());
    });

    socket.on('opponent-left', () => {
      alert("Opponent left the game.");
    });

    return () => socket.disconnect();
  }, []);

  const onDrop = ({ sourceSquare, targetSquare }) => {
    const move = {
      from: sourceSquare,
      to: targetSquare,
      promotion: 'q',
    };

    const result = game.move(move);
    if (result) {
      setFen(game.fen());
      socket.emit('move', move);
    }
  };

  return (
    <div>
      <h2>You are playing as {color}</h2>
      <Chessboard
        width={500}
        position={fen}
        onDrop={onDrop}
        orientation={color}
        draggable
      />
    </div>
  );
} 
fortend setup

npm install chessboardjsx chess.js socket.io-client
backend setup 
npm install express socket.io cors


backend start

cd server
node server.js
fortend start

cd client
npm start

