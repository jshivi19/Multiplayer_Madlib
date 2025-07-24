# Multiplayer Mad Lib Game

A fun multiplayer Mad Lib game that runs on a local network using SSL encryption. Players connect to a server, answer creative questions, and vote for the funniest responses!

## 🎮 How It Works

1. Players connect to the server using their username
2. The server presents a Mad Lib question with one player's name randomly inserted
3. All players submit their creative answers
4. Players vote for their favorite answer
5. Points are awarded based on votes received
6. After 3 rounds, the player with the most points wins!

## 📋 Requirements

- Python 3.6 or higher
- SSL certificates (cert.pem, key.pem, ca.pem)
- Local network connection
- Minimum 2 players to start the game

## 🔧 Setup Instructions



### 1 . Configure Network Settings

Update the `HOST` variable in both server and client files:

**Server (server.py):**
```python
HOST = "192.168.247.85"  # Replace with your server's IP address
PORT = 65432
```

**Client (client.py):**
```python
HOST = "192.168.247.85"  # Must match server IP
PORT = 65432
```

### 3. File Structure

Ensure your project directory contains:
```
multiplayer-madlib/
├── server.py
├── client.py
├── cert.pem
├── key.pem
├── ca.pem
└── README.md
```

## 🚀 Running the Game

### Start the Server

1. Run the server on the host machine:
```bash
python server.py
```

2. The server will display:
```
Server is listening on 192.168.247.85:65432
```

### Connect Clients

1. On each player's machine, run:
```bash
python client.py
```

2. Enter your username when prompted
3. Wait for other players to join

### Game Flow

1. **Minimum Players**: Game starts when at least 2 players join
2. **Rounds**: 3 rounds total
3. **Questions**: Random Mad Lib questions with player names inserted
4. **Voting**: Players vote for the funniest answers
5. **Scoring**: Points awarded based on votes received
6. **Winner**: Player with most points after 3 rounds wins

## 🎯 Game Rules

- Players cannot vote for their own answers (optional - can be enabled in client code)
- Each vote gives 1 point to the selected answer's author
- In case of a tie, multiple winners are declared
- Disconnected players are automatically removed from active rounds

## 🔒 Security Features

- SSL/TLS encryption for all client-server communication
- Certificate-based authentication
- Secure socket connections

## 🛠️ Configuration Options

### Server Settings (server.py)
```python
no_of_rounds = 3        # Number of game rounds
minimum_players = 2     # Minimum players to start
HOST = "IP_ADDRESS"     # Server IP address
PORT = 65432           # Server port
```

### Client Settings (client.py)
```python
game_code = "1234"     # Game room identifier
HOST = "IP_ADDRESS"    # Server IP address
PORT = 65432          # Server port
```

## 📝 Sample Questions

The game includes 21 pre-written Mad Lib questions such as:
- "If [player] could have any superpower, it would be the ability to __________."
- "[player] secret talent is juggling flaming __________."
- "If [player] were a superhero, his arch-nemesis would be the evil __________."

## 🐛 Troubleshooting

### Common Issues

**Connection Refused:**
- Ensure the server is running
- Check if the IP address and port are correct
- Verify firewall settings allow connections on the specified port

**SSL Certificate Errors:**
- Ensure all certificate files (cert.pem, key.pem, ca.pem) are present
- Regenerate certificates if they're corrupted or expired
- Make sure certificate permissions are readable

**Game Not Starting:**
- Check if minimum number of players (2) have joined
- Verify all players are properly connected
- Look at server console for error messages

**Player Disconnection:**
- Disconnected players are automatically removed from active rounds
- Game continues with remaining players
- Check network stability and connection quality

## 🎮 Example Gameplay

```
Server Console:
> Alice ('192.168.1.100', 52341) has joined the queue!
> Bob ('192.168.1.101', 52342) has joined the queue!
> 
> Round 1 started! Remaining players will be kept in queue!
> Answer from Alice: flying unicorns
> Answer from Bob: invisible socks
> Vote from Alice: 192.168.1.101
> Vote from Bob: 192.168.1.100
> Updated Scoreboard: Alice: 1, Bob: 1

Client Console:
> Enter your username: Alice
> Alice ('192.168.1.100', 52341) joined the game.
> 
> ------------------------------------------------------------
> Question: If Alice could have any superpower, it would be the ability to __________.
> ------------------------------------------------------------
> Enter your answer: fly through dimensions
> 
> Sent answer! Waiting for others to answer...
> 
> ------------------------------------------------------------
> Voting Options:
> ------------------------------------------------------------
>     1: fly through dimensions
>     2: read minds backwards
> 
> Vote for an option: 2
> You selected the answer by 192.168.1.101: read minds backwards
> 
> ------------------------------------------------------------
> Updated Scoreboard: Alice: 0, Bob: 1
> ------------------------------------------------------------
```


## 🔧 Technical Details

### Server Architecture
- **Threading**: Uses ThreadPoolExecutor for handling multiple client connections
- **SSL Context**: Implements server-side SSL with certificate authentication
- **Game State**: Maintains client information using thread-safe dictionaries
- **Error Handling**: Graceful handling of client disconnections and network errors

### Communication Protocol
1. **Connection**: Client connects with SSL handshake
2. **Authentication**: Username exchange and game code verification
3. **Game Loop**: Question → Answer → Vote → Scoreboard cycle
4. **Termination**: Final scores and winner announcement

### Data Structures
- `ClientInfo`: Stores connection, IP, username, and score
- `client_info_dict`: Main player registry (IP → ClientInfo)
- `client_answers`: Temporary storage for round answers (IP → Answer)

## 🎯 Game Features

- **21 Unique Questions**: Pre-written Mad Lib templates
- **Random Player Selection**: Questions feature random player names
- **Secure Voting**: Players vote by selecting numbered options
- **Real-time Scoring**: Live scoreboard updates after each round
- **Tie Handling**: Multiple winners supported
- **Graceful Disconnection**: Automatic cleanup of disconnected players

## 🚀 Future Enhancements

Potential improvements you could add:
- Custom question sets
- Multiple game rooms with different codes
- Spectator mode
- Chat functionality
- Player statistics tracking
- Web-based interface
- Database persistence for game history

## 📄 License

This project is open source. Feel free to modify and distribute according to your needs.

---

**Happy Gaming! 🎉**

*Create hilarious stories with friends in this multiplayer Mad Lib adventure!*
