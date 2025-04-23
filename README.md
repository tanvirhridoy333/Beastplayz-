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

