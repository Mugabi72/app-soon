import React, { useState } from "react";

export default function App() {
  const [activeTab, setActiveTab] = useState("scores");

  // Mock Data
  const liveScores = [
    { id: 1, home: "Arsenal", away: "Chelsea", score: "2 - 1", minute: "78'", status: "LIVE", league: "Premier League" },
    { id: 2, home: "Real Madrid", away: "Barcelona", score: "1 - 1", minute: "HT", status: "HALF TIME", league: "La Liga" },
    { id: 3, home: "Bayern Munich", away: "Dortmund", score: "3 - 0", minute: "FT", status: "FINISHED", league: "Bundesliga" },
  ];

  const standings = [
    { pos: 1, team: "Arsenal", p: 28, w: 20, d: 5, l: 3, pts: 65 },
    { pos: 2, team: "Manchester City", p: 27, w: 19, d: 6, l: 2, pts: 63 },
    { pos: 3, team: "Liverpool", p: 28, w: 18, d: 7, l: 3, pts: 61 },
    { pos: 4, team: "Aston Villa", p: 28, w: 17, d: 4, l: 7, pts: 55 },
  ];

  const newsList = [
    { id: 1, title: "Title Race Heats Up as Arsenal Secure Crucial Win", time: "2 hours ago", category: "Premier League" },
    { id: 2, title: "Champions League Quarter-Final Draw: What to Expect", time: "5 hours ago", category: "UEFA Champions League" },
    { id: 3, title: "Rising Star Striker Breaks All-Time Scoring Record", time: "1 day ago", category: "Transfers" },
  ];

  return (
    <div className="min-h-screen bg-slate-900 text-slate-100 font-sans">
      {/* Header / Navbar */}
      <header className="bg-slate-950 border-b border-slate-800 sticky top-0 z-50">
        <div className="max-w-6xl mx-auto px-4 py-4 flex flex-col sm:flex-row justify-between items-center gap-4">
          <div className="flex items-center space-x-2">
            <span className="text-3xl">⚽</span>
            <h1 className="text-2xl font-black tracking-wider text-emerald-400">PITCH<span className="text-white">LIVE</span></h1>
          </div>
          <nav className="flex space-x-2 bg-slate-900 p-1 rounded-xl border border-slate-800">
            <button 
              onClick={() => setActiveTab("scores")} 
              className={`px-4 py-2 rounded-lg text-sm font-semibold transition ${activeTab === "scores" ? "bg-emerald-500 text-white shadow-lg" : "text-slate-400 hover:text-white"}`}
            >
              Live Scores
            </button>
            <button 
              onClick={() => setActiveTab("standings")} 
              className={`px-4 py-2 rounded-lg text-sm font-semibold transition ${activeTab === "standings" ? "bg-emerald-500 text-white shadow-lg" : "text-slate-400 hover:text-white"}`}
            >
              Standings
            </button>
            <button 
              onClick={() => setActiveTab("news")} 
              className={`px-4 py-2 rounded-lg text-sm font-semibold transition ${activeTab === "news" ? "bg-emerald-500 text-white shadow-lg" : "text-slate-400 hover:text-white"}`}
            >
              News
            </button>
          </nav>
        </div>
      </header>

      {/* Main Content Area */}
      <main className="max-w-6xl mx-auto px-4 py-8">
        {/* TAB 1: LIVE SCORES */}
        {activeTab === "scores" && (
          <div className="space-y-6">
            <div className="flex justify-between items-center">
              <h2 className="text-xl font-bold border-l-4 border-emerald-500 pl-3">Today's Match Center</h2>
              <span className="text-xs bg-emerald-500/20 text-emerald-400 px-3 py-1 rounded-full border border-emerald-500/30 font-semibold animate-pulse">● LIVE UPDATES ACTIVE</span>
            </div>

            <div className="grid grid-cols-1 md:grid-cols-3 gap-4">
              {liveScores.map((match) => (
                <div key={match.id} className="bg-slate-800/60 border border-slate-700/60 rounded-2xl p-5 hover:border-emerald-500/50 transition shadow-xl">
                  <div className="flex justify-between text-xs text-slate-400 mb-4 font-medium">
                    <span>{match.league}</span>
                    <span className={`px-2 py-0.5 rounded text-[10px] font-bold ${match.status === 'LIVE' ? 'bg-red-500/20 text-red-400 border border-red-500/30' : 'bg-slate-700 text-slate-300'}`}>
                      {match.status} ({match.minute})
                    </span>
                  </div>
                  
                  <div className="flex justify-between items-center my-3">
                    <span className="font-bold text-lg w-5/12 truncate">{match.home}</span>
                    <span className="text-xl font-black bg-slate-900 px-4 py-2 rounded-xl text-emerald-400 border border-slate-700">{match.score}</span>
                    <span className="font-bold text-lg w-5/12 text-right truncate">{match.away}</span>
                  </div>

                  <div className="mt-4 pt-3 border-t border-slate-700/50 text-center">
                    <button className="text-xs font-semibold text-emerald-400 hover:text-emerald-300 transition">View Match Stats &rarr;</button>
                  </div>
                </div>
              ))}
            </div>
          </div>
        )}

        {/* TAB 2: STANDINGS */}
        {activeTab === "standings" && (
          <div className="space-y-6">
            <h2 className="text-xl font-bold border-l-4 border-emerald-500 pl-3">Premier League Standings</h2>
            
            <div className="bg-slate-800/50 border border-slate-700/60 rounded-2xl overflow-hidden shadow-xl">
              <table className="w-full text-left border-collapse">
                <thead>
                  <tr className="bg-slate-900/80 text-slate-400 text-xs uppercase tracking-wider border-b border-slate-700">
                    <th className="py-3 px-4">Pos</th>
                    <th className="py-3 px-4">Club</th>
                    <th className="py-3 px-4 text-center">P</th>
                    <th className="py-3 px-4 text-center">W</th>
                    <th className="py-3 px-4 text-center">D</th>
                    <th className="py-3 px-4 text-center">L</th>
                    <th className="py-3 px-4 text-center font-bold text-emerald-400">Pts</th>
                  </tr>
                </thead>
                <tbody className="divide-y divide-slate-700/50 text-sm">
                  {standings.map((row) => (
                    <tr key={row.pos} className="hover:bg-slate-700/30 transition">
                      <td className="py-3 px-4 font-bold text-slate-400">{row.pos}</td>
                      <td className="py-3 px-4 font-semibold text-white">{row.team}</td>
                      <td className="py-3 px-4 text-center text-slate-300">{row.p}</td>
                      <td className="py-3 px-4 text-center text-slate-300">{row.w}</td>
                      <td className="py-3 px-4 text-center text-slate-300">{row.d}</td>
                      <td className="py-3 px-4 text-center text-slate-300">{row.l}</td>
                      <td className="py-3 px-4 text-center font-black text-emerald-400">{row.pts}</td>
                    </tr>
                  ))}
                </tbody>
              </table>
            </div>
          </div>
        )}

        {/* TAB 3: NEWS */}
        {activeTab === "news" && (
          <div className="space-y-6">
            <h2 className="text-xl font-bold border-l-4 border-emerald-500 pl-3">Latest Football News</h2>
            
            <div className="grid grid-cols-1 md:grid-cols-3 gap-6">
              {newsList.map((news) => (
                <div key={news.id} className="bg-slate-800/60 border border-slate-700/60 rounded-2xl p-5 flex flex-col justify-between hover:border-emerald-500/50 transition shadow-xl">
                  <div>
                    <span className="text-xs bg-emerald-500/10 text-emerald-400 px-2.5 py-1 rounded-full font-semibold border border-emerald-500/20">{news.category}</span>
                    <h3 className="text-lg font-bold mt-3 leading-snug text-slate-100">{news.title}</h3>
                  </div>
                  <div className="mt-6 flex justify-between items-center text-xs text-slate-400 pt-3 border-t border-slate-700/50">
                    <span>{news.time}</span>
                    <button className="text-emerald-400 font-semibold hover:underline">Read Article</button>
                  </div>
                </div>
              ))}
            </div>
          </div>
        )}
      </main>

      {/* Footer */}
      <footer className="mt-16 bg-slate-950 border-t border-slate-800 py-6 text-center text-xs text-slate-500">
        <p>&copy; 2026 PitchLive Football App. Built with React & Tailwind CSS.</p>
      </footer>
    </div>
  );
}
