# Mimi Bot Commands

Welcome to Mimi Bot! Here’s a full list of currently available commands, what they do, and how to use them. For all commands, prefix them with `!` in your Discord server.

---

## 1. `!sus @user`
**Description:**  
Adds a "SUS" (suspicious) point to the mentioned user. Tracks who’s the most suspicious in your server.

**Data:**  
Stored in `commands/sus.json` as a mapping of Discord user IDs to their SUS score.

---

## 2. `!fact`
**Description:**  
Sends a random fun fact from a list.

**Data:**  
Facts are stored in `commands/facts.json` as an array of strings.

---

## 3. `!roast @user`
**Description:**  
Sends a random roast to the mentioned user. Use for friendly banter!

**Data:**  
Roasts are stored in `commands/roasts.json` as an array of strings.

---

## 4. `!complement @user`
**Description:**  
Sends a random compliment to the mentioned user. Spread some positivity!

**Data:**  
Compliments are stored in `commands/comp.json` as an array of strings.

---

## 5. `!insult @user`
**Description:**  
Sends a random lighthearted insult to the mentioned user. For jokes only—keep it fun!

**Data:**  
Insults are stored in `commands/insult.json` as an array of strings.

---

## Example Usage

```
!sus @Monday_Riot
!fact
!roast @friend
!complement @teammate
!insult @rival
```

---

## Notes

- All commands should be used in the spirit of fun and positivity.
- Mentioned users must be real users (not bots) for `!roast`, `!complement`, and `!insult`.
- If a command is not working, check that the relevant `.json` file exists and contains valid JSON.

---

Enjoy using Mimi Bot!
