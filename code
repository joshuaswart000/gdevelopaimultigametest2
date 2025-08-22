// server.js
import express from "express";
import cors from "cors";
import { initializeApp } from "firebase/app";
import { getAI, getGenerativeModel, GoogleAIBackend } from "firebase/ai";

const app = express();
app.use(cors());
app.use(express.json()); // parse JSON bodies

// Firebase config
const firebaseConfig = {
  apiKey: "YOUR_API_KEY",
  authDomain: "multi-game-gdevelop.firebaseapp.com",
  projectId: "multi-game-gdevelop",
  storageBucket: "multi-game-gdevelop.firebasestorage.app",
  messagingSenderId: "260214790439",
  appId: "1:260214790439:web:5a462b947fa93846d5f102",
  measurementId: "G-4MCBDQ2DFP"
};

// Initialize Firebase
const firebaseApp = initializeApp(firebaseConfig);
const ai = getAI(firebaseApp, { backend: new GoogleAIBackend() });
const model = getGenerativeModel(ai, { model: "gemini-2.5-flash" });

// Endpoint for GDevelop
app.post("/ask", async (req, res) => {
  const prompt = req.body.prompt;
  if (!prompt) return res.status(400).json({ error: "No prompt provided" });

  try {
    const result = await model.generateContent(prompt);
    const text = result.response.text();
    res.json({ reply: text });
  } catch (e) {
    res.status(500).json({ error: e.message });
  }
});

const PORT = process.env.PORT || 3000;
app.listen(PORT, () => console.log(`Server running on port ${PORT}`));
