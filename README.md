const express = require("express");
const axios = require("axios");
const app = express();
const port = process.env.PORT || 3000;

const BOT_TOKEN = "8445873582:AAEMhQJwA-Qk7SRVLkkvWjZPtAi5WYQuKV0";
const CHAT_ID = "241553097";

app.get("/", (req, res) => {
  res.send("✅ Alpha Sniper Bot Running");
});

app.get("/send", async (req, res) => {
  const message = `
🚨 *Alpha Sniper Signal Alert*

📉 *Asset:* EUR/USD  
📍 *Signal:* PUT ⬇️  
🧠 *Reason:* Top Wick + Fractal Resistance + Chaos Rejection  
⏰ *Entry Time:* Next 2–3 minutes

✅ *Confirm Before Entry:*
- [✔] Top Wick Rejection?  
- [✔] Fractal Arrow Present?  
- [✔] Chaos Direction Matches?  
- [✔] Entry after candle closes?

🎯 *If all 4 are ✅ → Enter trade sniper-style*
`;
  try {
    await axios.post(`https://api.telegram.org/bot${BOT_TOKEN}/sendMessage`, {
      chat_id: CHAT_ID,
      text: message,
      parse_mode: "Markdown"
    });
    res.send("✅ Signal sent to Telegram!");
  } catch (err) {
    console.error(err.message);
    res.status(500).send("❌ Failed to send signal.");
  }
});

app.listen(port, () => {
  console.log(`Bot is live on port ${port}`);
});
