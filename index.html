‎
‎module.exports = async function handler(req, res) {
‎  res.setHeader("Cache-Control", "no-store");
‎
‎  if (req.method !== "POST") {
‎    res.setHeader("Allow", "POST");
‎    return res.status(405).json({
‎      error: "Sirf POST request allowed hai."
‎    });
‎  }
‎
‎  const apiKey = process.env.GROQ_API_KEY;
‎
‎  if (!apiKey) {
‎    return res.status(500).json({
‎      error: "Vercel mein GROQ_API_KEY set nahi hai."
‎    });
‎  }
‎
‎  try {
‎    const body = req.body || {};
‎    const messages = body.messages;
‎    const system = typeof body.system === "string"
‎      ? body.system.slice(0, 6000)
‎      : "Tum JANI ho, ek samajhdar aur friendly AI dost. User ki zaban mein jawab do.";
‎
‎    if (!Array.isArray(messages) || messages.length === 0) {
‎      return res.status(400).json({
‎        error: "Message khali hai. Dobara likho."
‎      });
‎    }
‎
‎    const cleanMessages = messages.slice(-24).map(function (msg) {
‎      if (
‎        !msg ||
‎        !["user", "assistant"].includes(msg.role) ||
‎        typeof msg.content !== "string"
‎      ) {
‎        throw new Error("Message format sahi nahi hai.");
‎      }
‎
‎      return {
‎        role: msg.role,
‎        content: msg.content.slice(0, 6000)
‎      };
‎    });
‎
‎    const response = await fetch(
‎      "https://api.groq.com/openai/v1/chat/completions",
‎      {
‎        method: "POST",
‎        headers: {
‎          "Authorization": "Bearer " + apiKey,
‎          "Content-Type": "application/json"
‎        },
‎        body: JSON.stringify({
‎          model: "llama-3.3-70b-versatile",
‎          messages: [
‎            {
‎              role: "system",
‎              content: system
‎            },
‎            ...cleanMessages
‎          ],
‎          temperature: 0.8,
‎          max_tokens: 1200
‎        })
‎      }
‎    );
‎
‎    const data = await response.json().catch(function () {
‎      return {};
‎    });
‎
‎    if (!response.ok) {
‎      console.error("Groq request failed:", response.status);
‎
‎      if (response.status === 401 || response.status === 403) {
‎        return res.status(502).json({
‎          error: "Groq API key invalid hai ya access nahi mila. Vercel settings check karo."
‎        });
‎      }
‎
‎      if (response.status === 429) {
‎        return res.status(429).json({
‎          error: "Groq ki request limit abhi poori hai. Thori dair baad koshish karo."
‎        });
‎      }
‎
‎      return res.status(502).json({
‎        error: "Groq AI se jawab nahi mila. Dobara koshish karo."
‎      });
‎    }
‎
‎    const reply = data.choices &&
‎      data.choices[0] &&
‎      data.choices[0].message &&
‎      data.choices[0].message.content;
‎
‎    if (typeof reply !== "string" || !reply.trim()) {
‎      return res.status(502).json({
‎        error: "AI ka jawab khali mila."
‎      });
‎    }
‎
‎    return res.status(200).json({
‎      reply: reply.trim()
‎    });
‎  } catch (error) {
‎    console.error("JANI API error:", error.message);
‎
‎    return res.status(500).json({
‎      error: "Server mein masla hua. Dobara koshish karo."
‎    });
‎  }
‎};
‎
