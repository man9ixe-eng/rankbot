import express from "express";
import noblox from "noblox.js";
import bodyParser from "body-parser";

const app = express();
app.use(bodyParser.json());

const COOKIE = process.env.BOT_COOKIE;
const API_KEY = process.env.API_KEY;
const PORT = process.env.PORT || 3000;

(async () => {
  await noblox.setCookie(COOKIE);
  console.log("✅ Logged in as:", await noblox.getCurrentUser());
})();

app.post("/rank", async (req, res) => {
  const { groupId, targetId, newRank, requestedBy, key } = req.body;
  if (key !== API_KEY) return res.status(403).send("Invalid key");

  try {
    await noblox.setRank(groupId, targetId, newRank);
    console.log(`${requestedBy} ranked ${targetId} -> ${newRank}`);
    res.send("Ranked successfully");
  } catch (e) {
    console.error(e);
    res.status(500).send(e.toString());
  }
});

app.listen(PORT, () => console.log(`✅ Rank Bot running on port ${PORT}`));
