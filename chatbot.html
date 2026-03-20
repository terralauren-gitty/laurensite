import { useState, useEffect, useRef } from "react";

const CATEGORIES = ["HR & Onboarding", "Culture & Values", "Role-Specific", "Benefits & Compensation"];

const DEFAULT_KB = [
  { id: 1, category: "HR & Onboarding", question: "What is the onboarding process?", answer: "New employees complete a 2-week onboarding program. Week 1 covers company orientation, tools setup, and meeting your team. Week 2 is role-specific training with your manager." },
  { id: 2, category: "HR & Onboarding", question: "How do I request time off?", answer: "Submit time-off requests through the HR portal at least 2 weeks in advance for planned leave. For sick days, notify your manager by 9am." },
  { id: 3, category: "Culture & Values", question: "What are the company core values?", answer: "Our core values are: Integrity (we do what we say), Innovation (we challenge the status quo), Collaboration (we win as a team), and Impact (we measure outcomes, not effort)." },
  { id: 4, category: "Benefits & Compensation", question: "When is payday?", answer: "Employees are paid bi-weekly on Fridays. The payroll cutoff is the Monday prior. Direct deposit is set up during onboarding." },
  { id: 5, category: "Benefits & Compensation", question: "What health benefits are offered?", answer: "We offer extended health, dental, and vision coverage from your first day. Coverage includes the employee and dependents. Full details are in the benefits guide in the HR portal." },
  { id: 6, category: "Role-Specific", question: "Who do I contact for IT support?", answer: "Reach IT support via the #it-help Slack channel or by emailing it@company.com. Response time is within 4 business hours." },
];

const STORAGE_KEY = "hr_chatbot_kb_v1";

const CategoryIcon = ({ cat }) => {
  const icons = {
    "HR & Onboarding": "🧭",
    "Culture & Values": "🌱",
    "Role-Specific": "🎯",
    "Benefits & Compensation": "💼",
  };
  return <span>{icons[cat] || "📋"}</span>;
};

export default function HRChatbot() {
  const [view, setView] = useState("chat"); // "chat" | "admin"
  const [kb, setKb] = useState([]);
  const [messages, setMessages] = useState([
    { role: "assistant", content: "Hi! I'm your internal company assistant. Ask me anything about HR policies, benefits, onboarding, company culture, or your role. How can I help you today?" }
  ]);
  const [input, setInput] = useState("");
  const [loading, setLoading] = useState(false);
  const [adminTab, setAdminTab] = useState(CATEGORIES[0]);
  const [editingId, setEditingId] = useState(null);
  const [form, setForm] = useState({ category: CATEGORIES[0], question: "", answer: "" });
  const [showAddForm, setShowAddForm] = useState(false);
  const bottomRef = useRef(null);

  useEffect(() => {
    try {
      const stored = localStorage.getItem(STORAGE_KEY);
      setKb(stored ? JSON.parse(stored) : DEFAULT_KB);
    } catch {
      setKb(DEFAULT_KB);
    }
  }, []);

  useEffect(() => {
    if (kb.length > 0) {
      try { localStorage.setItem(STORAGE_KEY, JSON.stringify(kb)); } catch {}
    }
  }, [kb]);

  useEffect(() => {
    bottomRef.current?.scrollIntoView({ behavior: "smooth" });
  }, [messages, loading]);

  const buildSystemPrompt = () => {
    const sections = CATEGORIES.map(cat => {
      const entries = kb.filter(e => e.category === cat);
      if (!entries.length) return "";
      return `## ${cat}\n` + entries.map(e => `Q: ${e.question}\nA: ${e.answer}`).join("\n\n");
    }).filter(Boolean).join("\n\n");

    return `You are a friendly, knowledgeable internal HR assistant for this company. Your job is to help employees and managers with questions about HR policies, onboarding, company culture, benefits, and role-specific topics.

Answer based on the knowledge base below. If a question isn't covered, say you don't have that information yet and suggest they contact HR directly. Keep answers concise, warm, and professional.

COMPANY KNOWLEDGE BASE:
${sections || "No knowledge base entries have been added yet."}`;
  };

  const sendMessage = async () => {
    if (!input.trim() || loading) return;
    const userMsg = { role: "user", content: input.trim() };
    const newMessages = [...messages, userMsg];
    setMessages(newMessages);
    setInput("");
    setLoading(true);

    try {
      const apiMessages = newMessages.map(m => ({ role: m.role, content: m.content }));
      const res = await fetch("https://api.anthropic.com/v1/messages", {
        method: "POST",
        headers: { "Content-Type": "application/json" },
        body: JSON.stringify({
          model: "claude-sonnet-4-20250514",
          max_tokens: 1000,
          system: buildSystemPrompt(),
          messages: apiMessages,
        }),
      });
      const data = await res.json();
      const reply = data.content?.[0]?.text || "Sorry, I couldn't generate a response. Please try again.";
      setMessages(prev => [...prev, { role: "assistant", content: reply }]);
    } catch {
      setMessages(prev => [...prev, { role: "assistant", content: "Something went wrong. Please check your connection and try again." }]);
    } finally {
      setLoading(false);
    }
  };

  const handleKeyDown = (e) => {
    if (e.key === "Enter" && !e.shiftKey) { e.preventDefault(); sendMessage(); }
  };

  const saveEntry = () => {
    if (!form.question.trim() || !form.answer.trim()) return;
    if (editingId !== null) {
      setKb(prev => prev.map(e => e.id === editingId ? { ...e, ...form } : e));
      setEditingId(null);
    } else {
      setKb(prev => [...prev, { id: Date.now(), ...form }]);
    }
    setForm({ category: adminTab, question: "", answer: "" });
    setShowAddForm(false);
  };

  const startEdit = (entry) => {
    setForm({ category: entry.category, question: entry.question, answer: entry.answer });
    setEditingId(entry.id);
    setShowAddForm(true);
    setAdminTab(entry.category);
  };

  const deleteEntry = (id) => {
    setKb(prev => prev.filter(e => e.id !== id));
    if (editingId === id) { setEditingId(null); setShowAddForm(false); }
  };

  const cancelForm = () => {
    setShowAddForm(false);
    setEditingId(null);
    setForm({ category: adminTab, question: "", answer: "" });
  };

  const tabEntries = kb.filter(e => e.category === adminTab);

  return (
    <div style={{
      fontFamily: "'DM Sans', 'Trebuchet MS', sans-serif",
      background: "#0f1117",
      minHeight: "100vh",
      display: "flex",
      flexDirection: "column",
      color: "#e8e4dc",
    }}>
      <style>{`
        @import url('https://fonts.googleapis.com/css2?family=DM+Sans:wght@300;400;500;600&family=Playfair+Display:wght@600&display=swap');
        * { box-sizing: border-box; margin: 0; padding: 0; }
        ::-webkit-scrollbar { width: 4px; }
        ::-webkit-scrollbar-track { background: transparent; }
        ::-webkit-scrollbar-thumb { background: #2a2d38; border-radius: 4px; }
        textarea:focus, input:focus { outline: none; }
        .msg-enter { animation: fadeUp 0.3s ease forwards; }
        @keyframes fadeUp { from { opacity: 0; transform: translateY(8px); } to { opacity: 1; transform: translateY(0); } }
        .kb-card:hover { background: #1e2130 !important; }
        .nav-btn:hover { background: rgba(215,178,106,0.1) !important; }
        .send-btn:hover:not(:disabled) { background: #c9a84c !important; }
        .tab-btn:hover { color: #d7b26a !important; }
        .action-btn:hover { opacity: 0.75; }
        .dot-pulse { display: flex; gap: 4px; align-items: center; padding: 4px 0; }
        .dot-pulse span { width: 7px; height: 7px; border-radius: 50%; background: #d7b26a; animation: pulse 1.2s infinite ease-in-out; }
        .dot-pulse span:nth-child(2) { animation-delay: 0.2s; }
        .dot-pulse span:nth-child(3) { animation-delay: 0.4s; }
        @keyframes pulse { 0%,80%,100% { opacity: 0.2; transform: scale(0.8); } 40% { opacity: 1; transform: scale(1); } }
      `}</style>

      {/* Header */}
      <div style={{ background: "#13161f", borderBottom: "1px solid #1e2130", padding: "0 24px", display: "flex", alignItems: "center", justifyContent: "space-between", height: 60 }}>
        <div style={{ display: "flex", alignItems: "center", gap: 12 }}>
          <div style={{ width: 32, height: 32, background: "linear-gradient(135deg, #d7b26a, #c9a84c)", borderRadius: 8, display: "flex", alignItems: "center", justifyContent: "center", fontSize: 16 }}>✦</div>
          <div>
            <div style={{ fontFamily: "'Playfair Display', serif", fontSize: 16, fontWeight: 600, color: "#e8e4dc", letterSpacing: "0.01em" }}>Company Assistant</div>
            <div style={{ fontSize: 11, color: "#5a6070", letterSpacing: "0.08em", textTransform: "uppercase" }}>Internal Knowledge Hub</div>
          </div>
        </div>
        <div style={{ display: "flex", gap: 4 }}>
          {["chat", "admin"].map(v => (
            <button key={v} className="nav-btn" onClick={() => setView(v)} style={{
              background: view === v ? "rgba(215,178,106,0.12)" : "transparent",
              border: view === v ? "1px solid rgba(215,178,106,0.3)" : "1px solid transparent",
              color: view === v ? "#d7b26a" : "#5a6070",
              padding: "6px 16px", borderRadius: 6, cursor: "pointer", fontSize: 13, fontWeight: 500,
              fontFamily: "inherit", transition: "all 0.2s",
            }}>
              {v === "chat" ? "💬 Chat" : "⚙️ Admin"}
            </button>
          ))}
        </div>
      </div>

      {/* Chat View */}
      {view === "chat" && (
        <div style={{ flex: 1, display: "flex", flexDirection: "column", maxWidth: 760, width: "100%", margin: "0 auto", padding: "0 16px" }}>
          {/* Quick topic chips */}
          <div style={{ display: "flex", gap: 8, padding: "16px 0 8px", flexWrap: "wrap" }}>
            {CATEGORIES.map(cat => (
              <button key={cat} onClick={() => setInput(`Tell me about ${cat}`)} style={{
                background: "#1a1d27", border: "1px solid #2a2d38", color: "#8890a0",
                padding: "5px 12px", borderRadius: 20, fontSize: 12, cursor: "pointer",
                fontFamily: "inherit", transition: "all 0.2s",
              }}
                onMouseOver={e => { e.target.style.borderColor = "#d7b26a55"; e.target.style.color = "#d7b26a"; }}
                onMouseOut={e => { e.target.style.borderColor = "#2a2d38"; e.target.style.color = "#8890a0"; }}
              >
                <CategoryIcon cat={cat} /> {cat}
              </button>
            ))}
          </div>

          {/* Messages */}
          <div style={{ flex: 1, overflowY: "auto", paddingBottom: 16, display: "flex", flexDirection: "column", gap: 16 }}>
            {messages.map((msg, i) => (
              <div key={i} className="msg-enter" style={{ display: "flex", gap: 12, flexDirection: msg.role === "user" ? "row-reverse" : "row", alignItems: "flex-start" }}>
                {msg.role === "assistant" && (
                  <div style={{ width: 32, height: 32, background: "linear-gradient(135deg, #d7b26a, #c9a84c)", borderRadius: 8, flexShrink: 0, display: "flex", alignItems: "center", justifyContent: "center", fontSize: 14, marginTop: 2 }}>✦</div>
                )}
                <div style={{
                  background: msg.role === "user" ? "#d7b26a" : "#1a1d27",
                  color: msg.role === "user" ? "#0f1117" : "#d8d4cc",
                  padding: "12px 16px", borderRadius: msg.role === "user" ? "18px 18px 4px 18px" : "18px 18px 18px 4px",
                  maxWidth: "75%", fontSize: 14, lineHeight: 1.65, fontWeight: msg.role === "user" ? 500 : 400,
                  border: msg.role === "assistant" ? "1px solid #2a2d38" : "none",
                  whiteSpace: "pre-wrap",
                }}>
                  {msg.content}
                </div>
              </div>
            ))}
            {loading && (
              <div style={{ display: "flex", gap: 12, alignItems: "flex-start" }}>
                <div style={{ width: 32, height: 32, background: "linear-gradient(135deg, #d7b26a, #c9a84c)", borderRadius: 8, flexShrink: 0, display: "flex", alignItems: "center", justifyContent: "center", fontSize: 14 }}>✦</div>
                <div style={{ background: "#1a1d27", border: "1px solid #2a2d38", padding: "12px 16px", borderRadius: "18px 18px 18px 4px" }}>
                  <div className="dot-pulse"><span /><span /><span /></div>
                </div>
              </div>
            )}
            <div ref={bottomRef} />
          </div>

          {/* Input */}
          <div style={{ padding: "12px 0 20px" }}>
            <div style={{ display: "flex", gap: 8, background: "#1a1d27", border: "1px solid #2a2d38", borderRadius: 12, padding: "4px 4px 4px 16px", transition: "border-color 0.2s" }}
              onFocus={e => e.currentTarget.style.borderColor = "#d7b26a55"}
              onBlur={e => e.currentTarget.style.borderColor = "#2a2d38"}
            >
              <textarea
                value={input}
                onChange={e => setInput(e.target.value)}
                onKeyDown={handleKeyDown}
                placeholder="Ask about onboarding, benefits, culture, your role..."
                rows={1}
                style={{
                  flex: 1, background: "transparent", border: "none", color: "#e8e4dc",
                  fontSize: 14, resize: "none", fontFamily: "inherit", lineHeight: 1.5, padding: "8px 0",
                  maxHeight: 120, overflowY: "auto",
                }}
                onInput={e => { e.target.style.height = "auto"; e.target.style.height = Math.min(e.target.scrollHeight, 120) + "px"; }}
              />
              <button className="send-btn" onClick={sendMessage} disabled={loading || !input.trim()} style={{
                background: "#d7b26a", border: "none", borderRadius: 8, width: 38, height: 38,
                cursor: loading || !input.trim() ? "not-allowed" : "pointer", opacity: loading || !input.trim() ? 0.4 : 1,
                display: "flex", alignItems: "center", justifyContent: "center", flexShrink: 0,
                alignSelf: "flex-end", marginBottom: 2, transition: "all 0.2s", fontSize: 16, color: "#0f1117",
              }}>↑</button>
            </div>
            <div style={{ textAlign: "center", fontSize: 11, color: "#3a3d48", marginTop: 8 }}>Press Enter to send · Shift+Enter for new line</div>
          </div>
        </div>
      )}

      {/* Admin View */}
      {view === "admin" && (
        <div style={{ flex: 1, maxWidth: 900, width: "100%", margin: "0 auto", padding: "24px 16px" }}>
          <div style={{ marginBottom: 24 }}>
            <div style={{ fontFamily: "'Playfair Display', serif", fontSize: 22, color: "#e8e4dc", marginBottom: 4 }}>Knowledge Base</div>
            <div style={{ fontSize: 13, color: "#5a6070" }}>{kb.length} entries across {CATEGORIES.length} categories — edit these to shape how the assistant responds</div>
          </div>

          {/* Category Tabs */}
          <div style={{ display: "flex", gap: 0, borderBottom: "1px solid #2a2d38", marginBottom: 24 }}>
            {CATEGORIES.map(cat => (
              <button key={cat} className="tab-btn" onClick={() => { setAdminTab(cat); setShowAddForm(false); setEditingId(null); setForm({ category: cat, question: "", answer: "" }); }} style={{
                background: "transparent", border: "none", borderBottom: adminTab === cat ? "2px solid #d7b26a" : "2px solid transparent",
                color: adminTab === cat ? "#d7b26a" : "#5a6070", padding: "10px 16px", cursor: "pointer",
                fontSize: 13, fontWeight: 500, fontFamily: "inherit", marginBottom: -1, transition: "color 0.2s",
                whiteSpace: "nowrap",
              }}>
                <CategoryIcon cat={cat} /> {cat} <span style={{ fontSize: 11, opacity: 0.6 }}>({kb.filter(e => e.category === cat).length})</span>
              </button>
            ))}
          </div>

          {/* Add button */}
          {!showAddForm && (
            <button onClick={() => { setShowAddForm(true); setEditingId(null); setForm({ category: adminTab, question: "", answer: "" }); }} style={{
              background: "rgba(215,178,106,0.1)", border: "1px dashed rgba(215,178,106,0.4)", color: "#d7b26a",
              padding: "10px 20px", borderRadius: 8, cursor: "pointer", fontSize: 13, fontFamily: "inherit",
              marginBottom: 20, display: "flex", alignItems: "center", gap: 8, fontWeight: 500,
            }}>
              + Add Entry to {adminTab}
            </button>
          )}

          {/* Add/Edit Form */}
          {showAddForm && (
            <div style={{ background: "#1a1d27", border: "1px solid #d7b26a44", borderRadius: 12, padding: 20, marginBottom: 20 }}>
              <div style={{ fontSize: 13, color: "#d7b26a", fontWeight: 600, marginBottom: 14 }}>
                {editingId !== null ? "✏️ Edit Entry" : "➕ New Entry"} — {adminTab}
              </div>
              <div style={{ display: "flex", flexDirection: "column", gap: 12 }}>
                <div>
                  <label style={{ fontSize: 12, color: "#5a6070", display: "block", marginBottom: 5, textTransform: "uppercase", letterSpacing: "0.06em" }}>Question</label>
                  <input value={form.question} onChange={e => setForm(f => ({ ...f, question: e.target.value }))}
                    placeholder="e.g. How do I request a leave of absence?"
                    style={{ width: "100%", background: "#0f1117", border: "1px solid #2a2d38", borderRadius: 8, padding: "10px 14px", color: "#e8e4dc", fontSize: 14, fontFamily: "inherit" }} />
                </div>
                <div>
                  <label style={{ fontSize: 12, color: "#5a6070", display: "block", marginBottom: 5, textTransform: "uppercase", letterSpacing: "0.06em" }}>Answer</label>
                  <textarea value={form.answer} onChange={e => setForm(f => ({ ...f, answer: e.target.value }))}
                    placeholder="Provide a clear, complete answer..."
                    rows={4}
                    style={{ width: "100%", background: "#0f1117", border: "1px solid #2a2d38", borderRadius: 8, padding: "10px 14px", color: "#e8e4dc", fontSize: 14, fontFamily: "inherit", resize: "vertical" }} />
                </div>
                <div style={{ display: "flex", gap: 8 }}>
                  <button onClick={saveEntry} disabled={!form.question.trim() || !form.answer.trim()} style={{
                    background: "#d7b26a", border: "none", color: "#0f1117", padding: "9px 20px",
                    borderRadius: 8, cursor: "pointer", fontSize: 13, fontWeight: 600, fontFamily: "inherit",
                    opacity: !form.question.trim() || !form.answer.trim() ? 0.5 : 1,
                  }}>
                    {editingId !== null ? "Save Changes" : "Add Entry"}
                  </button>
                  <button onClick={cancelForm} style={{
                    background: "transparent", border: "1px solid #2a2d38", color: "#5a6070",
                    padding: "9px 20px", borderRadius: 8, cursor: "pointer", fontSize: 13, fontFamily: "inherit",
                  }}>Cancel</button>
                </div>
              </div>
            </div>
          )}

          {/* Entries list */}
          <div style={{ display: "flex", flexDirection: "column", gap: 10 }}>
            {tabEntries.length === 0 && (
              <div style={{ textAlign: "center", color: "#3a3d48", fontSize: 14, padding: "40px 0" }}>
                No entries yet in this category. Add your first one above.
              </div>
            )}
            {tabEntries.map(entry => (
              <div key={entry.id} className="kb-card" style={{
                background: editingId === entry.id ? "#1e2130" : "#16181f",
                border: editingId === entry.id ? "1px solid #d7b26a44" : "1px solid #2a2d38",
                borderRadius: 10, padding: "16px 18px",
                transition: "background 0.2s, border-color 0.2s",
              }}>
                <div style={{ display: "flex", justifyContent: "space-between", alignItems: "flex-start", gap: 12 }}>
                  <div style={{ flex: 1 }}>
                    <div style={{ fontSize: 14, fontWeight: 600, color: "#d8d4cc", marginBottom: 6 }}>{entry.question}</div>
                    <div style={{ fontSize: 13, color: "#6a7080", lineHeight: 1.6 }}>{entry.answer}</div>
                  </div>
                  <div style={{ display: "flex", gap: 6, flexShrink: 0 }}>
                    <button className="action-btn" onClick={() => startEdit(entry)} style={{
                      background: "#1e2130", border: "1px solid #2a2d38", color: "#8890a0",
                      padding: "5px 12px", borderRadius: 6, cursor: "pointer", fontSize: 12, fontFamily: "inherit", transition: "opacity 0.2s",
                    }}>Edit</button>
                    <button className="action-btn" onClick={() => deleteEntry(entry.id)} style={{
                      background: "transparent", border: "1px solid #3a1a1a", color: "#8a4040",
                      padding: "5px 12px", borderRadius: 6, cursor: "pointer", fontSize: 12, fontFamily: "inherit", transition: "opacity 0.2s",
                    }}>Delete</button>
                  </div>
                </div>
              </div>
            ))}
          </div>
        </div>
      )}
    </div>
  );
}
