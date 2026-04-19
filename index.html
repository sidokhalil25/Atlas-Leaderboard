import { useState, useEffect } from "react";

const ADMIN_PIN = "13122";
const CATS = [
  { key:"kip",    label:"KIP" },
  { key:"digi",   label:"Digi" },
  { key:"net",    label:"Net" },
  { key:"mobile", label:"Mobile" },
  { key:"upsell", label:"Upsell" },
];

function hashPin(p) {
  let h = 0;
  for (let i = 0; i < p.length; i++) h = (Math.imul(31,h) + p.charCodeAt(i)) | 0;
  return h.toString();
}

function crColor(cr) {
  if (cr >= 20) return { bg:"#002a12", fg:"#00A651" };
  if (cr >= 10) return { bg:"#1a1000", fg:"#f5a623" };
  return { bg:"#1a0000", fg:"#E8002D" };
}

export default function App() {
  const [members, setMembers]     = useState([]);
  const [view, setView]           = useState("board");
  const [period, setPeriod]       = useState("week");
  const [currentUser, setCurrentUser] = useState(null);
  const [loginName, setLoginName] = useState("");
  const [loginPin, setLoginPin]   = useState("");
  const [loginErr, setLoginErr]   = useState("");
  const [entry, setEntry]         = useState({ kip:"", digi:"", net:"", mobile:"", upsell:"", gespräche:"", kunden:"" });
  const [entryMsg, setEntryMsg]   = useState("");
  const [adminPin, setAdminPin]   = useState("");
  const [adminErr, setAdminErr]   = useState("");
  const [adminOk, setAdminOk]     = useState(false);
  const [newName, setNewName]     = useState("");
  const [newPin, setNewPin]       = useState("");
  const [addMsg, setAddMsg]       = useState("");
  const [bulkText, setBulkText]   = useState("");
  const [bulkPin, setBulkPin]     = useState("");
  const [bulkMsg, setBulkMsg]     = useState("");
  const [loading, setLoading]     = useState(true);

  useEffect(() => { init(); }, []);

  async function init() {
    setLoading(true);
    try {
      const r = await window.storage.get("atlas_v4");
      setMembers(r ? JSON.parse(r.value) : []);
    } catch(e) { setMembers([]); }
    setLoading(false);
  }

  async function save(m) {
    setMembers([...m]);
    await window.storage.set("atlas_v4", JSON.stringify(m));
  }

  function getStats(member) {
    const now = new Date();
    const filtered = (member.entries||[]).filter(e => {
      const d = new Date(e.date);
      if (period === "week") {
        const mon = new Date(now);
        mon.setDate(now.getDate() - ((now.getDay()+6)%7));
        mon.setHours(0,0,0,0);
        return d >= mon;
      }
      if (period === "month") return d.getMonth()===now.getMonth() && d.getFullYear()===now.getFullYear();
      return true;
    });
    const s = { gespräche:0, kunden:0 };
    CATS.forEach(c => s[c.key] = 0);
    filtered.forEach(e => {
      s.gespräche += e.gespräche||0;
      s.kunden    += e.kunden||0;
      CATS.forEach(c => s[c.key] += e[c.key]||0);
    });
    s.total = CATS.reduce((sum,c) => sum + s[c.key], 0);
    s.cr    = s.gespräche > 0 ? (s.kunden / s.gespräche * 100) : null;
    return s;
  }

  const ranked = [...members].sort((a,b) => getStats(b).total - getStats(a).total);

  function doLogin() {
    const m = members.find(m => m.name.toLowerCase() === loginName.trim().toLowerCase());
    if (!m)                              { setLoginErr("Name nicht gefunden."); return; }
    if (m.pinHash !== hashPin(loginPin)) { setLoginErr("Falsche PIN."); return; }
    setCurrentUser(m.name); setLoginErr(""); setLoginPin(""); setView("entry");
  }

  async function doEntry() {
    const vals = {};
    CATS.forEach(c => vals[c.key] = parseInt(entry[c.key])||0);
    vals.gespräche = parseInt(entry.gespräche)||0;
    vals.kunden    = parseInt(entry.kunden)||0;
    const total = CATS.reduce((s,c)=>s+vals[c.key],0);
    if (!total && !vals.gespräche && !vals.kunden) { setEntryMsg("Mindestens einen Wert eintragen."); return; }
    const updated = members.map(m =>
      m.name !== currentUser ? m : { ...m, entries:[...(m.entries||[]), { date:new Date().toISOString(), ...vals }] }
    );
    await save(updated);
    setEntryMsg(`Eingetragen: ${total} Verträge · ${vals.gespräche} Gespräche · ${vals.kunden} Kunden`);
    setEntry({ kip:"", digi:"", net:"", mobile:"", upsell:"", gespräche:"", kunden:"" });
    setTimeout(() => { setEntryMsg(""); setView("board"); }, 2000);
  }

  async function doAdd() {
    if (!newName.trim() || newPin.length < 4) { setAddMsg("Name + mind. 4-stellige PIN."); return; }
    if (members.find(m => m.name.toLowerCase()===newName.trim().toLowerCase())) { setAddMsg("Name bereits vorhanden."); return; }
    const updated = [...members, { name:newName.trim(), pinHash:hashPin(newPin), entries:[] }];
    await save(updated);
    setNewName(""); setNewPin("");
    setAddMsg(`${newName.trim()} hinzugefügt!`);
    setTimeout(()=>setAddMsg(""),2000);
  }

  async function doBulk() {
    if (bulkPin.length < 4) { setBulkMsg("Mind. 4-stellige Standard-PIN eingeben."); return; }
    const names = bulkText.split("\n").map(n=>n.trim()).filter(n=>n.length>0);
    if (!names.length) { setBulkMsg("Keine Namen gefunden."); return; }
    const existing = members.map(m=>m.name.toLowerCase());
    const toAdd = names.filter(n=>!existing.includes(n.toLowerCase()))
      .map(n=>({ name:n, pinHash:hashPin(bulkPin), entries:[] }));
    if (!toAdd.length) { setBulkMsg("Alle Namen bereits vorhanden."); return; }
    await save([...members, ...toAdd]);
    setBulkText(""); setBulkMsg(`${toAdd.length} Mitglieder hinzugefügt!`);
    setTimeout(()=>setBulkMsg(""),3000);
  }

  async function doDelete(name) { await save(members.filter(m=>m.name!==name)); }

  const inp     = { background:"#0d0d0d", border:"1px solid #262626", borderRadius:6, padding:"9px 12px", color:"#fff", fontSize:".88rem", width:"100%", fontFamily:"inherit", outline:"none", marginBottom:8, boxSizing:"border-box" };
  const lbl     = { color:"#555", fontSize:".7rem", letterSpacing:".06em", textTransform:"uppercase", display:"block", marginBottom:3, fontWeight:600 };
  const redBtn  = { background:"#E8002D", border:"none", borderRadius:6, padding:"8px 18px", color:"#fff", fontSize:".82rem", fontWeight:700, cursor:"pointer", fontFamily:"inherit" };
  const grayBtn = { background:"transparent", border:"1px solid #262626", borderRadius:6, padding:"8px 14px", color:"#555", fontSize:".82rem", cursor:"pointer", fontFamily:"inherit" };
  const th      = { padding:"9px 10px", textAlign:"center", color:"#444", fontWeight:600, fontSize:".7rem", textTransform:"uppercase", letterSpacing:".05em", whiteSpace:"nowrap", borderBottom:"1px solid #1e1e1e" };
  const td      = { padding:"10px 10px", textAlign:"center", fontSize:".82rem", borderBottom:"1px solid #161616" };

  if (loading) return (
    <div style={{ fontFamily:"Inter,sans-serif", background:"#0a0a0a", minHeight:"100vh", display:"flex", alignItems:"center", justifyContent:"center", color:"#333" }}>Laden…</div>
  );

  return (
    <div style={{ fontFamily:"Inter,sans-serif", background:"#0a0a0a", minHeight:"100vh", color:"#fff", paddingBottom:40 }}>

      {/* NAV */}
      <div style={{ display:"flex", alignItems:"center", justifyContent:"space-between", padding:"13px 16px", borderBottom:"1px solid #1a1a1a", flexWrap:"wrap", gap:8 }}>
        <div style={{ fontWeight:800, fontSize:"1rem", display:"flex", alignItems:"center", gap:8 }}>
          <span style={{ background:"#E8002D", color:"#fff", fontSize:".65rem", fontWeight:800, padding:"2px 8px", borderRadius:3, letterSpacing:".06em" }}>ATLAS</span>
          Leaderboard
        </div>
        <div style={{ display:"flex", gap:8 }}>
          {currentUser
            ? <button style={grayBtn} onClick={()=>{ setCurrentUser(null); setView("board"); }}>Abmelden</button>
            : <button style={redBtn}  onClick={()=>setView("login")}>+ Eintragen</button>
          }
          <button style={grayBtn} onClick={()=>setView("admin")}>Admin</button>
        </div>
      </div>

      {/* BOARD */}
      {view==="board" && <>
        <div style={{ display:"flex", gap:8, padding:"14px 16px 0" }}>
          {[["week","Woche"],["month","Monat"],["alltime","Gesamt"]].map(([k,l]) => (
            <button key={k} onClick={()=>setPeriod(k)} style={{
              background:period===k?"#E8002D":"transparent",
              border:period===k?"none":"1px solid #262626",
              borderRadius:5, padding:"5px 13px",
              color:period===k?"#fff":"#555",
              fontSize:".75rem", cursor:"pointer", fontFamily:"inherit", fontWeight:period===k?700:400
            }}>{l}</button>
          ))}
        </div>

        <div style={{ margin:"12px 16px 0", overflowX:"auto", borderRadius:10, border:"1px solid #1e1e1e" }}>
          <table style={{ width:"100%", borderCollapse:"collapse", background:"#111", minWidth:560 }}>
            <thead>
              <tr>
                <th style={{...th, textAlign:"left", paddingLeft:14}}>#</th>
                <th style={{...th, textAlign:"left"}}>Name</th>
                {CATS.map(c => <th key={c.key} style={th}>{c.label}</th>)}
                <th style={th}>Gespräche</th>
                <th style={th}>Kunden</th>
                <th style={{...th, color:"#888"}}>CR %</th>
              </tr>
            </thead>
            <tbody>
              {members.length===0 && (
                <tr><td colSpan={9} style={{...td, color:"#333", padding:24, textAlign:"center"}}>
                  Noch keine Mitglieder — Admin → Mitglieder hinzufügen
                </td></tr>
              )}
              {ranked.map((m,i) => {
                const s = getStats(m);
                const cc = s.cr!==null ? crColor(s.cr) : null;
                return (
                  <tr key={m.name} style={{ background:i===0&&s.total>0?"#150505":"transparent" }}>
                    <td style={{...td, textAlign:"left", paddingLeft:14, color:"#444", fontWeight:700, fontSize:".75rem"}}>{i+1}</td>
                    <td style={{...td, textAlign:"left", fontWeight:700, color:"#ddd", whiteSpace:"nowrap"}}>{m.name}</td>
                    {CATS.map(c => (
                      <td key={c.key} style={{...td, color:s[c.key]>0?"#fff":"#2a2a2a", fontWeight:s[c.key]>0?600:400}}>
                        {s[c.key]>0?s[c.key]:"–"}
                      </td>
                    ))}
                    <td style={{...td, color:"#555"}}>{s.gespräche>0?s.gespräche:"–"}</td>
                    <td style={{...td, color:"#555"}}>{s.kunden>0?s.kunden:"–"}</td>
                    <td style={td}>
                      {cc
                        ? <span style={{ background:cc.bg, color:cc.fg, borderRadius:4, padding:"2px 7px", fontSize:".73rem", fontWeight:700 }}>{s.cr.toFixed(1)}%</span>
                        : <span style={{ color:"#2a2a2a" }}>–</span>
                      }
                    </td>
                  </tr>
                );
              })}
            </tbody>
          </table>
        </div>
        <div style={{ textAlign:"center", color:"#252525", fontSize:".68rem", padding:"12px 0" }}>
          {period==="week"?"Diese Woche":period==="month"?"Dieser Monat":"Gesamt"} · {new Date().toLocaleDateString("de-DE")} · {members.length} Mitglieder
        </div>
      </>}

      {/* LOGIN */}
      {view==="login" && (
        <div style={{ background:"#111", border:"1px solid #1e1e1e", borderRadius:10, padding:20, margin:16 }}>
          <div style={{ fontWeight:800, fontSize:"1rem", marginBottom:14 }}>Einloggen</div>
          <label style={lbl}>Name</label>
          <input style={inp} placeholder="Dein Name" value={loginName} onChange={e=>setLoginName(e.target.value)} />
          <label style={lbl}>PIN</label>
          <input style={inp} type="password" placeholder="••••" value={loginPin} onChange={e=>setLoginPin(e.target.value)} onKeyDown={e=>e.key==="Enter"&&doLogin()} />
          {loginErr && <div style={{ color:"#E8002D", fontSize:".8rem", marginBottom:8 }}>{loginErr}</div>}
          <div style={{ display:"flex", gap:8 }}>
            <button style={redBtn} onClick={doLogin}>Weiter</button>
            <button style={grayBtn} onClick={()=>{ setView("board"); setLoginErr(""); }}>Zurück</button>
          </div>
        </div>
      )}

      {/* ENTRY */}
      {view==="entry" && (
        <div style={{ background:"#111", border:"1px solid #1e1e1e", borderRadius:10, padding:20, margin:16 }}>
          <div style={{ fontWeight:800, fontSize:"1rem", marginBottom:4 }}>Hey {currentUser}</div>
          <div style={{ color:"#444", fontSize:".82rem", marginBottom:14 }}>Heute eintragen:</div>
          <div style={{ display:"grid", gridTemplateColumns:"1fr 1fr", gap:"0 12px" }}>
            {CATS.map(c => (
              <div key={c.key}>
                <label style={lbl}>{c.label}</label>
                <input style={inp} type="number" min="0" placeholder="0" value={entry[c.key]} onChange={e=>setEntry({...entry,[c.key]:e.target.value})} />
              </div>
            ))}
          </div>
          <div style={{ display:"grid", gridTemplateColumns:"1fr 1fr", gap:"0 12px" }}>
            <div>
              <label style={lbl}>Gespräche</label>
              <input style={inp} type="number" min="0" placeholder="0" value={entry.gespräche} onChange={e=>setEntry({...entry,gespräche:e.target.value})} />
            </div>
            <div>
              <label style={lbl}>Geschr. Kunden</label>
              <input style={inp} type="number" min="0" placeholder="0" value={entry.kunden} onChange={e=>setEntry({...entry,kunden:e.target.value})} />
            </div>
          </div>
          {entryMsg && <div style={{ color:"#00A651", fontSize:".8rem", marginBottom:8 }}>{entryMsg}</div>}
          <div style={{ display:"flex", gap:8 }}>
            <button style={redBtn} onClick={doEntry}>Eintragen</button>
            <button style={grayBtn} onClick={()=>setView("board")}>Abbrechen</button>
          </div>
        </div>
      )}

      {/* ADMIN */}
      {view==="admin" && (
        <div style={{ background:"#111", border:"1px solid #1e1e1e", borderRadius:10, padding:20, margin:16 }}>
          <div style={{ fontWeight:800, fontSize:"1rem", marginBottom:14 }}>Admin</div>
          {!adminOk ? <>
            <label style={lbl}>Admin-PIN</label>
            <input style={inp} type="password" placeholder="••••" value={adminPin} onChange={e=>setAdminPin(e.target.value)}
              onKeyDown={e=>{ if(e.key==="Enter") adminPin===ADMIN_PIN?(setAdminOk(true),setAdminErr("")):(setAdminErr("Falsche PIN.")); }} />
            {adminErr && <div style={{ color:"#E8002D", fontSize:".8rem", marginBottom:8 }}>{adminErr}</div>}
            <div style={{ display:"flex", gap:8 }}>
              <button style={redBtn} onClick={()=>adminPin===ADMIN_PIN?(setAdminOk(true),setAdminErr("")):(setAdminErr("Falsche PIN."))}>Entsperren</button>
              <button style={grayBtn} onClick={()=>{ setView("board"); setAdminPin(""); setAdminErr(""); }}>Zurück</button>
            </div>
          </> : <>

            {/* BULK IMPORT */}
            <div style={{ background:"#0d0d0d", border:"1px solid #262626", borderRadius:8, padding:14, marginBottom:20 }}>
              <div style={{ fontWeight:700, fontSize:".88rem", marginBottom:2, color:"#ccc" }}>Alle Namen auf einmal importieren</div>
              <div style={{ color:"#444", fontSize:".75rem", marginBottom:10 }}>Ein Name pro Zeile — alle bekommen dieselbe Standard-PIN</div>
              <textarea
                style={{...inp, height:120, resize:"vertical", marginBottom:8, fontFamily:"inherit"}}
                placeholder={"Adam Magomedov\nAhmet Kökösari\nCan Çamli\n..."}
                value={bulkText}
                onChange={e=>setBulkText(e.target.value)}
              />
              <label style={lbl}>Standard-PIN für alle</label>
              <input style={inp} type="password" placeholder="••••" value={bulkPin} onChange={e=>setBulkPin(e.target.value)} />
              {bulkMsg && <div style={{ color:bulkMsg.includes("!")?"#00A651":"#E8002D", fontSize:".8rem", marginBottom:8 }}>{bulkMsg}</div>}
              <button style={redBtn} onClick={doBulk}>Alle importieren</button>
            </div>

            {/* SINGLE ADD */}
            <div style={{ fontWeight:700, fontSize:".88rem", marginBottom:8, color:"#666" }}>Einzeln hinzufügen</div>
            <label style={lbl}>Name</label>
            <input style={inp} placeholder="Name" value={newName} onChange={e=>setNewName(e.target.value)} />
            <label style={lbl}>PIN (mind. 4 Stellen)</label>
            <input style={inp} type="password" placeholder="••••" value={newPin} onChange={e=>setNewPin(e.target.value)} />
            {addMsg && <div style={{ color:"#00A651", fontSize:".8rem", marginBottom:8 }}>{addMsg}</div>}
            <button style={{...redBtn, marginBottom:20}} onClick={doAdd}>Hinzufügen</button>

            {/* MEMBER LIST */}
            {members.length>0 && <>
              <div style={{ fontWeight:700, fontSize:".88rem", marginBottom:8, color:"#666" }}>Mitglieder ({members.length})</div>
              <div style={{ maxHeight:260, overflowY:"auto" }}>
                {members.map(m => (
                  <div key={m.name} style={{ display:"flex", justifyContent:"space-between", alignItems:"center", padding:"8px 0", borderBottom:"1px solid #1a1a1a" }}>
                    <span style={{ fontSize:".88rem", color:"#ccc" }}>{m.name}</span>
                    <button onClick={()=>doDelete(m.name)} style={{ background:"transparent", border:"1px solid #2a0000", borderRadius:4, color:"#E8002D", fontSize:".72rem", padding:"3px 10px", cursor:"pointer" }}>Entfernen</button>
                  </div>
                ))}
              </div>
            </>}
            <button style={{...grayBtn, marginTop:16}} onClick={()=>{ setView("board"); setAdminOk(false); setAdminPin(""); }}>Schließen</button>
          </>}
        </div>
      )}
    </div>
  );
}
