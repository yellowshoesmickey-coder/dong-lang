const express = require('express');
const http = require('http');
const { Server } = require('socket.io');
const path = require('path');

const app = express();
const server = http.createServer(app);
const io = new Server(server);

app.use(express.static(path.join(__dirname, 'public')));

// ─── Role Catalog ───────────────────────────────────────────────────────────
const ROLES = {
  // ── Villager Team ──
  villager: {
    id: 'villager', name: 'Villager', team: 'villager',
    desc: 'No special ability. Win if all werewolves and vampires are eliminated.',
    minPlayers: 5, maxPlayers: 40, action: null
  },
  seer: {
    id: 'seer', name: 'Seer', team: 'villager',
    desc: 'Each night, check one player\'s team (Villager, Werewolf, or Vampire).',
    minPlayers: 5, maxPlayers: 40, action: 'choose_one'
  },
  doctor: {
    id: 'doctor', name: 'Doctor', team: 'villager',
    desc: 'Each night, save one player from being killed (can\'t save same player two nights in a row).',
    minPlayers: 5, maxPlayers: 40, action: 'choose_one'
  },
  hunter: {
    id: 'hunter', name: 'Hunter', team: 'villager',
    desc: 'When you are eliminated, you may shoot one other player of your choice.',
    minPlayers: 5, maxPlayers: 40, action: null, onElimination: 'shoot'
  },
  cupid: {
    id: 'cupid', name: 'Cupid', team: 'villager',
    desc: 'Each night, pair two players as lovers. If one dies, the other dies too. Lovers win together or lose together.',
    minPlayers: 5, maxPlayers: 40, action: 'choose_two'
  },
  builder: {
    id: 'builder', name: 'Builder', team: 'villager',
    desc: 'Each night, check one player\'s exact role (not just their team).',
    minPlayers: 5, maxPlayers: 40, action: 'choose_one'
  },
  prophet: {
    id: 'prophet', name: 'Prophet', team: 'villager',
    desc: 'Each night, see all players\' roles of one team (Villager, Werewolf, or Vampire).',
    minPlayers: 5, maxPlayers: 40, action: 'choose_team'
  },
  veteran: {
    id: 'veteran', name: 'Veteran', team: 'villager',
    desc: 'Cannot be killed on the first night. After that, normal.',
    minPlayers: 5, maxPlayers: 40, action: null
  },

  // ── Werewolf Team ──
  werewolf: {
    id: 'werewolf', name: 'Werewolf', team: 'werewolf',
    desc: 'Each night, kill one player. Win if werewolves + vampires outnumber villagers.',
    minPlayers: 5, maxPlayers: 40, action: 'choose_one', isWolf: true
  },
  wolf_alpha: {
    id: 'wolf_alpha', name: 'Wolf Alpha', team: 'werewolf',
    desc: 'As long as you live, you can kill TWO players each night.',
    minPlayers: 5, maxPlayers: 40, action: 'choose_two', isWolf: true
  },
  baby_wolf: {
    id: 'baby_wolf', name: 'Baby Wolf', team: 'werewolf',
    desc: 'If hanged by villagers, the wolf pack gets angry. The next night, all werewolves can kill 2 players instead of 1.',
    minPlayers: 5, maxPlayers: 40, action: 'choose_one', isWolf: true, revengeKill: true
  },
  bigfoot: {
    id: 'bigfoot', name: 'Bigfoot', team: 'werewolf',
    desc: 'On the second night, choose to join the Villager team or the Werewolf team. Your allegiance is secret until you choose.',
    minPlayers: 5, maxPlayers: 40, action: 'choose_side', isWolf: true, switchesTeam: true
  },

  // ── Vampire Team ──
  vampire: {
    id: 'vampire', name: 'Vampire', team: 'vampire',
    desc: 'Each night, kill one player. Win if all other players are dead.',
    minPlayers: 5, maxPlayers: 40, action: 'choose_one', isVampire: true
  },

  // ── Neutral ──
  doppelganger: {
    id: 'doppelganger', name: 'Doppelgänger', team: 'neutral',
    desc: 'Each night, choose a player to copy their role. If that player dies, you take their role and abilities.',
    minPlayers: 5, maxPlayers: 40, action: 'choose_one'
  },
  drunk: {
    id: 'drunk', name: 'Drunk', team: 'neutral',
    desc: 'You have a secret role each night but don\'t know what it is. Your true role is Villager. Win with Villagers.',
    minPlayers: 5, maxPlayers: 40, action: null, drunkRole: true
  },
  troublemaker: {
    id: 'troublemaker', name: 'Troublemaker', team: 'neutral',
    desc: 'Each night, swap the roles of two players of your choice.',
    minPlayers: 5, maxPlayers: 40, action: 'choose_two'
  },
  shaman: {
    id: 'shaman', name: 'Shaman', team: 'neutral',
    desc: 'Each night, choose a role to give to another player. They become that role.',
    minPlayers: 5, maxPlayers: 40, action: 'choose_one_then_role'
  },
  sorcerer: {
    id: 'sorcerer', name: 'Sorcerer', team: 'neutral',
    desc: 'Can communicate with werewolves at night, but is not a werewolf. Wins with Villagers.',
    minPlayers: 5, maxPlayers: 40, action: 'choose_one', canTalkToWolves: true
  },
  robber: {
    id: 'robber', name: 'Robber', team: 'neutral',
    desc: 'Each night, steal another player\'s role and give them yours. You become their role, they become yours.',
    minPlayers: 5, maxPlayers: 40, action: 'choose_one'
  },
  huntress: {
    id: 'huntress', name: 'Huntress', team: 'neutral',
    desc: 'Each night, kill one player. You win if you survive until the end (all others dead or eliminated).',
    minPlayers: 5, maxPlayers: 40, action: 'choose_one'
  },
  jester: {
    id: 'jester', name: 'Jester', team: 'neutral',
    desc: 'Win if you are voted out and hanged during the day phase.',
    minPlayers: 5, maxPlayers: 40, action: null, winsIfHanged: true
  },
  peace_lover: {
    id: 'peace_lover', name: 'Peace Lover', team: 'neutral',
    desc: 'You can NEVER vote to hang anyone during the day phase. Trying to vote disqualifies your vote.',
    minPlayers: 5, maxPlayers: 40, action: null, cannotVote: true
  },
  retarded: {
    id: 'retarded', name: 'Fool', team: 'neutral',
    desc: 'Win if you are hanged by the villagers during the day phase.',
    minPlayers: 5, maxPlayers: 40, action: null, winsIfHanged: true
  },
  mafioso: {
    id: 'mafioso', name: 'Mafioso', team: 'neutral',
    desc: 'You know who the werewolves are. You can communicate with them at night. You win with the werewolves.',
    minPlayers: 5, maxPlayers: 40, action: null, knowsWolves: true, winsWithWolves: true
  },
  mutant: {
    id: 'mutant', name: 'Mutant', team: 'neutral',
    desc: 'Werewolves cannot kill you. You win if you survive until the end.',
    minPlayers: 5, maxPlayers: 40, action: null, immuneToWolf: true
  },
  witch: {
    id: 'witch', name: 'Witch', team: 'neutral',
    desc: 'Each night, choose to either save a player from death OR kill a player (once per game for each power).',
    minPlayers: 5, maxPlayers: 40, action: 'witch_action'
  },
};

// Roles that can be selected multiple times (filler roles)
const MULTI_ROLE_IDS = ['villager'];

// ─── In-memory state ────────────────────────────────────────────────────────
const rooms = {};
const ROOM_TIMEOUT_MS = 20 * 60 * 1000; // 20 minutes

// ─── Helpers ────────────────────────────────────────────────────────────────
function generateRoomId() {
  return 'room_' + Math.random().toString(36).substring(2, 8).toUpperCase();
}

function generatePassword() {
  return Math.floor(100000 + Math.random() * 900000).toString();
}

function touchRoom(roomId) {
  if (rooms[roomId]) {
    rooms[roomId].lastActivity = Date.now();
  }
}

function cleanupStaleRooms() {
  const now = Date.now();
  const ids = Object.keys(rooms);
  for (const id of ids) {
    if (now - rooms[id].lastActivity > ROOM_TIMEOUT_MS) {
      // Notify players before deleting
      const room = rooms[id];
      if (room && room.sockets) {
        room.sockets.forEach(sid => {
          const conn = io.sockets.sockets.get(sid);
          if (conn) conn.emit('room_expired', { reason: 'Room inactive for 20 minutes' });
        });
      }
      delete rooms[id];
    }
  }
}
setInterval(cleanupStaleRooms, 30000);

// ─── Discord webhook helper ─────────────────────────────────────────────────
function sendDiscordWebhook(room, message) {
  if (!room.discordWebhook) return;
  const url = room.discordWebhook;
  const payload = { content: message };
  fetch(url, {
    method: 'POST',
    headers: { 'Content-Type': 'application/json' },
    body: JSON.stringify(payload)
  }).catch(() => {}); // silent fail
}

// ─── Socket.IO ──────────────────────────────────────────────────────────────
io.on('connection', (socket) => {
  console.log('Client connected:', socket.id);

  // ── Create Room ──
  socket.on('create_room', (data) => {
    const roomId = generateRoomId();
    // Password is optional — null means no password required
    const password = data.password || null;
    const roomName = data.roomName || 'Unnamed Room';
    const discordWebhook = data.discordWebhook || '';
    const maxPlayers = Math.min(Math.max(5, data.maxPlayers || 8), 40);

    rooms[roomId] = {
      id: roomId,
      name: roomName,
      password: password,
      host: socket.id,
      maxPlayers: maxPlayers,
      discordWebhook: discordWebhook,
      lastActivity: Date.now(),
      sockets: new Map(), // socketId -> { name, role, team, isHost, agreed }
      selectedRoles: [],   // list of role IDs chosen by host
      gameState: 'lobby',  // lobby | role_reveal | night | day | voting | gameover
      currentNight: 0,
      eliminated: new Set(),
      votedOut: [],        // history of who was voted out and their real role
      wolfRevengeNight: false, // baby wolf triggered revenge
      assignments: {},     // socketId -> roleId
      nightActions: {},   // socketId -> action result
      votes: {},          // socketId -> voted socketId
      voteTimer: null,
      phaseStartTime: null,
      nightActionResults: {}, // role_id -> result for public announcements
    };

    const room = rooms[roomId];
    room.sockets.set(socket.id, {
      name: data.playerName || 'Anonymous',
      role: null,
      team: null,
      isHost: true,
      agreed: false
    });

    socket.join(roomId);
    touchRoom(roomId);

    socket.emit('room_created', {
      roomId,
      password,
      roomName,
      maxPlayers,
      discordWebhook
    });

    // Notify host that room is created
    io.to(roomId).emit('room_updated', getRoomStatus(roomId));
  });

  // ── Join Room ──
  socket.on('join_room', (data) => {
    const { roomId, password, playerName } = data;

    if (!rooms[roomId]) {
      socket.emit('join_error', { message: 'Room not found.' });
      return;
    }

    const room = rooms[roomId];
    touchRoom(roomId);

    if (room.password !== password) {
      socket.emit('join_error', { message: 'Wrong password.' });
      return;
    }

    if (room.sockets.size >= room.maxPlayers) {
      socket.emit('join_error', { message: 'Room is full.' });
      return;
    }

    if (room.sockets.has(socket.id)) {
      socket.emit('join_error', { message: 'You are already in this room.' });
      return;
    }

    room.sockets.set(socket.id, {
      name: playerName || 'Anonymous',
      role: null,
      team: null,
      isHost: false,
      agreed: false
    });

    socket.join(roomId);
    socket.emit('joined_room', { roomId });
    io.to(roomId).emit('room_updated', getRoomStatus(roomId));
  });

  // ── Join by Room ID (click from active rooms list) ──
  socket.on('join_by_id', (data) => {
    const { roomId, playerName } = data;

    if (!rooms[roomId]) {
      socket.emit('join_error', { message: 'Phòng không tồn tại.' });
      return;
    }

    const room = rooms[roomId];
    touchRoom(roomId);

    // If room has a password, require it
    if (room.password && !data.password) {
      socket.emit('join_password_required', { roomId, roomName: room.name });
      return;
    }

    if (room.password && data.password !== room.password) {
      socket.emit('join_error', { message: 'Sai mã phòng.' });
      return;
    }

    if (room.sockets.size >= room.maxPlayers) {
      socket.emit('join_error', { message: 'Phòng đã đầy.' });
      return;
    }

    if (room.sockets.has(socket.id)) {
      socket.emit('join_error', { message: 'Bạn đã ở trong phòng này.' });
      return;
    }

    room.sockets.set(socket.id, {
      name: playerName || 'Khách',
      role: null,
      team: null,
      isHost: false,
      agreed: false
    });

    socket.join(roomId);
    socket.emit('joined_room', { roomId });
    io.to(roomId).emit('room_updated', getRoomStatus(roomId));
  });

  // ── Get Active Rooms List ──
  socket.on('get_active_rooms', () => {
    const active = [];
    for (const [rid, room] of Object.entries(rooms)) {
      if (room.sockets.size > 0) {
        active.push({
          roomId: rid,
          name: room.name,
          playerCount: room.sockets.size,
          maxPlayers: room.maxPlayers,
          hasPassword: room.password !== null,
          isFull: room.sockets.size >= room.maxPlayers
        });
      }
    }
    socket.emit('active_rooms_list', { rooms: active });
  });

  // ── Leave Room ──
  socket.on('leave_room', () => {
    for (const [rid, room] of Object.entries(rooms)) {
      if (room.sockets.has(socket.id)) {
        const wasHost = room.host === socket.id;
        room.sockets.delete(socket.id);
        socket.leave(rid);

        if (wasHost && room.sockets.size > 0) {
          // Transfer host to first remaining player
          const newHostId = room.sockets.keys().next().value;
          room.host = newHostId;
          room.sockets.get(newHostId).isHost = true;
          io.to(rid).emit('host_changed', { newHostId });
        }

        if (room.sockets.size === 0) {
          delete rooms[rid];
        } else {
          io.to(rid).emit('room_updated', getRoomStatus(rid));
        }
        break;
      }
    }
  });

  // ── Update Player Name ──
  socket.on('update_name', (data) => {
    for (const [rid, room] of Object.entries(rooms)) {
      if (room.sockets.has(socket.id)) {
        room.sockets.get(socket.id).name = data.name;
        touchRoom(rid);
        io.to(rid).emit('room_updated', getRoomStatus(rid));
        break;
      }
    }
  });

  // ── Host: Select Roles ──
  socket.on('select_roles', (data) => {
    for (const [rid, room] of Object.entries(rooms)) {
      if (room.sockets.has(socket.id) && room.sockets.get(socket.id).isHost) {
        const { roleIds } = data;
        // Validate: at least 1 werewolf or vampire, and enough roles for players
        const numPlayers = room.maxPlayers;
        const validRoles = roleIds.filter(rid => ROLES[rid]);

        // Count non-filler roles
        const nonFiller = validRoles.filter(r => !MULTI_ROLE_IDS.includes(r));
        const fillerCount = numPlayers - nonFiller.length;

        if (fillerCount < 0) {
          socket.emit('select_roles_error', { message: 'Too many special roles for the number of players.' });
          return;
        }

        // Add filler villager roles
        const finalRoles = [...nonFiller];
        for (let i = 0; i < fillerCount; i++) {
          finalRoles.push('villager');
        }

        // Ensure at least 1 wolf or vampire
        const hasWolf = finalRoles.some(r => ROLES[r] && (ROLES[r].isWolf || ROLES[r].team === 'werewolf'));
        const hasVampire = finalRoles.some(r => ROLES[r] && ROLES[r].isVampire);
        if (!hasWolf && !hasVampire) {
          socket.emit('select_roles_error', { message: 'You must select at least 1 Werewolf or Vampire.' });
          return;
        }

        room.selectedRoles = finalRoles;
        room.assignedRoles = null; // reset assignment
        touchRoom(rid);
        io.to(rid).emit('roles_selected', { roleIds: finalRoles });
        io.to(rid).emit('room_updated', getRoomStatus(rid));

        // If all players have agreed, enable start
        checkAllAgreed(rid);
        break;
      }
    }
  });

  // ── Player: Agree to roles ──
  socket.on('agree_roles', () => {
    for (const [rid, room] of Object.entries(rooms)) {
      if (room.sockets.has(socket.id)) {
        room.sockets.get(socket.id).agreed = true;
        touchRoom(rid);
        io.to(rid).emit('room_updated', getRoomStatus(rid));
        checkAllAgreed(rid);
        break;
      }
    }
  });

  // ── Host: Start Game ──
  socket.on('start_game', () => {
    for (const [rid, room] of Object.entries(rooms)) {
      if (room.sockets.has(socket.id) && room.sockets.get(socket.id).isHost) {
        if (room.gameState !== 'lobby') {
          socket.emit('start_error', { message: 'Game already started.' });
          return;
        }
        if (!room.selectedRoles || room.selectedRoles.length === 0) {
          socket.emit('start_error', { message: 'Chưa chọn vai cho trò chơi.' });
          return;
        }

        // Check minimum players
        const minPlayers = 5;
        if (room.sockets.size < minPlayers) {
          socket.emit('start_error', { message: `Cần ít nhất ${minPlayers} người chơi để bắt đầu (hiện có ${room.sockets.size}).` });
          return;
        }

        // Check all agreed
        let allAgreed = true;
        for (const [sid, player] of room.sockets) {
          if (!player.agreed) { allAgreed = false; break; }
        }
        if (!allAgreed) {
          socket.emit('start_error', { message: 'Not all players have agreed to the roles.' });
          return;
        }

        // Assign roles randomly
        assignRoles(rid);
        room.gameState = 'role_reveal';
        room.phaseStartTime = Date.now();

        // Reveal roles to all players
        revealRolesToPlayers(rid);

        io.to(rid).emit('room_updated', getRoomStatus(rid));
        touchRoom(rid);
        break;
      }
    }
  });

  // ── Night Phase Actions ──
  socket.on('night_action', (data) => {
    for (const [rid, room] of Object.entries(rooms)) {
      if (room.sockets.has(socket.id)) {
        const player = room.sockets.get(socket.id);
        const roleId = player.role;
        const role = ROLES[roleId];

        if (!role || !role.action) return;
        if (room.gameState !== 'night') return;

        const action = role.action;
        let result = null;

        if (action === 'choose_one') {
          const targetId = data.targetId;
          if (targetId && room.sockets.has(targetId) && !room.eliminated.has(targetId)) {
            result = { type: 'choose_one', targetId };
          }
        } else if (action === 'choose_two') {
          const targetIds = data.targetIds || [];
          if (Array.isArray(targetIds) && targetIds.length === 2) {
            const valid = targetIds.every(tid => room.sockets.has(tid) && !room.eliminated.has(tid));
            if (valid) result = { type: 'choose_two', targetIds };
          }
        } else if (action === 'choose_team') {
          const team = data.team;
          if (['villager', 'werewolf', 'vampire'].includes(team)) {
            result = { type: 'choose_team', team };
          }
        } else if (action === 'choose_side') {
          const side = data.side;
          if (['villager', 'werewolf'].includes(side)) {
            result = { type: 'choose_side', side };
            // Bigfoot switches team
            player.team = side;
            player.switchedTeam = true;
          }
        } else if (action === 'witch_action') {
          const witchAction = data.witchAction; // 'save' or 'kill'
          const targetId = data.targetId;
          if (['save', 'kill'].includes(witchAction) && targetId) {
            if (witchAction === 'save') {
              result = { type: 'witch_save', targetId };
            } else {
              result = { type: 'witch_kill', targetId };
            }
          }
        } else if (action === 'choose_one_then_role') {
          // Shaman: choose a player, then choose a role to give them
          const targetId = data.targetId;
          const newRoleId = data.newRoleId;
          if (targetId && newRoleId && ROLES[newRoleId]) {
            result = { type: 'shaman', targetId, newRoleId };
          }
        }

        if (result) {
          room.nightActions[socket.id] = result;
          player.nightActionDone = true;
          touchRoom(rid);
        }

        // Check if all night actions are done
        checkNightComplete(rid);
        break;
      }
    }
  });

  // ── Werewolf pack communication (for sorcerer/mafioso) ──
  socket.on('wolf_chat', (data) => {
    for (const [rid, room] of Object.entries(rooms)) {
      if (room.sockets.has(socket.id)) {
        const player = room.sockets.get(socket.id);
        const roleId = player.realRole || player.role;
        const role = ROLES[roleId];

        if (room.gameState === 'night' &&
            (role.canTalkToWolves || role.knowsWolves || role.winsWithWolves || player.team === 'werewolf')) {
          // Broadcast to all wolf-aligned players in the room
          const msg = {
            from: player.name,
            message: data.message,
            night: room.currentNight
          };
          for (const [sid, p] of room.sockets) {
            const rp = ROLES[p.realRole || p.role];
            if (rp && (rp.isWolf || rp.isVampire || rp.canTalkToWolves || rp.knowsWolves || rp.winsWithWolves)) {
              io.to(sid).emit('wolf_chat', msg);
            }
          }
        }
        break;
      }
    }
  });

  // ── Host: Advance to Night ──
  socket.on('advance_to_night', () => {
    for (const [rid, room] of Object.entries(rooms)) {
      if (room.sockets.has(socket.id) && room.sockets.get(socket.id).isHost) {
        if (room.gameState !== 'day' && room.gameState !== 'role_reveal') return;

        room.currentNight++;
        room.gameState = 'night';
        room.phaseStartTime = Date.now();
        room.nightActions = {};
        room.wolfRevengeNight = false; // reset each night (baby wolf revenge is tracked per-night)

        // Check if baby wolf was hanged last day -> revenge night
        const lastVote = room.votedOut[room.votedOut.length - 1];
        if (lastVote && lastVote.roleId === 'baby_wolf') {
          room.wolfRevengeNight = true;
        }

        // If Bigfoot hasn't switched yet and this is night 2, force reveal
        // (handled client-side)

        // Discord announcement
        let discordMsg = `🌙 **Night ${room.currentNight}** begins!\n`;
        if (room.wolfRevengeNight) {
          discordMsg += '🔥 *The wolf pack is angry! All werewolves may kill 2 players tonight!* 🔥\n';
        }
        sendDiscordWebhook(room, discordMsg);

        // Notify all players
        io.to(rid).emit('night_started', {
          night: room.currentNight,
          wolfRevenge: room.wolfRevengeNight,
          playersAlive: getAlivePlayers(rid)
        });

        io.to(rid).emit('room_updated', getRoomStatus(rid));
        touchRoom(rid);
        break;
      }
    }
  });

  // ── Host: Check Night Complete → Advance to Day ──
  socket.on('check_night_done', () => {
    for (const [rid, room] of Object.entries(rooms)) {
      if (room.sockets.has(socket.id) && room.sockets.get(socket.id).isHost) {
        checkNightComplete(rid);
        break;
      }
    }
  });

  // ── Host: Advance to Voting (Day Phase) ──
  socket.on('advance_to_voting', () => {
    for (const [rid, room] of Object.entries(rooms)) {
      if (room.sockets.has(socket.id) && room.sockets.get(socket.id).isHost) {
        if (room.gameState !== 'night') return;

        // Process night results
        processNightResults(rid);

        room.gameState = 'voting';
        room.votes = {};
        room.phaseStartTime = Date.now();
        room.voteTimer = Date.now() + 60000; // 60 second vote

        // Discord announcement
        const aliveCount = getAlivePlayers(rid).length;
        sendDiscordWebhook(room, `☀️ **Day ${room.currentNight}** begins! ${aliveCount} players remain. Discuss and vote.`);

        // Send day start to all players
        io.to(rid).emit('day_started', {
          night: room.currentNight,
          playersAlive: getAlivePlayers(rid),
          voteTime: 60
        });

        io.to(rid).emit('room_updated', getRoomStatus(rid));
        touchRoom(rid);
        break;
      }
    }
  });

  // ── Vote ──
  socket.on('vote', (data) => {
    for (const [rid, room] of Object.entries(rooms)) {
      if (room.sockets.has(socket.id)) {
        const player = room.sockets.get(socket.id);

        if (room.gameState !== 'voting') return;
        if (room.eliminated.has(socket.id)) return;
        if (player.cannotVote) {
          socket.emit('vote_error', { message: 'Peace Lover cannot vote.' });
          return;
        }

        const targetId = data.targetId;
        if (!targetId || room.eliminated.has(targetId)) {
          socket.emit('vote_error', { message: 'Invalid target.' });
          return;
        }

        room.votes[socket.id] = targetId;
        touchRoom(rid);
        io.to(rid).emit('room_updated', getRoomStatus(rid));
        break;
      }
    }
  });

  // ── Host: End Voting ──
  socket.on('end_voting', () => {
    for (const [rid, room] of Object.entries(rooms)) {
      if (room.sockets.has(socket.id) && room.sockets.get(socket.id).isHost) {
        if (room.gameState !== 'voting') return;
        processVotingResult(rid);
        break;
      }
    }
  });

  // ── Host: Start Next Round ──
  socket.on('next_round', () => {
    for (const [rid, room] of Object.entries(rooms)) {
      if (room.sockets.has(socket.id) && room.sockets.get(socket.id).isHost) {
        const alive = getAlivePlayers(rid);

        // Check win conditions
        const winResult = checkWinCondition(rid);
        if (winResult) {
          room.gameState = 'gameover';
          io.to(rid).emit('game_over', winResult);
          sendDiscordWebhook(room, `🏆 **Game Over!** ${winResult.winTeam} wins!`);
          return;
        }

        if (alive.length <= 1) {
          room.gameState = 'gameover';
          io.to(rid).emit('game_over', {
            winTeam: 'villager',
            message: 'Only one player remains. Villagers win by default.',
            winners: alive
          });
          return;
        }

        // Reset for next round — re-assign roles randomly
        assignRoles(rid);
        room.gameState = 'day'; // host advances to night
        room.eliminated = new Set();
        room.votedOut = [];
        room.nightActions = {};

        io.to(rid).emit('room_updated', getRoomStatus(rid));
        touchRoom(rid);
        break;
      }
    }
  });

  // ── Disconnect ──
  socket.on('disconnect', () => {
    console.log('Client disconnected:', socket.id);
    for (const [rid, room] of Object.entries(rooms)) {
      if (room.sockets.has(socket.id)) {
        const wasHost = room.host === socket.id;
        room.sockets.delete(socket.id);
        touchRoom(rid);

        if (wasHost && room.sockets.size > 0) {
          const newHostId = room.sockets.keys().next().value;
          room.host = newHostId;
          room.sockets.get(newHostId).isHost = true;
          io.to(rid).emit('host_changed', { newHostId });
        }

        if (room.sockets.size === 0) {
          delete rooms[rid];
        } else {
          io.to(rid).emit('room_updated', getRoomStatus(rid));
        }
        break;
      }
    }
  });
});

// ─── Game Logic Helpers ─────────────────────────────────────────────────────

function assignRoles(roomId) {
  const room = rooms[roomId];
  const aliveSockets = [];
  for (const [sid, player] of room.sockets) {
    aliveSockets.push(sid);
  }

  // Shuffle the role list
  const roles = [...room.selectedRoles];
  for (let i = roles.length - 1; i > 0; i--) {
    const j = Math.floor(Math.random() * (i + 1));
    [roles[i], roles[j]] = [roles[j], roles[i]];
  }

  // Assign roles to players
  room.assignments = {};
  for (let i = 0; i < aliveSockets.length; i++) {
    room.assignments[aliveSockets[i]] = roles[i % roles.length];
  }
}

function getAlivePlayers(roomId) {
  const room = rooms[roomId];
  const alive = [];
  for (const [sid, player] of room.sockets) {
    if (!room.eliminated.has(sid)) {
      alive.push({ id: sid, name: player.name, role: player.role, team: player.team });
    }
  }
  return alive;
}

function checkNightComplete(roomId) {
  const room = rooms[roomId];
  if (room.gameState !== 'night') return;

  let allDone = true;
  for (const [sid, player] of room.sockets) {
    if (room.eliminated.has(sid)) continue;
    const roleId = player.realRole || player.role;
    const role = ROLES[roleId];
    if (role && role.action && !player.nightActionDone) {
      allDone = false;
      break;
    }
  }

  if (allDone) {
    // Auto-advance after a short delay so players can see results
    setTimeout(() => {
      if (rooms[roomId] && rooms[roomId].gameState === 'night') {
        processNightResults(roomId);
        rooms[roomId].gameState = 'day';
        rooms[roomId].phaseStartTime = Date.now();

        // Discord
        sendDiscordWebhook(rooms[roomId], `🌅 **Night ${rooms[roomId].currentNight}** is over. Day ${rooms[roomId].currentNight} begins!`);

        io.to(roomId).emit('day_started_auto', {
          night: rooms[roomId].currentNight,
          playersAlive: getAlivePlayers(roomId)
        });
        io.to(roomId).emit('room_updated', getRoomStatus(roomId));
        touchRoom(roomId);
      }
    }, 3000);
  }
}

function processNightResults(roomId) {
  const room = rooms[roomId];
  const results = [];
  const killed = [];

  // Process each night action
  for (const [sid, action] of room.nightActions) {
    const player = room.sockets.get(sid);
    const roleId = player.realRole || player.role;
    const role = ROLES[roleId];

    if (!role) continue;

    if (action.type === 'choose_one') {
      // Werewolf/Vampire/Seer/Doctor/etc. target
      const target = room.sockets.get(action.targetId);
      if (target) {
        results.push({
          actor: player.name,
          actorRole: role.name,
          action: `${role.name} targeted ${target.name}`,
          targetId: action.targetId
        });

        // Doctor save check
        const doctorSave = checkDoctorSave(room, action.targetId);
        if (doctorSave) {
          results.push({ actor: 'Doctor', action: `saved ${target.name} from being killed` });
        } else if (role.isWolf || role.isVampire) {
          // Kill the target (unless immune)
          const targetRole = ROLES[target.realRole || target.role];
          if (targetRole && targetRole.immuneToWolf && !(role.isVampire)) {
            results.push({ actor: 'Mutant', action: `${target.name} is immune to wolf attacks` });
          } else {
            killed.push(action.targetId);
            results.push({ actor: role.name, action: `killed ${target.name}` });
          }
        }
      }
    } else if (action.type === 'choose_two') {
      if (role.isWolf || role.isVampire) {
        // Wolf Alpha or revenge night: kill 2
        for (const tid of action.targetIds) {
          const target = room.sockets.get(tid);
          if (target) {
            const targetRole = ROLES[target.realRole || target.role];
            if (targetRole && targetRole.immuneToWolf && !role.isVampire) {
              results.push({ actor: 'Mutant', action: `${target.name} is immune to wolf attacks` });
            } else {
              killed.push(tid);
              results.push({ actor: role.name, action: `killed ${target.name}` });
            }
          }
        }
      } else if (role.action === 'choose_two') {
        // Cupid pairs
        results.push({
          actor: player.name,
          actorRole: 'Cupid',
          action: `paired ${action.targetIds[0]} and ${action.targetIds[1]} as lovers`
        });
        // Store lovers relationship
        if (!room.lovers) room.lovers = {};
        room.lovers[action.targetIds[0]] = action.targetIds[1];
        room.lovers[action.targetIds[1]] = action.targetIds[0];
      }
    } else if (action.type === 'choose_team') {
      results.push({
        actor: player.name,
        actorRole: 'Prophet',
        action: `saw all ${action.team} team members`
      });
    } else if (action.type === 'choose_side') {
      results.push({
        actor: player.name,
        actorRole: 'Bigfoot',
        action: `chose to join the ${action.side} team`
      });
    } else if (action.type === 'witch_save') {
      results.push({ actor: 'Witch', action: `saved ${room.sockets.get(action.targetId)?.name || 'unknown'}` });
    } else if (action.type === 'witch_kill') {
      const target = room.sockets.get(action.targetId);
      if (target) {
        killed.push(action.targetId);
        results.push({ actor: 'Witch', action: `killed ${target.name}` });
      }
    } else if (action.type === 'shaman') {
      const target = room.sockets.get(action.targetId);
      const newRole = ROLES[action.newRoleId];
      if (target && newRole) {
        target.role = action.newRoleId;
        target.team = newRole.team;
        target.realRole = action.newRoleId;
        results.push({
          actor: player.name,
          actorRole: 'Shaman',
          action: `gave ${target.name} the role of ${newRole.name}`
        });
      }
    }
  }

  // Process kills (eliminate players)
  for (const kid of killed) {
    if (!room.eliminated.has(kid)) {
      room.eliminated.add(kid);
      const killedPlayer = room.sockets.get(kid);

      // Hunter retaliation
      if (killedPlayer && ROLES[killedPlayer.realRole || killedPlayer.role]?.onElimination === 'shoot') {
        results.push({ actor: 'Hunter', action: `${killedPlayer.name} (Hunter) is eliminated! Hunter will shoot someone...` });
        // Hunter shoot is handled during voting/elimination phase
        room.hunterRetaliation = kid; // mark that hunter needs to shoot
      }

      // Jester / Fool win if hanged (handled in voting, not night)
      // Baby wolf revenge
      if (ROLES[killedPlayer?.realRole || killedPlayer?.role]?.revengeKill) {
        room.wolfRevengeNight = true;
        results.push({ actor: 'Baby Wolf', action: `${killedPlayer.name} was a Baby Wolf! The wolf pack will be angry tonight!` });
      }

      // Lovers: if one dies, the other dies too
      if (room.lovers && room.lovers[kid]) {
        const loverId = room.lovers[kid];
        if (!room.eliminated.has(loverId)) {
          room.eliminated.add(loverId);
          const lover = room.sockets.get(loverId);
          results.push({ actor: 'Cupid', action: `Lovers: ${lover?.name || 'Unknown'} also dies because their lover was killed` });

          // Hunter retaliation for lover too
          if (lover && ROLES[lover.realRole || lover.role]?.onElimination === 'shoot') {
            room.hunterRetaliation = loverId;
          }
        }
      }

      // If killed player is a Hunter, they need to shoot
      if (killedPlayer && ROLES[killedPlayer.realRole || killedPlayer.role]?.onElimination === 'shoot') {
        room.hunterRetaliation = kid;
      }
    }
  }

  // Store results for public display
  room.nightResults = results;
  room.killedThisNight = killed;

  // Notify players of night results (without revealing roles)
  io.to(roomId).emit('night_results', {
    results: results.map(r => ({
      action: r.action,
      actor: r.actor === 'Doctor' || r.actor === 'Witch' || r.actor === 'Hunter' || r.actor === 'Mutant' || r.actor === 'Cupid' || r.actor === 'Baby Wolf' ? r.actor : 'Unknown'
    })),
    killed: killed.map(kid => room.sockets.get(kid)?.name || 'Unknown'),
    wolfRevenge: room.wolfRevengeNight
  });

  // Handle Hunter retaliation (ask hunter who to shoot)
  if (room.hunterRetaliation && room.gameState === 'day') {
    // Find the hunter among eliminated
    for (const [sid, player] of room.sockets) {
      if (room.eliminated.has(sid) && ROLES[player.realRole || player.role]?.onElimination === 'shoot') {
        io.to(sid).emit('hunter_shoot_prompt', { targetId: room.hunterRetaliation });
      }
    }
  }
}

function checkDoctorSave(room, targetId) {
  // Check if any doctor saved this target (can't save same person two nights in a row)
  for (const [sid, action] of room.nightActions) {
    const player = room.sockets.get(sid);
    const role = ROLES[player.realRole || player.role];
    if (role && role.id === 'doctor' && action.type === 'choose_one' && action.targetId === targetId) {
      return true;
    }
  }
  return false;
}

function processVotingResult(roomId) {
  const room = rooms[roomId];
  if (room.gameState !== 'voting') return;

  // Count votes
  const voteCounts = {};
  for (const [voterId, targetId] of room.votes) {
    if (!voteCounts[targetId]) voteCounts[targetId] = 0;
    voteCounts[targetId]++;
  }

  // Find the player with most votes
  let maxVotes = 0;
  let votedOutId = null;
  for (const [tid, count] of Object.entries(voteCounts)) {
    if (count > maxVotes) {
      maxVotes = count;
      votedOutId = tid;
    }
  }

  // Check if Jester or Fool wins by being hanged
  let specialWinner = null;
  if (votedOutId) {
    const votedOutPlayer = room.sockets.get(votedOutId);
    const role = ROLES[votedOutPlayer?.realRole || votedOutPlayer?.role];
    if (role?.winsIfHanged) {
      specialWinner = { id: votedOutId, name: votedOutPlayer?.name, role: role.name };
    }
  }

  // Eliminate the voted-out player
  if (votedOutId && !room.eliminated.has(votedOutId)) {
    room.eliminated.add(votedOutId);
    const votedOutPlayer = room.sockets.get(votedOutId);

    // Handle Jester/Fool win
    if (specialWinner) {
      room.gameState = 'gameover';
      const winResult = {
        winTeam: 'jester',
        message: `${specialWinner.name} (${specialWinner.role}) was hanged and wins!`,
        winners: [specialWinner.id],
        eliminated: votedOutId
      };
      io.to(roomId).emit('game_over', winResult);
      sendDiscordWebhook(room, `🏆 **Game Over!** ${specialWinner.name} (${specialWinner.role}) wins by being hanged!`);
      return;
    }

    // Hunter retaliation
    if (ROLES[votedOutPlayer?.realRole || votedOutPlayer?.role]?.onElimination === 'shoot') {
      // Hunter shoots someone during elimination
      room.hunterRetaliation = votedOutId;
    }

    // Lovers
    if (room.lovers && room.lovers[votedOutId]) {
      const loverId = room.lovers[votedOutId];
      if (!room.eliminated.has(loverId)) {
        room.eliminated.add(loverId);
        const lover = room.sockets.get(loverId);
        io.to(roomId).emit('lover_died', { name: lover?.name });

        if (ROLES[lover?.realRole || lover?.role]?.onElimination === 'shoot') {
          room.hunterRetaliation = loverId;
        }
      }
    }

    room.votedOut.push({
      playerId: votedOutId,
      playerName: votedOutPlayer?.name,
      roleId: votedOutPlayer?.realRole || votedOutPlayer?.role,
      roleName: ROLES[votedOutPlayer?.realRole || votedOutPlayer?.role]?.name || 'Unknown',
      team: ROLES[votedOutPlayer?.realRole || votedOutPlayer?.role]?.team || 'unknown',
      votes: maxVotes
    });
  }

  // Handle Hunter retaliation (shoot someone)
  if (room.hunterRetaliation) {
    // Find the hunter
    for (const [sid, player] of room.sockets) {
      if (room.eliminated.has(sid) && ROLES[player.realRole || player.role]?.onElimination === 'shoot') {
        // Hunter is eliminated, they need to choose who to shoot
        // For simplicity, hunter shoots the player with most votes among remaining
        // Or we can ask the hunter via a prompt
        io.to(sid).emit('hunter_shoot_prompt', { targetId: room.hunterRetaliation });
        return; // Wait for hunter response
      }
    }
  }

  // Check win conditions
  const winResult = checkWinCondition(roomId);
  if (winResult) {
    room.gameState = 'gameover';
    io.to(roomId).emit('game_over', winResult);
    sendDiscordWebhook(room, `🏆 **Game Over!** ${winResult.winTeam} wins!`);
    return;
  }

  // Proceed to next round
  room.gameState = 'day';
  io.to(roomId).emit('voting_complete', {
    votedOut: room.votedOut[room.votedOut.length - 1],
    eliminated: [...room.eliminated],
    playersAlive: getAlivePlayers(roomId)
  });
  io.to(roomId).emit('room_updated', getRoomStatus(roomId));
  touchRoom(roomId);
}

function checkWinCondition(roomId) {
  const room = rooms[roomId];
  const alive = getAlivePlayers(roomId);

  if (alive.length === 0) return null;

  // Count teams among alive players
  const teamCounts = { villager: 0, werewolf: 0, vampire: 0, neutral: 0 };
  for (const p of alive) {
    const role = ROLES[p.role || p.realRole];
    const team = role?.team || 'neutral';
    teamCounts[team]++;
  }

  const totalAlive = alive.length;

  // Villager win: all werewolves and vampires eliminated
  if (teamCounts.werewolf === 0 && teamCounts.vampire === 0) {
    return {
      winTeam: 'villager',
      message: 'All werewolves and vampires have been eliminated! Villagers win!',
      winners: alive.map(p => p.id),
      teamCounts
    };
  }

  // Werewolf win: werewolves + vampires >= villagers
  if (teamCounts.werewolf + teamCounts.vampire >= teamCounts.villager) {
    return {
      winTeam: 'werewolf',
      message: 'Werewolves and vampires outnumber the villagers! Werewolves win!',
      winners: alive.filter(p => {
        const r = ROLES[p.role || p.realRole];
        return r?.team === 'werewolf' || r?.team === 'vampire';
      }).map(p => p.id),
      teamCounts
    };
  }

  // Vampire win: all other players dead
  if (teamCounts.vampire > 0 && totalAlive === teamCounts.vampire) {
    return {
      winTeam: 'vampire',
      message: 'All other players are dead! Vampires win!',
      winners: alive.filter(p => {
        const r = ROLES[p.role || p.realRole];
        return r?.team === 'vampire';
      }).map(p => p.id),
      teamCounts
    };
  }

  // Neutral wins (Jester already handled, Fool already handled)
  // Huntress wins if survives alone
  const huntressAlive = alive.filter(p => {
    const r = ROLES[p.role || p.realRole];
    return r?.id === 'huntress';
  });
  if (huntressAlive.length > 0 && alive.length === 1) {
    return {
      winTeam: 'huntress',
      message: 'The Huntress survives alone! Huntress wins!',
      winners: huntressAlive.map(p => p.id),
      teamCounts
    };
  }

  return null;
}

function checkAllAgreed(roomId) {
  const room = rooms[roomId];
  if (!room || room.gameState !== 'lobby') return;

  let allAgreed = true;
  for (const [sid, player] of room.sockets) {
    if (!player.agreed) { allAgreed = false; break; }
  }

  if (allAgreed && room.selectedRoles && room.selectedRoles.length > 0) {
    io.to(roomId).emit('all_agreed', { ready: true });
  }
}

function getRoomStatus(roomId) {
  const room = rooms[roomId];
  if (!room) return null;

  const players = [];
  for (const [sid, player] of room.sockets) {
    players.push({
      id: sid,
      name: player.name,
      isHost: player.isHost,
      agreed: player.agreed,
      role: player.role ? ROLES[player.role]?.name : null,
      team: player.team,
      eliminated: room.eliminated.has(sid)
    });
  }

  const allAgreed = players.every(p => p.agreed);

  return {
    id: room.id,
    name: room.name,
    host: room.host,
    maxPlayers: room.maxPlayers,
    playerCount: room.sockets.size,
    players: players,
    selectedRoles: room.selectedRoles,
    gameState: room.gameState,
    currentNight: room.currentNight,
    allAgreed: allAgreed,
    discordWebhook: room.discordWebhook,
    aliveCount: getAlivePlayers(roomId).length
  };
}

// ─── Start Server ───────────────────────────────────────────────────────────
const PORT = process.env.PORT || 3000;
server.listen(PORT, '0.0.0.0', () => {
  console.log(`Werewolf game server running on port ${PORT}`);
  console.log(`http://localhost:${PORT}`);
});
