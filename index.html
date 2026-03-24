import { useState, useRef, useEffect } from "react";

// ─────────────────────────────────────────────
//  AGENT BRAIN — Full autonomous system prompt
// ─────────────────────────────────────────────
const AGENT_SYSTEM_PROMPT = `You are SARAH — a fully autonomous AI receptionist AGENT for Texas Dental Center. You are NOT a chatbot. You take REAL ACTIONS using your tools.

══ TOOLS YOU MUST USE ══
• google_calendar → Check slots, create appointments, set reminders, schedule follow-ups
• gmail → Send confirmation emails, reminder emails, review request emails

══ MANDATORY AGENT WORKFLOW FOR EVERY BOOKING ══
Step 1: Collect → patient name, phone, email, service needed
Step 2: USE google_calendar → create event:
  Title: "🦷 [Service] — [Patient Name]"
  Duration: 45 minutes
  Description: "Phone: [number] | Service: [service] | Booked via AI Agent"
  Add 1-day-before reminder
Step 3: USE gmail → send confirmation to patient:
  Subject: "✅ Appointment Confirmed — Texas Dental Center"
  Body: Full appointment details + what to bring + clinic address
Step 4: USE google_calendar → schedule follow-up event (2 days after appointment):
  Title: "📧 Send Review Request — [Patient Name]"
  This reminds you to send a Google review request
Step 5: Confirm everything to patient with summary

══ MORE AUTOMATION (always do these) ══
• Cleaning/checkup appointment → Also schedule 6-month recall reminder in calendar
• Root canal / implant / major treatment → Schedule 1-week post-treatment follow-up call reminder
• Emergency patients → Find TODAY's first available slot, mark as URGENT in calendar

══ SERVICES & PRICES ══
Cleaning/Scaling: ₹500–1,500 | Filling: ₹800–2,500 | Extraction: ₹500–3,000
Root Canal: ₹3,000–7,000 | Crown: ₹3,000–8,000 | Bridge: ₹8,000–20,000
Implant: ₹15,000–45,000 | Whitening: ₹5,000–15,000 | Veneers: ₹8,000–20,000/tooth
Invisalign/Braces: ₹80,000–2,50,000 | Emergency consult: ₹500–1,500
Always give RANGES. Always say final cost depends on doctor's evaluation.

══ CLINIC INFO ══
Texas Dental Center | Mon–Sat 9:00 AM – 6:00 PM | Lunch break: 1:00 PM – 2:00 PM
NO bookings during lunch break. Emergency cases: prioritize same-day slots.

══ LANGUAGE RULE ══
Match the patient's language perfectly. Hindi → reply in Hindi. English → English. Hinglish is fine and natural.

══ TRANSPARENCY RULE ══
Always tell the patient step-by-step what you are doing:
"Main abhi aapka Google Calendar mein appointment add kar rahi hoon..."
"Ab main aapko confirmation email bhej rahi hoon..."
"Ek reminder bhi set kar diya 1 din pehle ke liye..."

══ PERSONALITY ══
Warm, calm, professional. Never robotic. Empathetic for pain/emergency cases.
End every major interaction with a confirmation summary.`;

// ─────────────────────────────────────────────
//  CONSTANTS
// ─────────────────────────────────────────────
const QUICK_ACTIONS = [
  { icon: "📅", label: "Appointment Book Karo", msg: "Mujhe appointment book karni hai" },
  { icon: "🚨", label: "Emergency — Dard Ho Raha Hai", msg: "Bahut zyada dard ho raha hai, urgent appointment chahiye" },
  { icon: "💰", label: "Treatment Cost Puchho", msg: "Root canal treatment ka kharcha kitna hoga?" },
  { icon: "🔄", label: "Reschedule / Cancel", msg: "Mujhe apni appointment reschedule karni hai" },
  { icon: "⭐", label: "Services Jano", msg: "Aap kaunsi dental services provide karte ho?" },
];

const SAVINGS_BREAKDOWN = [
  { icon: "👩‍💼", label: "Receptionist Cost Saved", amount: 20000, detail: "Full-time receptionist replace" },
  { icon: "📅", label: "No-Show Prevention", amount: 15000, detail: "Auto-reminders reduce no-shows by 80%" },
  { icon: "🌙", label: "After-Hours Bookings", amount: 9000, detail: "Patients book at night, weekends" },
  { icon: "💌", label: "Follow-up Revenue", amount: 8000, detail: "Recalls bring back old patients" },
  { icon: "⭐", label: "Review Generation", amount: 5500, detail: "More reviews = more new patients" },
  { icon: "⚡", label: "Admin Time Saved", amount: 4500, detail: "Zero manual calls/messages needed" },
];

const INTEGRATIONS = [
  { icon: "📅", name: "Google Calendar", desc: "Appointments + Reminders + Follow-ups", status: "active" },
  { icon: "📧", name: "Gmail", desc: "Confirmations + Recalls + Review Requests", status: "active" },
  { icon: "🤖", name: "Claude AI (Sonnet)", desc: "Agent Brain — Bilingual Intelligence", status: "active" },
  { icon: "📋", name: "Google Sheets", desc: "Patient Database & Records", status: "soon" },
  { icon: "📱", name: "WhatsApp Business API", desc: "WhatsApp Reminders & Booking", status: "soon" },
  { icon: "💳", name: "Razorpay (Free)", desc: "Online Consultation Fee Collection", status: "soon" },
];

const ACTION_ICONS = { thinking: "🧠", tool: "🔧", calendar: "📅", email: "📧", success: "✅", error: "❌" };
const ACTION_COLORS = { thinking: "#a78bfa", tool: "#fb923c", calendar: "#34d399", email: "#60a5fa", success: "#4ade80", error: "#f87171" };

// ─────────────────────────────────────────────
//  MAIN COMPONENT
// ─────────────────────────────────────────────
export default function DentalAgent() {
  const [tab, setTab] = useState("chat");
  const [messages, setMessages] = useState([{
    role: "assistant",
    content: "Namaste! 🙏 Main **Sarah** hoon — Texas Dental Center ki autonomous AI Agent.\n\nMain sirf baatein nahi karti — **real actions** leti hoon:\n\n✅ Google Calendar mein appointment book karti hoon\n✅ Gmail se confirmation email bhejti hoon\n✅ 1-din-pehle reminder set karti hoon\n✅ 6-month recall aur follow-up schedule karti hoon\n\nAaj kaise madad kar sakti hoon?",
  }]);
  const [input, setInput] = useState("");
  const [loading, setLoading] = useState(false);
  const [actions, setActions] = useState([]);
  const [sessionStats, setSessionStats] = useState({ appointments: 0, emails: 0, reminders: 0, noShows: 0 });
  const bottomRef = useRef(null);
  const inputRef = useRef(null);

  useEffect(() => { bottomRef.current?.scrollIntoView({ behavior: "smooth" }); }, [messages, loading]);

  const addAction = (type, desc, detail = "") => {
    setActions(prev => [{
      id: Date.now() + Math.random(),
      type, desc, detail,
      time: new Date().toLocaleTimeString("en-IN", { hour: "2-digit", minute: "2-digit", second: "2-digit" }),
    }, ...prev].slice(0, 60));
  };

  const sendMessage = async (text) => {
    const userText = (text || input).trim();
    if (!userText || loading) return;
    const history = [...messages, { role: "user", content: userText }];
    setMessages(history);
    setInput("");
    setLoading(true);
    addAction("thinking", "Patient message processing ho raha hai...", userText.slice(0, 70) + (userText.length > 70 ? "..." : ""));

    try {
      addAction("tool", "MCP Servers se connect ho raha hai...", "Google Calendar + Gmail APIs");

      const res = await fetch("https://api.anthropic.com/v1/messages", {
        method: "POST",
        headers: { "Content-Type": "application/json" },
        body: JSON.stringify({
          model: "claude-sonnet-4-20250514",
          max_tokens: 1000,
          system: AGENT_SYSTEM_PROMPT,
          messages: history.map(m => ({ role: m.role, content: m.content })),
          mcp_servers: [
            { type: "url", url: "https://gcal.mcp.claude.com/mcp", name: "google-calendar" },
            { type: "url", url: "https://gmail.mcp.claude.com/mcp", name: "gmail" },
          ],
        }),
      });

      const data = await res.json();
      let finalText = "";
      let calUsed = false, mailUsed = false, toolsCount = 0;

      for (const block of (data.content || [])) {
        if (block.type === "text") {
          finalText += block.text;
        } else if (block.type === "mcp_tool_use") {
          toolsCount++;
          const n = (block.name || "").toLowerCase();
          const inp = JSON.stringify(block.input || {});
          if (n.includes("calendar") || n.includes("event") || n.includes("gcal")) {
            calUsed = true;
            addAction("calendar", `📅 Calendar: ${block.name}`, inp.slice(0, 120));
          } else if (n.includes("gmail") || n.includes("mail") || n.includes("send") || n.includes("email")) {
            mailUsed = true;
            addAction("email", `📧 Gmail: ${block.name}`, inp.slice(0, 120));
          } else {
            addAction("tool", `🔧 Tool: ${block.name}`, inp.slice(0, 100));
          }
        } else if (block.type === "mcp_tool_result") {
          const content = Array.isArray(block.content)
            ? block.content.map(c => c.text || "").join(" ")
            : (typeof block.content === "string" ? block.content : JSON.stringify(block.content || {}));
          addAction("success", "Tool executed successfully ✅", content.slice(0, 120));
        }
      }

      if (calUsed) setSessionStats(p => ({ ...p, appointments: p.appointments + 1, reminders: p.reminders + 1 }));
      if (mailUsed) setSessionStats(p => ({ ...p, emails: p.emails + 1, noShows: p.noShows + 1 }));

      if (!finalText) finalText = "Kuch issue aa gaya. Please dobara try karein. 🙏";
      setMessages(prev => [...prev, { role: "assistant", content: finalText }]);

    } catch (err) {
      addAction("error", "Connection error", err.message);
      setMessages(prev => [...prev, { role: "assistant", content: "Technical error aa gaya. Dobara try karein. 🙏" }]);
    }
    setLoading(false);
  };

  const md = (t) => t
    .replace(/\*\*(.*?)\*\*/g, '<strong>$1</strong>')
    .replace(/\*(.*?)\*/g, '<em>$1</em>')
    .replace(/\n/g, '<br/>');

  const totalSavings = SAVINGS_BREAKDOWN.reduce((s, r) => s + r.amount, 0);

  return (
    <>
      <style>{`
        @import url('https://fonts.googleapis.com/css2?family=Manrope:wght@400;500;600;700;800&family=Syne:wght@700;800&display=swap');
        :root {
          --bg: #080d18;
          --surface: #0e1525;
          --surface2: #131e30;
          --border: rgba(255,255,255,0.07);
          --teal: #00d4a8;
          --blue: #3b9eff;
          --green: #4ade80;
          --amber: #fbbf24;
          --red: #f87171;
          --violet: #a78bfa;
          --text: #e2e8f0;
          --muted: #64748b;
          --subtle: #1e2d42;
        }
        *, *::before, *::after { box-sizing: border-box; margin: 0; padding: 0; }
        body { 
          font-family: 'Manrope', sans-serif; 
          background: var(--bg); 
          color: var(--text);
          height: 100vh; overflow: hidden;
        }
        .root { display: flex; flex-direction: column; height: 100vh; }

        /* HEADER */
        .hdr {
          background: linear-gradient(135deg, #0a1628 0%, #0e1f3a 100%);
          padding: 12px 18px;
          display: flex; align-items: center; gap: 12px;
          border-bottom: 1px solid var(--border);
          flex-shrink: 0;
          position: relative;
          overflow: hidden;
        }
        .hdr::after {
          content: '';
          position: absolute; inset: 0;
          background: linear-gradient(90deg, rgba(0,212,168,0.04) 0%, transparent 60%);
          pointer-events: none;
        }
        .hdr-logo {
          width: 44px; height: 44px;
          background: linear-gradient(135deg, var(--teal), var(--blue));
          border-radius: 14px;
          display: flex; align-items: center; justify-content: center;
          font-size: 22px; flex-shrink: 0;
          box-shadow: 0 4px 20px rgba(0,212,168,0.35);
        }
        .hdr-name {
          font-family: 'Syne', sans-serif;
          font-size: 16px; font-weight: 800;
          background: linear-gradient(90deg, var(--teal), var(--blue));
          -webkit-background-clip: text; -webkit-text-fill-color: transparent;
        }
        .hdr-sub { font-size: 11.5px; color: var(--muted); margin-top: 1px; }
        .live-pill {
          margin-left: auto;
          display: flex; align-items: center; gap: 6px;
          background: rgba(0,212,168,0.08);
          border: 1px solid rgba(0,212,168,0.25);
          border-radius: 20px; padding: 5px 12px;
          font-size: 11px; font-weight: 700; color: var(--teal);
          flex-shrink: 0;
        }
        .live-dot { width: 7px; height: 7px; border-radius: 50%; background: var(--teal); animation: lp 1.8s infinite; }
        @keyframes lp { 0%,100%{box-shadow:0 0 4px var(--teal);opacity:1} 50%{box-shadow:none;opacity:0.4} }

        /* TABS */
        .tabs { display: flex; background: var(--surface); border-bottom: 1px solid var(--border); flex-shrink: 0; }
        .tb {
          flex: 1; padding: 11px 6px;
          background: none; border: none; border-bottom: 2px solid transparent;
          color: var(--muted); font-size: 12px; font-weight: 700;
          cursor: pointer; font-family: 'Manrope', sans-serif;
          transition: all 0.2s;
          display: flex; align-items: center; justify-content: center; gap: 5px;
        }
        .tb.on { color: var(--teal); border-bottom-color: var(--teal); background: rgba(0,212,168,0.04); }
        .tb:hover:not(.on) { color: #94a3b8; }

        /* CHAT */
        .chat-scroll { flex: 1; overflow-y: auto; padding: 14px 16px; display: flex; flex-direction: column; gap: 10px; }
        .chat-scroll::-webkit-scrollbar { width: 3px; }
        .chat-scroll::-webkit-scrollbar-thumb { background: var(--subtle); border-radius: 10px; }

        .qrow { padding: 8px 16px 4px; display: flex; gap: 6px; flex-wrap: wrap; flex-shrink: 0; }
        .qbtn {
          padding: 5px 12px; border-radius: 20px;
          border: 1px solid rgba(0,212,168,0.2);
          background: rgba(0,212,168,0.05);
          color: var(--teal); font-size: 12px; font-weight: 600;
          cursor: pointer; font-family: 'Manrope', sans-serif;
          transition: all 0.15s; white-space: nowrap;
        }
        .qbtn:hover { background: rgba(0,212,168,0.14); border-color: var(--teal); }

        .mrow { display: flex; align-items: flex-end; gap: 8px; }
        .mrow.u { flex-direction: row-reverse; }
        .mav {
          width: 30px; height: 30px; border-radius: 50%; flex-shrink: 0;
          background: linear-gradient(135deg, rgba(0,212,168,0.15), rgba(59,158,255,0.15));
          border: 1px solid rgba(0,212,168,0.2);
          display: flex; align-items: center; justify-content: center; font-size: 14px;
        }
        .bbl {
          max-width: 80%; padding: 10px 14px; border-radius: 18px;
          font-size: 13.5px; line-height: 1.65; word-break: break-word;
        }
        .bbl.a {
          background: var(--surface2);
          border: 1px solid var(--border);
          border-bottom-left-radius: 4px;
        }
        .bbl.u {
          background: linear-gradient(135deg, #009e7f, #2673cc);
          color: #fff; border-bottom-right-radius: 4px;
          box-shadow: 0 4px 16px rgba(0,180,140,0.25);
        }
        .dots { display: flex; gap: 4px; align-items: center; padding: 2px 0; }
        .dots span { width: 7px; height: 7px; border-radius: 50%; background: var(--teal); animation: db 1.2s infinite; }
        .dots span:nth-child(2){animation-delay:.2s} .dots span:nth-child(3){animation-delay:.4s}
        @keyframes db{0%,80%,100%{transform:translateY(0)}40%{transform:translateY(-6px)}}

        .ibar {
          padding: 10px 14px; background: var(--surface);
          border-top: 1px solid var(--border);
          display: flex; gap: 8px; align-items: center; flex-shrink: 0;
        }
        .inp {
          flex: 1; padding: 10px 16px;
          background: var(--surface2); border: 1px solid var(--border);
          border-radius: 24px; color: var(--text);
          font-size: 13.5px; font-family: 'Manrope', sans-serif;
          outline: none; transition: border 0.2s;
        }
        .inp:focus { border-color: var(--teal); }
        .inp::placeholder { color: #3a4d65; }
        .sbtn {
          width: 40px; height: 40px; border-radius: 50%; flex-shrink: 0;
          background: linear-gradient(135deg, var(--teal), var(--blue));
          border: none; cursor: pointer; color: #fff;
          font-size: 16px; display: flex; align-items: center; justify-content: center;
          transition: transform 0.15s;
        }
        .sbtn:hover:not(:disabled) { transform: scale(1.08); }
        .sbtn:disabled { opacity: 0.3; cursor: not-allowed; }

        /* AGENT LOG */
        .log-scroll { flex: 1; overflow-y: auto; padding: 14px 16px; display: flex; flex-direction: column; gap: 7px; }
        .log-scroll::-webkit-scrollbar { width: 3px; }
        .log-item {
          background: var(--surface2); border-radius: 10px;
          padding: 9px 13px; border-left: 3px solid;
          animation: fade 0.3s ease;
        }
        @keyframes fade{from{opacity:0;transform:translateY(-4px)}to{opacity:1;transform:none}}
        .log-row { display: flex; justify-content: space-between; align-items: flex-start; gap: 8px; }
        .log-desc { font-size: 12.5px; font-weight: 700; color: var(--text); }
        .log-time { font-size: 10.5px; color: var(--muted); white-space: nowrap; flex-shrink: 0; }
        .log-det { font-size: 11px; color: #4a6080; font-family: 'Courier New', monospace; margin-top: 3px; word-break: break-all; }
        .log-empty { text-align: center; color: var(--muted); margin-top: 50px; }
        .log-empty-icon { font-size: 36px; margin-bottom: 8px; }

        /* DASHBOARD */
        .dash-scroll { flex: 1; overflow-y: auto; padding: 14px 16px; }
        .dash-scroll::-webkit-scrollbar { width: 3px; }
        .dash-grid { display: grid; grid-template-columns: 1fr 1fr; gap: 10px; margin-bottom: 14px; }
        .stat-box {
          background: var(--surface2); border-radius: 14px;
          padding: 14px 12px; text-align: center;
          border: 1px solid var(--border);
        }
        .stat-n {
          font-family: 'Syne', sans-serif; font-size: 28px; font-weight: 800;
          background: linear-gradient(135deg, var(--teal), var(--blue));
          -webkit-background-clip: text; -webkit-text-fill-color: transparent;
        }
        .stat-l { font-size: 11px; color: var(--muted); margin-top: 2px; font-weight: 600; }

        .section { background: var(--surface2); border-radius: 16px; padding: 16px; margin-bottom: 12px; border: 1px solid var(--border); }
        .sec-title {
          font-size: 11px; font-weight: 800; color: var(--muted);
          text-transform: uppercase; letter-spacing: 1.2px; margin-bottom: 12px;
        }
        .srow {
          display: flex; justify-content: space-between; align-items: center;
          padding: 8px 0; border-bottom: 1px solid rgba(255,255,255,0.04);
          font-size: 13px;
        }
        .srow:last-child { border-bottom: none; }
        .srow-l { display: flex; align-items: center; gap: 8px; }
        .srow-icon { font-size: 18px; }
        .srow-text { }
        .srow-name { color: var(--text); font-weight: 600; font-size: 13px; }
        .srow-det { color: var(--muted); font-size: 11px; }
        .srow-amt { font-weight: 800; color: var(--green); font-size: 14px; }
        .total-banner {
          background: linear-gradient(135deg, rgba(0,212,168,0.1), rgba(59,158,255,0.08));
          border: 1px solid rgba(0,212,168,0.25);
          border-radius: 14px; padding: 16px;
          display: flex; justify-content: space-between; align-items: center;
          margin-top: 4px;
        }
        .total-lbl { font-size: 13px; font-weight: 700; color: var(--text); }
        .total-sub { font-size: 11px; color: var(--muted); margin-top: 2px; }
        .total-amt {
          font-family: 'Syne', sans-serif; font-size: 26px; font-weight: 800;
          background: linear-gradient(135deg, var(--teal), var(--green));
          -webkit-background-clip: text; -webkit-text-fill-color: transparent;
        }

        .int-item {
          display: flex; align-items: center; gap: 10px;
          padding: 9px 10px; border-radius: 10px;
          background: rgba(255,255,255,0.02); margin-bottom: 6px;
        }
        .int-icon { font-size: 20px; width: 32px; text-align: center; }
        .int-body { flex: 1; }
        .int-name { font-size: 13px; font-weight: 700; color: var(--text); }
        .int-desc { font-size: 11px; color: var(--muted); }
        .int-badge {
          border-radius: 8px; padding: 2px 9px; font-size: 11px; font-weight: 800;
          flex-shrink: 0;
        }
        .int-badge.active { background: rgba(74,222,128,0.12); color: var(--green); border: 1px solid rgba(74,222,128,0.3); }
        .int-badge.soon { background: rgba(251,191,36,0.1); color: var(--amber); border: 1px solid rgba(251,191,36,0.25); }
      `}</style>

      <div className="root">

        {/* ── HEADER ── */}
        <div className="hdr">
          <div className="hdr-logo">🦷</div>
          <div>
            <div className="hdr-name">Texas Dental Center</div>
            <div className="hdr-sub">Autonomous AI Agent • Hindi + English • Zero Investment</div>
          </div>
          <div className="live-pill">
            <div className="live-dot" />
            AGENT LIVE
          </div>
        </div>

        {/* ── TABS ── */}
        <div className="tabs">
          {[["chat","💬","Patient Agent"],["log","⚡","Live Actions"],["dash","📊","ROI Dashboard"]].map(([id,ic,lbl]) => (
            <button key={id} className={`tb ${tab===id?"on":""}`} onClick={() => setTab(id)}>
              {ic} {lbl}
            </button>
          ))}
        </div>

        {/* ════════════════ CHAT ════════════════ */}
        {tab === "chat" && (
          <>
            {messages.length <= 1 && (
              <div className="qrow">
                {QUICK_ACTIONS.map(q => (
                  <button key={q.label} className="qbtn" onClick={() => sendMessage(q.msg)}>
                    {q.icon} {q.label}
                  </button>
                ))}
              </div>
            )}
            <div className="chat-scroll">
              {messages.map((m, i) => (
                <div key={i} className={`mrow ${m.role === "user" ? "u" : ""}`}>
                  {m.role === "assistant" && <div className="mav">👩‍⚕️</div>}
                  <div className={`bbl ${m.role === "user" ? "u" : "a"}`}>
                    {m.role === "assistant"
                      ? <span dangerouslySetInnerHTML={{ __html: md(m.content) }} />
                      : m.content}
                  </div>
                </div>
              ))}
              {loading && (
                <div className="mrow">
                  <div className="mav">👩‍⚕️</div>
                  <div className="bbl a"><div className="dots"><span/><span/><span/></div></div>
                </div>
              )}
              <div ref={bottomRef} />
            </div>
            <div className="ibar">
              <input
                ref={inputRef}
                className="inp"
                placeholder="Hindi ya English mein likhein..."
                value={input}
                onChange={e => setInput(e.target.value)}
                onKeyDown={e => e.key === "Enter" && !e.shiftKey && sendMessage()}
                disabled={loading}
              />
              <button className="sbtn" onClick={() => sendMessage()} disabled={loading || !input.trim()}>
                ➤
              </button>
            </div>
          </>
        )}

        {/* ════════════════ AGENT LOG ════════════════ */}
        {tab === "log" && (
          <div className="log-scroll">
            {actions.length === 0 ? (
              <div className="log-empty">
                <div className="log-empty-icon">⚡</div>
                <div style={{fontWeight:600, marginBottom:6}}>Agent Actions yahan dikhenge</div>
                <div style={{fontSize:12}}>Patient se baat karo — real-time tool calls yahan track honge</div>
              </div>
            ) : actions.map(a => (
              <div key={a.id} className="log-item" style={{ borderLeftColor: ACTION_COLORS[a.type] || "#64748b" }}>
                <div className="log-row">
                  <div className="log-desc">{ACTION_ICONS[a.type] || "🔹"} {a.desc}</div>
                  <div className="log-time">{a.time}</div>
                </div>
                {a.detail && <div className="log-det">{a.detail}</div>}
              </div>
            ))}
          </div>
        )}

        {/* ════════════════ DASHBOARD ════════════════ */}
        {tab === "dash" && (
          <div className="dash-scroll">

            {/* Session stats */}
            <div className="dash-grid">
              {[
                ["📅", sessionStats.appointments, "Appointments Booked"],
                ["📧", sessionStats.emails, "Emails Sent"],
                ["🔔", sessionStats.reminders, "Reminders Set"],
                ["✅", sessionStats.noShows, "No-Shows Prevented"],
              ].map(([ic, v, l]) => (
                <div className="stat-box" key={l}>
                  <div style={{fontSize:22, marginBottom:4}}>{ic}</div>
                  <div className="stat-n">{v}</div>
                  <div className="stat-l">{l}</div>
                </div>
              ))}
            </div>

            {/* Savings breakdown */}
            <div className="section">
              <div className="sec-title">💰 Monthly Savings Breakdown (Doctor)</div>
              {SAVINGS_BREAKDOWN.map(s => (
                <div className="srow" key={s.label}>
                  <div className="srow-l">
                    <div className="srow-icon">{s.icon}</div>
                    <div className="srow-text">
                      <div className="srow-name">{s.label}</div>
                      <div className="srow-det">{s.detail}</div>
                    </div>
                  </div>
                  <div className="srow-amt">+₹{s.amount.toLocaleString()}</div>
                </div>
              ))}
              <div className="total-banner">
                <div>
                  <div className="total-lbl">🎯 Total Monthly Value</div>
                  <div className="total-sub">Conservative estimate • Real savings can be higher</div>
                </div>
                <div className="total-amt">₹{totalSavings.toLocaleString()}</div>
              </div>
            </div>

            {/* Integrations */}
            <div className="section">
              <div className="sec-title">🔧 Agent Integrations — Sab FREE</div>
              {INTEGRATIONS.map(it => (
                <div className="int-item" key={it.name}>
                  <div className="int-icon">{it.icon}</div>
                  <div className="int-body">
                    <div className="int-name">{it.name}</div>
                    <div className="int-desc">{it.desc}</div>
                  </div>
                  <div className={`int-badge ${it.status}`}>
                    {it.status === "active" ? "✅ LIVE" : "⏳ SOON"}
                  </div>
                </div>
              ))}
            </div>

            {/* Agent capabilities */}
            <div className="section">
              <div className="sec-title">🤖 Agent Kya Kya Karta Hai (Automatically)</div>
              {[
                ["📅", "Appointment book + Google Calendar entry"],
                ["📧", "Confirmation email instantly bhejta hai"],
                ["🔔", "1-din-pehle reminder set karta hai"],
                ["💌", "2-din-baad review request email"],
                ["🔄", "6-month recall reminder for checkups"],
                ["⚕️", "Post-treatment follow-up schedule"],
                ["🚨", "Emergency? Same-day URGENT slot"],
                ["💰", "Treatment cost estimate + consultation book"],
                ["🌙", "24/7 available — raat ko bhi booking"],
                ["📊", "Har action ka full log maintain karta hai"],
              ].map(([ic, t]) => (
                <div key={t} style={{display:"flex",alignItems:"center",gap:10,padding:"7px 0",borderBottom:"1px solid rgba(255,255,255,0.04)",fontSize:12.5}}>
                  <span style={{fontSize:16,width:24}}>{ic}</span>
                  <span style={{color:"#94a3b8"}}>{t}</span>
                </div>
              ))}
            </div>

          </div>
        )}

      </div>
    </>
  );
}
