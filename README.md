<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>PRAXIS — The Mindful Process Engine</title>
  
  <!-- Fonts -->
  <link rel="preconnect" href="https://fonts.googleapis.com">
  <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
  <link href="https://fonts.googleapis.com/css2?family=Newsreader:ital,opsz,wght@0,6..72,400;0,6..72,500;0,6..72,600;1,6..72,400;1,6..72,600&family=Plus+Jakarta+Sans:wght@300;400;500;600;700&family=JetBrains+Mono:wght@400;500&display=swap" rel="stylesheet">
  
  <!-- Tailwind CSS -->
  <script src="https://cdn.tailwindcss.com"></script>
  <!-- Lucide Icons -->
  <script src="https://unpkg.com/lucide@latest"></script>

  <script>
    tailwind.config = {
      darkMode: 'class',
      theme: {
        extend: {
          fontFamily: {
            sans: ['"Plus Jakarta Sans"', 'sans-serif'],
            serif: ['"Newsreader"', 'serif'],
            mono: ['"JetBrains Mono"', 'monospace'],
          },
          colors: {
            theme: {
              base: 'var(--bg-base)',
              surface: 'var(--bg-surface)',
              panel: 'var(--bg-panel)',
              border: 'var(--border-color)',
              accent: 'var(--accent-color)',
              accentHover: 'var(--accent-hover)',
              accentGlow: 'var(--accent-glow)',
              textMuted: 'var(--text-muted)',
              textBright: 'var(--text-bright)',
            }
          }
        }
      }
    }
  </script>

  <style>
    /* Theme color palettes with friendly, science-backed benefits */
    :root {
      /* Ocean Teal (Default): Relaxes tired eyes & steadies breathing */
      --bg-base: #061113;
      --bg-surface: #0a191c;
      --bg-panel: rgba(10, 25, 28, 0.82);
      --border-color: rgba(45, 212, 191, 0.18);
      --accent-color: #2dd4bf;
      --accent-hover: #14b8a6;
      --accent-glow: rgba(45, 212, 191, 0.3);
      --text-muted: #82a3aa;
      --text-bright: #e8faf7;
      --transition-speed: 0.5s;
    }

    [data-theme="amber"] {
      /* Candlelight Amber: Cozy evening light that protects sleep hormones */
      --bg-base: #110b06;
      --bg-surface: #1a1109;
      --bg-panel: rgba(26, 17, 9, 0.85);
      --border-color: rgba(245, 158, 11, 0.2);
      --accent-color: #f59e0b;
      --accent-hover: #d97706;
      --accent-glow: rgba(245, 158, 11, 0.35);
      --text-muted: #af927d;
      --text-bright: #fef4dc;
    }

    [data-theme="forest"] {
      /* Forest Green: Natural soothing greens that signal safety to your body */
      --bg-base: #051009;
      --bg-surface: #091a0f;
      --bg-panel: rgba(9, 26, 15, 0.84);
      --border-color: rgba(52, 211, 153, 0.2);
      --accent-color: #34d399;
      --accent-hover: #10b981;
      --accent-glow: rgba(52, 211, 153, 0.32);
      --text-muted: #81aa92;
      --text-bright: #eafaf1;
    }

    [data-theme="indigo"] {
      /* Midnight Indigo: Crisp, dark night sky mode for distraction-free logic */
      --bg-base: #060914;
      --bg-surface: #0b1124;
      --bg-panel: rgba(11, 17, 36, 0.85);
      --border-color: rgba(129, 140, 248, 0.2);
      --accent-color: #818cf8;
      --accent-hover: #6366f1;
      --accent-glow: rgba(129, 140, 248, 0.32);
      --text-muted: #8895c0;
      --text-bright: #eef2ff;
    }

    body {
      background-color: var(--bg-base);
      color: var(--text-bright);
      transition: background-color var(--transition-speed) ease, color var(--transition-speed) ease;
    }

    .glass-surface {
      background-color: var(--bg-panel);
      backdrop-filter: blur(16px);
      -webkit-backdrop-filter: blur(16px);
      border: 1px solid var(--border-color);
      transition: all var(--transition-speed) ease;
    }

    .glass-surface:hover {
      box-shadow: 0 10px 30px -10px var(--accent-glow);
    }

    .border-theme {
      border-color: var(--border-color);
    }

    @keyframes physiologicalSigh {
      0% { transform: scale(0.85); opacity: 0.45; }
      35% { transform: scale(1.15); opacity: 0.85; }
      50% { transform: scale(1.3); opacity: 1; }
      100% { transform: scale(0.85); opacity: 0.45; }
    }

    .animate-sigh-ring {
      animation: physiologicalSigh 6.5s cubic-bezier(0.4, 0, 0.2, 1) infinite;
    }

    ::-webkit-scrollbar {
      width: 6px;
      height: 6px;
    }
    ::-webkit-scrollbar-track {
      background: var(--bg-base);
    }
    ::-webkit-scrollbar-thumb {
      background: var(--border-color);
      border-radius: 9999px;
    }
  </style>
</head>
<body class="min-h-screen font-sans antialiased selection:bg-teal-500/30 selection:text-teal-200 overflow-x-hidden flex flex-col justify-between" data-theme="teal">

  <!-- Ambient Background Lighting -->
  <div class="fixed inset-0 pointer-events-none z-0 overflow-hidden">
    <div id="ambientHalo1" class="absolute -top-40 -left-40 w-[620px] h-[620px] rounded-full blur-[170px] opacity-35 transition-colors duration-1000" style="background-color: var(--accent-color);"></div>
    <div id="ambientHalo2" class="absolute top-1/2 -right-40 w-[620px] h-[620px] rounded-full blur-[180px] opacity-25 transition-colors duration-1000" style="background-color: var(--accent-color);"></div>
  </div>

  <!-- Easy Color Selector & Friendly Benefits Bar -->
  <div class="relative z-40 border-b border-theme/60 bg-black/40 backdrop-blur-md px-4 sm:px-8 py-2.5 text-xs transition-colors duration-500">
    <div class="max-w-7xl mx-auto flex flex-wrap items-center justify-between gap-3">
      
      <div class="flex items-center gap-2">
        <span class="text-[11px] font-mono uppercase tracking-wider text-theme-textMuted flex items-center gap-1.5">
          <i data-lucide="palette" class="w-3.5 h-3.5 text-theme-accent"></i>
          <span>Calming Colors:</span>
        </span>
        <div class="flex items-center gap-1 bg-black/50 p-1 rounded-xl border border-theme/40">
          <button onclick="setTheme('teal')" id="btnThemeTeal" class="px-2.5 py-1 rounded-lg transition-all flex items-center gap-1.5 font-medium border border-teal-500/50 bg-teal-500/20 text-teal-300" title="Cuts screen glare and helps your eyes relax">
            <span class="w-2 h-2 rounded-full bg-teal-400"></span>
            <span>Ocean Teal</span>
          </button>
          <button onclick="setTheme('amber')" id="btnThemeAmber" class="px-2.5 py-1 rounded-lg transition-all flex items-center gap-1.5 font-medium border border-transparent text-theme-textMuted hover:text-amber-300" title="Zero blue glare for cozy evening focus">
            <span class="w-2 h-2 rounded-full bg-amber-400"></span>
            <span>Candlelight</span>
          </button>
          <button onclick="setTheme('forest')" id="btnThemeForest" class="px-2.5 py-1 rounded-lg transition-all flex items-center gap-1.5 font-medium border border-transparent text-theme-textMuted hover:text-emerald-300" title="Nature greens that make you feel grounded">
            <span class="w-2 h-2 rounded-full bg-emerald-400"></span>
            <span>Forest Green</span>
          </button>
          <button onclick="setTheme('indigo')" id="btnThemeIndigo" class="px-2.5 py-1 rounded-lg transition-all flex items-center gap-1.5 font-medium border border-transparent text-theme-textMuted hover:text-indigo-300" title="Clear night sky tone for quiet, deep thought">
            <span class="w-2 h-2 rounded-full bg-indigo-400"></span>
            <span>Midnight Indigo</span>
          </button>
        </div>
      </div>

      <!-- Plain English Color Rationale -->
      <div class="flex items-center gap-2 px-3 py-1 rounded-full bg-theme-surface/70 border border-theme text-[11px] text-theme-textMuted">
        <i data-lucide="sparkles" class="w-3.5 h-3.5 text-theme-accent shrink-0"></i>
        <span id="rationaleText" class="truncate">Ocean Teal: Soft on your eyes, eases screen strain, and slows down your breathing.</span>
      </div>

      <!-- Plain English Guide Button -->
      <button onclick="openScienceInPlainEnglishModal()" class="text-[11px] text-theme-accent hover:underline flex items-center gap-1 font-mono">
        <i data-lucide="help-circle" class="w-3.5 h-3.5"></i>
        <span>How it works in plain English</span>
      </button>

    </div>
  </div>

  <!-- Main Header -->
  <header class="relative z-30 border-b border-theme/60 bg-theme-base/80 backdrop-blur-xl px-4 sm:px-8 py-3.5 transition-colors duration-500">
    <div class="max-w-7xl mx-auto flex items-center justify-between">
      <div class="flex items-center gap-3.5">
        <div class="w-11 h-11 rounded-2xl bg-gradient-to-br from-theme-surface to-black/60 border border-theme flex items-center justify-center text-theme-accent shadow-inner">
          <i data-lucide="activity" class="w-6 h-6 stroke-[2.2]"></i>
        </div>
        <div>
          <div class="flex items-center gap-2">
            <h1 class="font-serif text-2xl tracking-tight font-semibold bg-gradient-to-r from-white via-slate-100 to-theme-accent bg-clip-text text-transparent">PRAXIS</h1>
            <span class="text-[10px] font-mono tracking-widest uppercase px-2 py-0.5 rounded-full border border-theme/60 bg-white/5 text-theme-accent">Process Over Outcome</span>
          </div>
          <p class="text-xs text-theme-textMuted hidden sm:block">Mindful steps, zero pressure, and rewarding progress</p>
        </div>
      </div>

      <!-- Action Nav -->
      <div class="flex items-center gap-3">
        <!-- Soothing Background Sounds -->
        <button id="soundToggleBtn" onclick="toggleSoundEngine()" class="px-3 py-2 rounded-xl bg-theme-surface/80 border border-theme hover:border-theme-accent text-theme-textMuted hover:text-white transition flex items-center gap-2 text-xs font-medium">
          <i data-lucide="volume-2" class="w-4 h-4 text-theme-accent"></i>
          <span id="soundLabel">Calm Sounds: Off</span>
        </button>

        <!-- New Task CTA -->
        <button onclick="openCreateModal()" class="px-4 py-2.5 rounded-xl font-semibold text-xs tracking-wide uppercase transition-all shadow-lg flex items-center gap-2 transform active:scale-95 text-black" style="background-color: var(--accent-color); box-shadow: 0 4px 20px var(--accent-glow);">
          <i data-lucide="plus-circle" class="w-4 h-4"></i>
          <span>New Process</span>
        </button>
      </div>
    </div>
  </header>

  <!-- Main Application Body -->
  <main class="relative z-10 max-w-7xl mx-auto px-4 sm:px-8 py-8 space-y-8 flex-1 w-full">
    
    <!-- Hero / Friendly Core Concept -->
    <section class="glass-surface rounded-3xl p-6 sm:p-8 relative overflow-hidden">
      <div class="flex flex-col lg:flex-row lg:items-center justify-between gap-6 relative z-10">
        <div class="max-w-2xl space-y-3">
          <div class="inline-flex items-center gap-2 px-3 py-1 rounded-full bg-theme-accent/10 border border-theme text-theme-accent text-xs font-mono">
            <i data-lucide="heart" class="w-3.5 h-3.5"></i>
            <span>No Shame • No Rushing • Pure Flow</span>
          </div>
          <h2 class="font-serif text-2xl sm:text-3xl text-slate-100 font-normal leading-snug">
            "Stop stressing over the finish line. Enjoy <span class="italic text-theme-accent font-serif">the step you're taking right now</span>."
          </h2>
          <p class="text-sm text-theme-textMuted leading-relaxed">
            Most to-do lists make you feel guilty for what isn't done yet. PRAXIS rewards you simply for <strong>showing up</strong>, taking a gentle 30-second start, and enjoying the craft.
          </p>
        </div>

        <!-- Quick Sound Preset Selector -->
        <div class="p-4 rounded-2xl bg-black/40 border border-theme/60 space-y-2.5 shrink-0 min-w-[250px]">
          <span class="text-[11px] uppercase tracking-wider font-mono text-theme-textMuted block flex items-center gap-1.5">
            <i data-lucide="headphones" class="w-3.5 h-3.5 text-theme-accent"></i> Ambient Background Sound:
          </span>
          <div class="grid grid-cols-2 gap-2 text-xs">
            <button onclick="setAudioFrequency('brown')" id="btnFreqBrown" class="px-2.5 py-1.5 rounded-lg border border-theme/40 bg-white/[0.02] text-theme-textMuted hover:text-white transition">Warm Rain Noise</button>
            <button onclick="setAudioFrequency('alpha')" id="btnFreqAlpha" class="px-2.5 py-1.5 rounded-lg border border-theme/40 bg-white/[0.02] text-theme-textMuted hover:text-white transition">10Hz Calm Flow</button>
            <button onclick="setAudioFrequency('gamma')" id="btnFreqGamma" class="px-2.5 py-1.5 rounded-lg border border-theme/40 bg-white/[0.02] text-theme-textMuted hover:text-white transition">40Hz Deep Focus</button>
            <button onclick="stopAudioEngine()" class="px-2.5 py-1.5 rounded-lg border border-theme/40 bg-white/[0.02] text-rose-400 hover:bg-rose-500/10 transition">Mute</button>
          </div>
        </div>
      </div>

      <!-- Friendly Stats Row -->
      <div class="mt-8 pt-6 border-t border-theme/40 grid grid-cols-2 sm:grid-cols-4 gap-3.5">
        <div class="p-3.5 rounded-2xl bg-white/[0.02] border border-theme/50">
          <div class="text-[11px] font-mono text-theme-textMuted uppercase flex items-center gap-1.5">
            <i data-lucide="clock" class="w-3.5 h-3.5 text-theme-accent"></i> Minutes in Flow
          </div>
          <div class="text-xl sm:text-2xl font-semibold text-slate-100 mt-1 font-mono" id="statArenaTime">0 min</div>
          <span class="text-[10px] text-theme-textMuted">Pure, focused practice</span>
        </div>

        <div class="p-3.5 rounded-2xl bg-white/[0.02] border border-theme/50">
          <div class="text-[11px] font-mono text-theme-textMuted uppercase flex items-center gap-1.5">
            <i data-lucide="award" class="w-3.5 h-3.5 text-amber-400"></i> Badges Earned
          </div>
          <div class="text-xl sm:text-2xl font-semibold text-slate-100 mt-1 font-mono" id="statIdentityVotes">0</div>
          <span class="text-[10px] text-theme-textMuted">Processes honored</span>
        </div>

        <div class="p-3.5 rounded-2xl bg-white/[0.02] border border-theme/50">
          <div class="text-[11px] font-mono text-theme-textMuted uppercase flex items-center gap-1.5">
            <i data-lucide="sprout" class="w-3.5 h-3.5 text-emerald-400"></i> Seeds Planted
          </div>
          <div class="text-xl sm:text-2xl font-semibold text-slate-100 mt-1 font-mono" id="statSeedsCount">0</div>
          <span class="text-[10px] text-theme-textMuted">Guilt-free early pauses</span>
        </div>

        <div class="p-3.5 rounded-2xl bg-white/[0.02] border border-theme/50">
          <div class="text-[11px] font-mono text-theme-textMuted uppercase flex items-center gap-1.5">
            <i data-lucide="bookmark" class="w-3.5 h-3.5 text-indigo-400"></i> Mental Bookmarks
          </div>
          <div class="text-xl sm:text-2xl font-semibold text-slate-100 mt-1 font-mono" id="statBookmarksCount">0</div>
          <span class="text-[10px] text-theme-textMuted">Saved notes for later</span>
        </div>
      </div>
    </section>

    <!-- Navigation Tabs & Templates -->
    <div class="flex flex-col sm:flex-row items-start sm:items-center justify-between gap-4">
      <div class="flex items-center gap-1 p-1 rounded-2xl bg-black/40 border border-theme/60 text-xs">
        <button onclick="setDashboardTab('active')" id="tabActiveBtn" class="px-4 py-2 rounded-xl font-medium transition-all bg-white/10 text-theme-accent border border-theme">
          My Processes (<span id="activeCountBadge">0</span>)
        </button>
        <button onclick="setDashboardTab('bookmarks')" id="tabBookmarksBtn" class="px-4 py-2 rounded-xl font-medium text-theme-textMuted hover:text-white transition-all">
          Mental Bookmarks &amp; Seeds (<span id="bookmarksCountBadge">0</span>)
        </button>
        <button onclick="setDashboardTab('chronicle')" id="tabChronicleBtn" class="px-4 py-2 rounded-xl font-medium text-theme-textMuted hover:text-white transition-all">
          Badge Trophy Room (<span id="trophyCountBadge">0</span>)
        </button>
      </div>

      <!-- Ready-Made Easy Templates -->
      <div class="flex items-center gap-2 overflow-x-auto w-full sm:w-auto pb-1 sm:pb-0 text-xs">
        <span class="text-theme-textMuted shrink-0 font-mono text-[11px] flex items-center gap-1">
          <i data-lucide="sparkle" class="w-3.5 h-3.5 text-theme-accent"></i> Quick Start:
        </span>
        <button onclick="loadTemplate('writing')" class="px-3 py-1.5 rounded-xl bg-white/[0.03] hover:bg-white/[0.08] border border-theme/40 text-slate-200 shrink-0 transition">
          🖋️ Casual Writing
        </button>
        <button onclick="loadTemplate('coding')" class="px-3 py-1.5 rounded-xl bg-white/[0.03] hover:bg-white/[0.08] border border-theme/40 text-slate-200 shrink-0 transition">
          💻 Deep Focus Project
        </button>
        <button onclick="loadTemplate('reading')" class="px-3 py-1.5 rounded-xl bg-white/[0.03] hover:bg-white/[0.08] border border-theme/40 text-slate-200 shrink-0 transition">
          📖 Calm Reading Session
        </button>
      </div>
    </div>

    <!-- Active Tasks Grid -->
    <div id="activeProcessesGrid" class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-5">
      <!-- Injected by JavaScript -->
    </div>

    <!-- Bookmarks View -->
    <div id="bookmarksView" class="hidden space-y-4">
      <!-- Injected by JavaScript -->
    </div>

    <!-- Badge Trophy Room View -->
    <div id="chronicleView" class="hidden space-y-6">
      <!-- Injected by JavaScript -->
    </div>

  </main>

  <!-- Create Process Modal (In Plain, Friendly Terms) -->
  <div id="createModal" class="fixed inset-0 z-50 bg-black/80 backdrop-blur-md flex items-center justify-center p-4 opacity-0 pointer-events-none transition-all duration-300">
    <div class="glass-surface w-full max-w-2xl rounded-3xl p-6 sm:p-8 max-h-[92vh] overflow-y-auto transform scale-95 transition-all duration-300 border border-theme shadow-2xl" id="createModalBox">
      
      <div class="flex items-center justify-between border-b border-theme/50 pb-4">
        <div>
          <span class="text-[11px] font-mono uppercase tracking-widest text-theme-accent">Plan Your Session</span>
          <h3 class="font-serif text-2xl text-slate-100 font-medium">Create a Mindful Process</h3>
        </div>
        <button onclick="closeCreateModal()" class="p-2 rounded-xl text-theme-textMuted hover:text-white hover:bg-white/5 transition">
          <i data-lucide="x" class="w-5 h-5"></i>
        </button>
      </div>

      <form id="createProcessForm" onsubmit="handleCreateProcess(event)" class="space-y-5 mt-5">
        
        <!-- Task Title -->
        <div>
          <label class="block text-xs font-mono uppercase tracking-wider text-theme-accent mb-1.5 flex items-center justify-between">
            <span>What are you doing?</span>
            <span class="text-[10px] text-theme-textMuted normal-case">Focus on the action, not the final result</span>
          </label>
          <input type="text" id="inputIntention" required placeholder="e.g., Draft 2 pages of ideas without worrying if they are perfect" class="w-full px-4 py-3 rounded-xl bg-black/50 border border-theme/60 focus:border-theme-accent text-slate-100 placeholder:text-theme-textMuted/50 text-sm outline-none transition">
        </div>

        <!-- The "Why" -->
        <div>
          <label class="block text-xs font-mono uppercase tracking-wider text-theme-accent mb-1.5 flex items-center gap-1.5">
            <i data-lucide="heart" class="w-3.5 h-3.5 text-rose-400"></i>
            <span>Why are you doing this? (The Real Reason)</span>
          </label>
          <textarea id="inputWhy" rows="2" required placeholder="What makes this meaningful to you? e.g., To clear my head, build confidence, or learn something exciting." class="w-full px-4 py-2.5 rounded-xl bg-black/50 border border-theme/60 focus:border-theme-accent text-slate-100 placeholder:text-theme-textMuted/50 text-sm outline-none transition"></textarea>
        </div>

        <!-- Easy Kickstart (Step 0) & What's In The Way -->
        <div class="grid grid-cols-1 sm:grid-cols-2 gap-4 p-4 rounded-2xl bg-white/[0.02] border border-theme/40">
          <div>
            <label class="block text-xs font-mono uppercase tracking-wider text-amber-300 mb-1 flex items-center gap-1.5">
              <i data-lucide="help-circle" class="w-3.5 h-3.5"></i>
              <span>What's holding you back?</span>
            </label>
            <select id="inputFriction" onchange="updateFrictionTip()" class="w-full px-3 py-2 rounded-xl bg-black/60 border border-theme/60 text-xs text-slate-200 outline-none">
              <option value="ambiguity">Not sure where to begin (Too messy)</option>
              <option value="fear">Fear of doing it badly (Perfectionism)</option>
              <option value="boredom">Boring or lacks quick excitement</option>
              <option value="fatigue">Tired or low physical energy</option>
            </select>
            <div id="frictionTip" class="text-[11px] text-theme-textMuted mt-1.5 italic">Tip: Just break it down into an easy 30-second start.</div>
          </div>

          <div>
            <label class="block text-xs font-mono uppercase tracking-wider text-emerald-300 mb-1 flex items-center gap-1.5">
              <i data-lucide="play-circle" class="w-3.5 h-3.5"></i>
              <span>The Easy Kickstart (The 30-Second Rule)</span>
            </label>
            <input type="text" id="inputStepZero" required placeholder="e.g., Open the app and write one messy sentence" class="w-full px-3 py-2 rounded-xl bg-black/60 border border-theme/60 text-xs text-slate-200 outline-none">
            <span class="text-[10px] text-theme-textMuted">Starting is the hardest part. Just doing 30s tricks your brain into motion!</span>
          </div>
        </div>

        <!-- Time Presets & Boundaries -->
        <div class="grid grid-cols-1 sm:grid-cols-3 gap-3">
          <div>
            <label class="block text-xs font-mono text-theme-textMuted mb-1">Time Preset</label>
            <select id="inputDurationPreset" onchange="applyDurationPreset()" class="w-full px-3 py-2 rounded-xl bg-black/60 border border-theme/60 text-xs text-slate-200 outline-none">
              <option value="15">15 min (Quick &amp; Light)</option>
              <option value="25">25 min (Standard Focus)</option>
              <option value="45" selected>45 min (Classic Flow Block)</option>
              <option value="60">60 min (Deep Session)</option>
              <option value="custom">Custom Minutes</option>
            </select>
          </div>
          <div>
            <label class="block text-xs font-mono text-theme-textMuted mb-1">Duration (Minutes)</label>
            <input type="number" id="inputDurationVal" min="1" max="180" value="45" class="w-full px-3 py-2 rounded-xl bg-black/60 border border-theme/60 text-xs text-slate-200 outline-none">
          </div>
          <div>
            <label class="block text-xs font-mono text-theme-textMuted mb-1">Time Boundary (When?)</label>
            <input type="text" id="inputHorizon" placeholder="e.g., 2:00 PM – 2:45 PM" class="w-full px-3 py-2 rounded-xl bg-black/60 border border-theme/60 text-xs text-slate-200 outline-none">
          </div>
        </div>

        <!-- Process Steps (Manageable Sub-actions) -->
        <div>
          <div class="flex items-center justify-between mb-1.5">
            <label class="text-xs font-mono uppercase tracking-wider text-theme-accent flex items-center gap-1.5">
              <i data-lucide="check-square" class="w-3.5 h-3.5"></i>
              <span>The Steps (Small, friendly checkpoints)</span>
            </label>
            <button type="button" onclick="addModalStepRow()" class="text-xs text-theme-accent hover:underline flex items-center gap-1">
              <i data-lucide="plus" class="w-3 h-3"></i> Add Step
            </button>
          </div>
          <div id="modalStepList" class="space-y-2">
            <!-- Dynamic step rows -->
          </div>
        </div>

        <!-- Custom Real-Life Treat (User Choice) -->
        <div class="p-3.5 rounded-2xl bg-black/40 border border-theme/40 space-y-1.5">
          <label class="block text-xs font-mono uppercase tracking-wider text-purple-300 flex items-center gap-1.5">
            <i data-lucide="gift" class="w-3.5 h-3.5"></i>
            <span>Real-Life Treat to Unlock (Optional)</span>
          </label>
          <input type="text" id="inputCustomReward" placeholder="e.g., Enjoy a cup of warm tea, stretch outside in the sun, or 10 min guilt-free reading" class="w-full px-3 py-2 rounded-xl bg-white/[0.03] border border-theme/50 text-xs text-slate-100 outline-none">
        </div>

        <!-- Submit Buttons -->
        <div class="pt-4 border-t border-theme/50 flex items-center justify-end gap-3">
          <button type="button" onclick="closeCreateModal()" class="px-5 py-2.5 rounded-xl text-xs font-medium text-theme-textMuted hover:text-white transition">Cancel</button>
          <button type="submit" class="px-6 py-2.5 rounded-xl text-xs font-semibold tracking-wide uppercase transition shadow-lg text-black" style="background-color: var(--accent-color); box-shadow: 0 4px 15px var(--accent-glow);">
            Commit to the Process
          </button>
        </div>
      </form>
    </div>
  </div>

  <!-- 10-Second Calming Breath Gate -->
  <div id="somaticModal" class="fixed inset-0 z-50 bg-black/90 backdrop-blur-2xl flex items-center justify-center p-4 opacity-0 pointer-events-none transition-all duration-500">
    <div class="max-w-md w-full text-center space-y-6">
      
      <div class="inline-flex items-center gap-2 px-3 py-1 rounded-full bg-theme-accent/10 border border-theme text-theme-accent text-xs font-mono">
        <i data-lucide="wind" class="w-3.5 h-3.5"></i>
        <span>10-Second Calming Breath</span>
      </div>

      <div class="space-y-2">
        <h3 class="font-serif text-3xl text-slate-100 font-medium">Clear Your Head</h3>
        <p class="text-xs text-theme-textMuted max-w-sm mx-auto leading-relaxed">
          Take two quick breaths through your nose, then one slow, long sigh out through your mouth. This immediately tells your body to relax.
        </p>
      </div>

      <!-- Breathing Ring -->
      <div class="relative w-60 h-60 mx-auto flex items-center justify-center">
        <div class="absolute inset-0 rounded-full border border-theme/30 animate-sigh-ring"></div>
        <div class="absolute inset-4 rounded-full border border-theme-accent/40 animate-sigh-ring" style="animation-delay: 0.3s;"></div>
        
        <div class="w-44 h-44 rounded-full bg-theme-surface border border-theme flex flex-col items-center justify-center p-4 shadow-2xl relative z-10">
          <span id="breathPhaseText" class="font-serif text-base text-theme-accent italic transition-all">Quick Inhale 1...</span>
          <span id="breathCountdown" class="text-3xl font-mono text-slate-100 font-light mt-1">4</span>
          <span class="text-[10px] font-mono uppercase text-theme-textMuted mt-1">Filling lungs</span>
        </div>
      </div>

      <div class="flex items-center justify-center gap-3">
        <button onclick="skipSomaticGate()" class="px-5 py-2.5 rounded-xl border border-theme/50 text-xs font-mono text-theme-textMuted hover:text-white transition">
          Skip to Kickstart
        </button>
        <button onclick="enterFlowTunnelNow()" class="px-6 py-2.5 rounded-xl text-xs font-mono uppercase tracking-wide font-semibold text-black transition shadow-lg" style="background-color: var(--accent-color);">
          I'm Ready • Let's Go
        </button>
      </div>

    </div>
  </div>

  <!-- Single-Task Focus Tunnel (All other tasks hidden) -->
  <div id="flowTunnelOverlay" class="fixed inset-0 z-50 bg-theme-base/98 backdrop-blur-2xl flex flex-col justify-between p-4 sm:p-8 opacity-0 pointer-events-none transition-all duration-500">
    
    <!-- Top Tunnel Bar -->
    <div class="max-w-4xl w-full mx-auto flex items-center justify-between border-b border-theme/50 pb-4">
      <div class="flex items-center gap-3">
        <div class="w-3 h-3 rounded-full bg-emerald-400 animate-ping"></div>
        <div>
          <span class="text-[10px] font-mono uppercase tracking-widest text-theme-accent">Laser Focus Mode (Distractions Hidden)</span>
          <h2 id="tunnelIntentionTitle" class="font-serif text-lg sm:text-xl text-slate-100 font-medium">Task In Hand</h2>
        </div>
      </div>

      <div class="flex items-center gap-2">
        <button onclick="promptHaltEarly()" class="px-3.5 py-1.5 rounded-xl border border-theme/60 text-xs font-mono text-theme-textMuted hover:text-emerald-300 hover:border-emerald-400/40 transition flex items-center gap-1.5" title="Pause whenever you feel tired — rest is part of work!">
          <i data-lucide="pause-circle" class="w-3.5 h-3.5"></i>
          <span>Pause &amp; Save Bookmark (No Guilt)</span>
        </button>
      </div>
    </div>

    <!-- Center Focus Core -->
    <div class="max-w-2xl w-full mx-auto my-auto text-center space-y-6">
      
      <!-- Step 0 30-Second Kickstart Banner -->
      <div id="tunnelStepZeroBanner" class="p-4 rounded-2xl bg-amber-500/10 border border-amber-500/30 text-amber-200 text-xs flex items-center justify-between gap-3 text-left">
        <div class="flex items-center gap-3">
          <span class="w-7 h-7 rounded-xl bg-amber-500/20 text-amber-300 flex items-center justify-center font-mono font-bold text-xs shrink-0">30s</span>
          <div>
            <strong class="font-mono uppercase text-[10px] tracking-wide block text-amber-300">Easy Kickstart (First 30 seconds only):</strong>
            <span id="tunnelStepZeroText">Open the blank document</span>
          </div>
        </div>
        <button onclick="dismissStepZero()" class="px-3 py-1.5 rounded-xl bg-amber-500/20 hover:bg-amber-500/30 text-xs font-mono text-amber-200 shrink-0 font-medium">Done!</button>
      </div>

      <!-- Why Reminder -->
      <div class="p-3 rounded-2xl bg-white/[0.02] border border-theme/40 text-xs text-theme-textMuted max-w-lg mx-auto italic">
        <span class="text-theme-accent not-italic font-mono text-[10px] uppercase block mb-0.5">Remember Your Why:</span>
        <span id="tunnelWhyText">Why you practice...</span>
      </div>

      <!-- Live Circular Timer -->
      <div class="relative w-64 h-64 sm:w-72 sm:h-72 mx-auto flex items-center justify-center">
        <svg class="w-full h-full transform -rotate-90">
          <circle cx="50%" cy="50%" r="42%" stroke="currentColor" stroke-width="4" fill="transparent" class="text-white/5" />
          <circle id="tunnelTimerCircle" cx="50%" cy="50%" r="42%" stroke="var(--accent-color)" stroke-width="6" stroke-dasharray="790" stroke-dashoffset="0" stroke-linecap="round" fill="transparent" class="transition-all duration-1000" />
        </svg>

        <div class="absolute flex flex-col items-center justify-center">
          <span id="tunnelTimerDisplay" class="font-mono text-5xl font-light text-slate-100 tracking-wider">45:00</span>
          <span class="text-[10px] font-mono uppercase tracking-widest text-theme-textMuted mt-1" id="tunnelTimerStatus">In The Flow</span>

          <div class="flex items-center gap-3 mt-4">
            <button onclick="toggleTunnelTimer()" id="tunnelPauseBtn" class="w-11 h-11 rounded-full flex items-center justify-center text-black font-bold shadow-lg transition active:scale-95" style="background-color: var(--accent-color);">
              <i data-lucide="pause" id="tunnelPauseIcon" class="w-5 h-5"></i>
            </button>
            <button onclick="addFiveMinutes()" class="px-3 py-1.5 rounded-full bg-white/5 hover:bg-white/10 border border-theme/60 text-[11px] font-mono text-theme-textMuted hover:text-white transition">
              +5 min
            </button>
          </div>
        </div>
      </div>

      <!-- Current Steps Checklist -->
      <div class="glass-surface rounded-2xl p-4 sm:p-5 text-left space-y-3">
        <div class="flex items-center justify-between border-b border-theme/40 pb-2">
          <span class="text-xs font-mono uppercase tracking-wider text-theme-accent">Step-by-Step Flow</span>
          <span id="tunnelStepsRatio" class="text-xs font-mono text-theme-textMuted">0 / 0</span>
        </div>
        <div id="tunnelStepsList" class="space-y-2 max-h-48 overflow-y-auto pr-1">
          <!-- Dynamic Steps -->
        </div>
      </div>

    </div>

    <!-- Bottom Tunnel Complete Bar -->
    <div class="max-w-4xl w-full mx-auto pt-4 border-t border-theme/50 flex flex-col sm:flex-row items-center justify-between gap-3">
      <div class="text-xs text-theme-textMuted font-mono">
        Ambient Sound: <span id="tunnelAudioStatus" class="text-theme-accent">Mute</span>
      </div>
      <button onclick="triggerProcessCompletion()" class="px-8 py-3 rounded-2xl text-xs font-mono uppercase tracking-wider font-bold text-black transition shadow-xl flex items-center gap-2 transform active:scale-95" style="background-color: var(--accent-color); box-shadow: 0 4px 25px var(--accent-glow);">
        <i data-lucide="sparkles" class="w-4 h-4"></i>
        <span>I Finished The Steps • Claim Rewards!</span>
      </button>
    </div>

  </div>

  <!-- Rich Multi-Reward Chest Celebration Modal -->
  <div id="celebrationOverlay" class="fixed inset-0 z-50 bg-black/92 backdrop-blur-md flex items-center justify-center p-4 opacity-0 pointer-events-none transition-all duration-700">
    <canvas id="fireworksCanvas" class="absolute inset-0 pointer-events-none z-10 w-full h-full"></canvas>

    <div class="relative z-20 max-w-2xl w-full glass-surface rounded-3xl p-6 sm:p-8 text-center border border-theme shadow-2xl transform scale-90 transition-all duration-500 max-h-[92vh] overflow-y-auto" id="celebrationBox">
      
      <!-- Celebration spectacle selector tabs -->
      <div class="flex items-center justify-between border-b border-theme/40 pb-3 mb-4">
        <span class="text-[11px] font-mono uppercase text-theme-accent flex items-center gap-1.5">
          <i data-lucide="sparkles" class="w-3.5 h-3.5"></i> Celebration Spectacle:
        </span>
        <div class="flex items-center gap-1 bg-black/60 p-1 rounded-xl border border-theme/40 text-[11px]">
          <button onclick="switchCelebrationVisual('crackworks')" id="btnAnimCrackworks" class="px-2.5 py-1 rounded-lg bg-theme-accent text-black font-semibold">Fireworks</button>
          <button onclick="switchCelebrationVisual('stars')" id="btnAnimStars" class="px-2.5 py-1 rounded-lg text-theme-textMuted hover:text-white">Star Shower</button>
          <button onclick="switchCelebrationVisual('aurora')" id="btnAnimAurora" class="px-2.5 py-1 rounded-lg text-theme-textMuted hover:text-white">Zen Aurora</button>
        </div>
      </div>

      <div class="inline-block px-3 py-1 rounded-full bg-amber-500/20 text-amber-300 text-xs font-mono uppercase tracking-wider mb-2">
        🎉 Flow Session Complete!
      </div>

      <h3 class="font-serif text-3xl sm:text-4xl text-slate-100 font-medium">You Honored The Process</h3>
      <p class="text-sm text-theme-textMuted mt-1 max-w-md mx-auto">
        You didn't just rush to get it done — you stayed present with the craft. Here is your reward package:
      </p>

      <!-- REWARD 1 & 2: Dynamic Collectible Badge & Identity Card -->
      <div id="badgeRewardCard" class="my-5 p-5 rounded-2xl bg-gradient-to-br from-black/80 to-theme-surface border border-theme text-left relative overflow-hidden shadow-2xl">
        <div class="absolute -right-8 -bottom-8 w-32 h-32 rounded-full opacity-20 blur-xl" style="background-color: var(--accent-color);"></div>

        <div class="flex items-start justify-between relative z-10">
          <div class="flex items-center gap-3">
            <div id="badgeIconBox" class="w-12 h-12 rounded-2xl bg-amber-500/20 border border-amber-400/40 text-amber-300 flex items-center justify-center font-bold text-2xl">
              ⚡
            </div>
            <div>
              <span class="text-[10px] font-mono uppercase tracking-wider text-amber-400 block" id="badgeSubtitle">Collectible Identity Badge</span>
              <h4 class="font-serif text-xl text-slate-100 font-semibold" id="badgeTitle">Master of the Craft</h4>
            </div>
          </div>
          <span class="text-[10px] font-mono px-2 py-1 rounded-md bg-white/10 text-theme-textMuted" id="badgeDateText">Today</span>
        </div>

        <div class="mt-4 pt-3 border-t border-theme/40 grid grid-cols-3 gap-2 text-center relative z-10">
          <div class="p-2 rounded-xl bg-black/40 border border-theme/30">
            <span class="text-[10px] font-mono text-theme-textMuted block">Time in Flow</span>
            <span class="font-mono text-base font-bold text-theme-accent" id="badgeMinutesText">45m</span>
          </div>
          <div class="p-2 rounded-xl bg-black/40 border border-theme/30">
            <span class="text-[10px] font-mono text-theme-textMuted block">Steps Honored</span>
            <span class="font-mono text-base font-bold text-emerald-400" id="badgeStepsText">3/3</span>
          </div>
          <div class="p-2 rounded-xl bg-black/40 border border-theme/30">
            <span class="text-[10px] font-mono text-theme-textMuted block">Flow Score</span>
            <span class="font-mono text-base font-bold text-purple-400">100%</span>
          </div>
        </div>

        <div class="mt-3 flex items-center justify-between relative z-10">
          <span class="text-[11px] text-theme-textMuted italic truncate pr-2" id="badgeProcessName">"Writing session"</span>
          <button onclick="copyBadgeVictoryText()" class="px-3 py-1 rounded-lg bg-white/10 hover:bg-white/20 border border-theme/40 text-[11px] font-mono text-slate-200 transition shrink-0 flex items-center gap-1">
            <i data-lucide="copy" class="w-3 h-3"></i>
            <span id="copyBadgeBtnText">Copy Victory Card</span>
          </button>
        </div>
      </div>

      <!-- REWARD 3: Real-Life Treat to Claim Right Now -->
      <div class="my-4 p-4 rounded-2xl bg-purple-500/10 border border-purple-500/30 text-left flex items-start gap-3.5">
        <div class="w-10 h-10 rounded-xl bg-purple-500/20 text-purple-300 flex items-center justify-center shrink-0">
          <i data-lucide="gift" class="w-5 h-5"></i>
        </div>
        <div class="flex-1">
          <span class="text-[10px] font-mono uppercase tracking-wider text-purple-300 font-semibold block">Your Real-Life Brain Treat:</span>
          <p class="text-xs text-slate-200 font-medium mt-0.5" id="celebrationRealReward">
            Treat yourself to a warm cup of herbal tea or 5 minutes of sunlight stretching!
          </p>
          <span class="text-[10px] text-theme-textMuted">You gave your brain genuine focus. Give it a guilt-free treat.</span>
        </div>
      </div>

      <!-- REWARD 4: Bite-Sized Wisdom Capsule -->
      <div class="my-4 p-4 rounded-2xl bg-black/40 border border-theme/40 text-left flex items-start gap-3.5">
        <div class="w-10 h-10 rounded-xl bg-amber-500/15 text-amber-300 flex items-center justify-center shrink-0">
          <i data-lucide="quote" class="w-5 h-5"></i>
        </div>
        <div>
          <span class="text-[10px] font-mono uppercase tracking-wider text-amber-300 font-semibold block">Wisdom Capsule:</span>
          <p class="text-xs text-slate-300 italic mt-0.5" id="wisdomQuoteText">
            "We are what we repeatedly do. Excellence, then, is not an act, but a habit."
          </p>
          <span class="text-[10px] text-theme-textMuted font-mono block mt-1" id="wisdomAuthorText">— Will Durant / Aristotle</span>
        </div>
      </div>

      <button onclick="dismissCelebration()" class="w-full py-3.5 rounded-2xl text-xs font-mono uppercase tracking-wider font-bold text-black transition shadow-xl mt-2" style="background-color: var(--accent-color);">
        Store In Badge Room &amp; Return
      </button>
    </div>
  </div>

  <!-- Guilt-Free Early Pause: "Seed Planted" + Mental Bookmark -->
  <div id="seedModal" class="fixed inset-0 z-50 bg-black/92 backdrop-blur-xl flex items-center justify-center p-4 opacity-0 pointer-events-none transition-all duration-700">
    <canvas id="seedCanvas" class="absolute inset-0 pointer-events-none z-10 w-full h-full"></canvas>

    <div class="relative z-20 max-w-xl w-full glass-surface rounded-3xl p-6 sm:p-8 text-center border border-theme shadow-2xl transform scale-90 transition-all duration-500" id="seedBox">
      
      <div class="w-16 h-16 rounded-2xl border border-emerald-500/30 flex items-center justify-center mx-auto mb-4 text-emerald-300" style="background-color: rgba(52, 211, 153, 0.15);">
        <i data-lucide="sprout" class="w-8 h-8 animate-bounce"></i>
      </div>

      <div class="inline-block px-3 py-1 rounded-full bg-emerald-500/20 text-emerald-300 text-xs font-mono uppercase tracking-wider mb-2">
        🌱 Seed Planted (Rest is Part of Mastery)
      </div>

      <h3 class="font-serif text-2xl sm:text-3xl text-slate-100 font-medium">No Shame. Nothing Lost.</h3>
      <p class="text-xs sm:text-sm text-theme-textMuted mt-2 leading-relaxed">
        Stopping when your brain needs rest is smart, not weak! Every single minute you spent in the arena made you better.
      </p>

      <!-- Mental Bookmark Note (Easy explanation of Zeigarnik effect) -->
      <div class="my-5 p-4 rounded-2xl bg-black/60 border border-theme/60 text-left space-y-2.5">
        <div class="flex items-center gap-2">
          <i data-lucide="bookmark-plus" class="w-4 h-4 text-indigo-400"></i>
          <span class="text-xs font-mono uppercase tracking-wider text-slate-200">Save a 10-Second Mental Bookmark:</span>
        </div>
        <p class="text-[11px] text-theme-textMuted">
          Why it works: Jotting down where you left off frees your mind from worrying about it so you can rest peacefully.
        </p>
        <input type="text" id="inputZeigarnikNote" placeholder="Where did you leave off? (e.g., Finished draft outline; resume with section 2)" class="w-full px-3.5 py-2.5 rounded-xl bg-white/[0.04] border border-theme/60 text-xs text-slate-100 outline-none focus:border-indigo-400">
      </div>

      <div class="flex items-center gap-3">
        <button onclick="saveCleanHaltAndClose()" class="w-full py-3.5 rounded-2xl text-xs font-mono uppercase tracking-wider font-semibold text-black transition shadow-lg" style="background-color: var(--accent-color);">
          Save Bookmark &amp; Relax
        </button>
      </div>

    </div>
  </div>

  <!-- Science in Plain English Educational Modal -->
  <div id="plainEnglishModal" class="fixed inset-0 z-50 bg-black/85 backdrop-blur-md flex items-center justify-center p-4 opacity-0 pointer-events-none transition-all duration-300">
    <div class="glass-surface w-full max-w-2xl rounded-3xl p-6 sm:p-8 max-h-[90vh] overflow-y-auto transform scale-95 transition-all duration-300 border border-theme shadow-2xl" id="plainEnglishBox">
      
      <div class="flex items-center justify-between border-b border-theme/50 pb-4 mb-4">
        <div>
          <span class="text-[11px] font-mono uppercase tracking-widest text-theme-accent">Plain English Guide</span>
          <h3 class="font-serif text-2xl text-slate-100 font-medium">Why This App Works Differently</h3>
        </div>
        <button onclick="closeScienceInPlainEnglishModal()" class="p-2 rounded-xl text-theme-textMuted hover:text-white hover:bg-white/5 transition">
          <i data-lucide="x" class="w-5 h-5"></i>
        </button>
      </div>

      <div class="space-y-4 text-xs">
        <div class="p-4 rounded-2xl bg-black/40 border border-theme/40 space-y-1">
          <h4 class="font-mono text-amber-300 text-sm font-semibold flex items-center gap-2">
            <span>⚡ The Easy Kickstart (The 30-Second Rule)</span>
          </h4>
          <p class="text-slate-300 leading-relaxed">
            <strong>The Science:</strong> Starting is usually the hardest hurdle. Your brain imagines the whole project and freezes in dread.<br>
            <strong>In Plain English:</strong> You only commit to 30 seconds (like opening the notebook). Once you make that tiny physical motion, inertia vanishes and your brain naturally keeps rolling.
          </p>
        </div>

        <div class="p-4 rounded-2xl bg-black/40 border border-theme/40 space-y-1">
          <h4 class="font-mono text-sky-300 text-sm font-semibold flex items-center gap-2">
            <span>🛡️ Laser Focus Tunnel</span>
          </h4>
          <p class="text-slate-300 leading-relaxed">
            <strong>The Science:</strong> Human working memory can only juggle 3 to 4 items at once before stress levels spike.<br>
            <strong>In Plain English:</strong> During focus mode, the app hides all other tasks. You only look at the one step right in front of you. No mental clutter.
          </p>
        </div>

        <div class="p-4 rounded-2xl bg-black/40 border border-theme/40 space-y-1">
          <h4 class="font-mono text-emerald-300 text-sm font-semibold flex items-center gap-2">
            <span>🌬️ The 10-Second Calming Breath</span>
          </h4>
          <p class="text-slate-300 leading-relaxed">
            <strong>The Science:</strong> Two quick inhales through the nose followed by a long, slow exhale through the mouth resets the autonomic nervous system.<br>
            <strong>In Plain English:</strong> It acts like an instant cool-down button. Your shoulders drop, your pulse slows, and your mind feels grounded.
          </p>
        </div>

        <div class="p-4 rounded-2xl bg-black/40 border border-theme/40 space-y-1">
          <h4 class="font-mono text-indigo-300 text-sm font-semibold flex items-center gap-2">
            <span>🔖 Mental Bookmarks (Guilt-Free Early Pauses)</span>
          </h4>
          <p class="text-slate-300 leading-relaxed">
            <strong>The Science:</strong> Unfinished tasks loop in your head like an annoying background app (the Zeigarnik Effect).<br>
            <strong>In Plain English:</strong> When you stop early, jot down where you left off. Your brain feels satisfied that it's safe, allowing you to relax without lingering guilt.
          </p>
        </div>
      </div>

      <div class="mt-6 pt-4 border-t border-theme/50 text-right">
        <button onclick="closeScienceInPlainEnglishModal()" class="px-5 py-2.5 rounded-xl font-mono text-xs uppercase tracking-wide font-semibold text-black transition" style="background-color: var(--accent-color);">
          Got It!
        </button>
      </div>

    </div>
  </div>

  <script>
    // Storage keys
    const STORAGE_KEY_PROCESSES = 'praxis_processes_v3';
    const STORAGE_KEY_CHRONICLE = 'praxis_chronicle_v3';
    const STORAGE_KEY_THEME = 'praxis_theme_v3';
    const STORAGE_KEY_BADGES = 'praxis_badges_v3';

    let processes = JSON.parse(localStorage.getItem(STORAGE_KEY_PROCESSES)) || [];
    let chronicle = JSON.parse(localStorage.getItem(STORAGE_KEY_CHRONICLE)) || [];
    let badges = JSON.parse(localStorage.getItem(STORAGE_KEY_BADGES)) || [];
    let activeDashboardTab = 'active';

    // Current Session State
    let currentSession = {
      processId: null,
      secondsElapsed: 0,
      targetSeconds: 45 * 60,
      timerRunning: false,
      intervalId: null,
      audioFrequencyType: null,
      stepZeroDone: false,
      customReward: ''
    };

    // Color definitions in simple terms
    const themeRationales = {
      teal: "Ocean Teal: Soft on your eyes, eases screen strain, and slows down your breathing.",
      amber: "Candlelight Amber: Warm, cozy evening light with zero harsh blue glare so you can sleep easily.",
      forest: "Forest Green: Natural soothing greens that signal safety to your nervous system.",
      indigo: "Midnight Indigo: Clear night sky tone for quiet, late-night deep thinking."
    };

    function setTheme(themeName) {
      document.body.setAttribute('data-theme', themeName);
      localStorage.setItem(STORAGE_KEY_THEME, themeName);

      ['teal', 'amber', 'forest', 'indigo'].forEach(t => {
        const btn = document.getElementById(`btnTheme${t.charAt(0).toUpperCase() + t.slice(1)}`);
        if (btn) {
          if (t === themeName) {
            btn.className = `px-2.5 py-1 rounded-lg transition-all flex items-center gap-1.5 font-medium border border-${t}-500/50 bg-${t}-500/20 text-${t}-300`;
          } else {
            btn.className = `px-2.5 py-1 rounded-lg transition-all flex items-center gap-1.5 font-medium border border-transparent text-theme-textMuted hover:text-white`;
          }
        }
      });

      const textElem = document.getElementById('rationaleText');
      if (textElem && themeRationales[themeName]) {
        textElem.innerText = themeRationales[themeName];
      }
    }

    let webAudioContext = null;
    let masterGain = null;
    let currentOscillators = [];
    let noiseNode = null;

    function initWebAudio() {
      if (!webAudioContext) {
        const AudioContextClass = window.AudioContext || window.webkitAudioContext;
        webAudioContext = new AudioContextClass();
        masterGain = webAudioContext.createGain();
        masterGain.gain.setValueAtTime(0.001, webAudioContext.currentTime);
        masterGain.connect(webAudioContext.destination);
      }
      if (webAudioContext.state === 'suspended') {
        webAudioContext.resume();
      }
    }

    function stopAudioEngine() {
      if (masterGain && webAudioContext) {
        masterGain.gain.linearRampToValueAtTime(0.0001, webAudioContext.currentTime + 0.4);
      }
      currentOscillators.forEach(osc => {
        try { osc.stop(webAudioContext.currentTime + 0.5); } catch(e){}
      });
      currentOscillators = [];
      if (noiseNode) {
        try { noiseNode.stop(webAudioContext.currentTime + 0.5); } catch(e){}
        noiseNode = null;
      }
      document.getElementById('soundLabel').innerText = 'Calm Sounds: Off';
      document.getElementById('tunnelAudioStatus').innerText = 'Mute';
      currentSession.audioFrequencyType = null;
    }

    function setAudioFrequency(type) {
      initWebAudio();
      stopAudioEngine();

      currentSession.audioFrequencyType = type;
      masterGain.gain.cancelScheduledValues(webAudioContext.currentTime);
      masterGain.gain.setValueAtTime(0.001, webAudioContext.currentTime);
      masterGain.gain.linearRampToValueAtTime(0.12, webAudioContext.currentTime + 1.2);

      if (type === 'gamma') {
        createBinauralOscillators(200, 240);
        document.getElementById('soundLabel').innerText = '40Hz Focus Wave';
        document.getElementById('tunnelAudioStatus').innerText = '40Hz Deep Focus Active';
      } else if (type === 'alpha') {
        createBinauralOscillators(210, 220);
        document.getElementById('soundLabel').innerText = '10Hz Calm Flow';
        document.getElementById('tunnelAudioStatus').innerText = '10Hz Calm Flow Active';
      } else if (type === 'brown') {
        createBrownNoise();
        document.getElementById('soundLabel').innerText = 'Warm Rain Noise';
        document.getElementById('tunnelAudioStatus').innerText = 'Warm Rain Active';
      }
      lucide.createIcons();
    }

    function createBinauralOscillators(freqLeft, freqRight) {
      const merger = webAudioContext.createChannelMerger(2);
      const oscL = webAudioContext.createOscillator();
      const oscR = webAudioContext.createOscillator();
      
      oscL.type = 'sine';
      oscL.frequency.setValueAtTime(freqLeft, webAudioContext.currentTime);
      oscR.type = 'sine';
      oscR.frequency.setValueAtTime(freqRight, webAudioContext.currentTime);

      oscL.connect(merger, 0, 0);
      oscR.connect(merger, 0, 1);
      merger.connect(masterGain);

      oscL.start();
      oscR.start();
      currentOscillators.push(oscL, oscR);
    }

    function createBrownNoise() {
      const bufferSize = webAudioContext.sampleRate * 2;
      const noiseBuffer = webAudioContext.createBuffer(1, bufferSize, webAudioContext.sampleRate);
      const output = noiseBuffer.getChannelData(0);
      let lastOut = 0.0;

      for (let i = 0; i < bufferSize; i++) {
        const white = Math.random() * 2 - 1;
        output[i] = (lastOut + (0.02 * white)) / 1.02;
        lastOut = output[i];
        output[i] *= 3.5;
      }

      noiseNode = webAudioContext.createBufferSource();
      noiseNode.buffer = noiseBuffer;
      noiseNode.loop = true;
      
      const filter = webAudioContext.createBiquadFilter();
      filter.type = 'lowpass';
      filter.frequency.setValueAtTime(320, webAudioContext.currentTime);

      noiseNode.connect(filter);
      filter.connect(masterGain);
      noiseNode.start();
    }

    function toggleSoundEngine() {
      if (currentSession.audioFrequencyType) {
        stopAudioEngine();
      } else {
        setAudioFrequency('brown');
      }
    }

    function playCelebrationChime() {
      try {
        initWebAudio();
        const now = webAudioContext.currentTime;
        const chimeGain = webAudioContext.createGain();
        chimeGain.gain.setValueAtTime(0.18, now);
        chimeGain.gain.exponentialRampToValueAtTime(0.0001, now + 2.5);
        chimeGain.connect(webAudioContext.destination);

        const chord = [523.25, 659.25, 783.99, 1046.50];
        chord.forEach((freq, idx) => {
          const osc = webAudioContext.createOscillator();
          osc.type = 'sine';
          osc.frequency.setValueAtTime(freq, now + idx * 0.08);
          osc.connect(chimeGain);
          osc.start(now + idx * 0.08);
          osc.stop(now + 2.4);
        });
      } catch(e) {}
    }

    const frictionTips = {
      ambiguity: "Tip: Just define a tiny 30-second action like 'Open blank file 1'.",
      fear: "Tip: Give yourself permission to make a messy first draft that nobody sees.",
      boredom: "Tip: Put on headphones and challenge yourself to a light 15-minute sprint.",
      fatigue: "Tip: Keep the session to 15m and plan a relaxing break right after."
    };

    function updateFrictionTip() {
      const val = document.getElementById('inputFriction').value;
      document.getElementById('frictionTip').innerText = frictionTips[val] || frictionTips.ambiguity;
    }

    function applyDurationPreset() {
      const preset = document.getElementById('inputDurationPreset').value;
      const valInp = document.getElementById('inputDurationVal');
      if (preset !== 'custom') {
        valInp.value = preset;
      }
    }

    let modalStepCount = 0;
    function addModalStepRow(defaultText = '') {
      modalStepCount++;
      const container = document.getElementById('modalStepList');
      const div = document.createElement('div');
      div.id = `modal-step-row-${modalStepCount}`;
      div.className = 'flex items-center gap-2';
      div.innerHTML = `
        <span class="text-xs font-mono text-theme-textMuted w-4">${container.children.length + 1}.</span>
        <input type="text" value="${defaultText.replace(/"/g, '&quot;')}" required placeholder="Micro-step in the journey..." class="flex-1 px-3 py-2 rounded-xl bg-black/60 border border-theme/60 text-xs text-slate-200 outline-none">
        <button type="button" onclick="removeModalStepRow('${div.id}')" class="p-1.5 text-theme-textMuted hover:text-rose-400 transition">
          <i data-lucide="trash-2" class="w-4 h-4"></i>
        </button>
      `;
      container.appendChild(div);
      lucide.createIcons();
    }

    function removeModalStepRow(id) {
      const elem = document.getElementById(id);
      if (elem) elem.remove();
    }

    function openCreateModal() {
      const modal = document.getElementById('createModal');
      const box = document.getElementById('createModalBox');
      document.getElementById('createProcessForm').reset();
      
      const container = document.getElementById('modalStepList');
      container.innerHTML = '';
      addModalStepRow('Silence notifications & put water on desk');
      addModalStepRow('Focus comfortably without judging yourself');
      addModalStepRow('Wrap up and leave a friendly note for tomorrow');

      modal.classList.remove('opacity-0', 'pointer-events-none');
      box.classList.remove('scale-95');
      box.classList.add('scale-100');
      lucide.createIcons();
    }

    function closeCreateModal() {
      const modal = document.getElementById('createModal');
      const box = document.getElementById('createModalBox');
      modal.classList.add('opacity-0', 'pointer-events-none');
      box.classList.add('scale-95');
      box.classList.remove('scale-100');
    }

    function loadTemplate(tpl) {
      openCreateModal();
      const intention = document.getElementById('inputIntention');
      const why = document.getElementById('inputWhy');
      const friction = document.getElementById('inputFriction');
      const stepZero = document.getElementById('inputStepZero');
      const durationVal = document.getElementById('inputDurationVal');
      const horizon = document.getElementById('inputHorizon');
      const customReward = document.getElementById('inputCustomReward');
      const container = document.getElementById('modalStepList');
      container.innerHTML = '';

      if (tpl === 'writing') {
        intention.value = "Draft thoughts freely without pressing backspace";
        why.value = "To give shape to my thoughts and write without self-criticism.";
        friction.value = "fear";
        stepZero.value = "Open blank page and type 1 unpolished sentence";
        durationVal.value = 25;
        horizon.value = "Morning Fresh Flow";
        customReward.value = "Enjoy a fresh cup of tea by the window";
        addModalStepRow("Put phone on silent in another room");
        addModalStepRow("Write without stopping for 20 minutes");
        addModalStepRow("Highlight 2 lines you genuinely enjoyed writing");
      } else if (tpl === 'coding') {
        intention.value = "Clean up project code and write tests";
        why.value = "To make things clean, elegant, and stress-free for future me.";
        friction.value = "ambiguity";
        stepZero.value = "Sketch the data flow on scrap paper with a pen";
        durationVal.value = 45;
        horizon.value = "Afternoon Flow Block";
        customReward.value = "10 minutes of relaxing sunlight walking";
        addModalStepRow("Write input and outputs on paper");
        addModalStepRow("Write the logic slowly with deep breathing");
        addModalStepRow("Run tests and celebrate the green checkmarks");
      } else if (tpl === 'reading') {
        intention.value = "Read 1 chapter with calm curiosity";
        why.value = "To relax, expand my perspective, and enjoy quiet ideas.";
        friction.value = "boredom";
        stepZero.value = "Open the book and read the first paragraph out loud";
        durationVal.value = 20;
        horizon.value = "Evening Quiet Time";
        customReward.value = "A square of dark chocolate";
        addModalStepRow("Find a comfortable seat with good lighting");
        addModalStepRow("Read without checking any screens");
        addModalStepRow("Jot down 1 memorable idea in your notes");
      }
      updateFrictionTip();
    }

    function handleCreateProcess(e) {
      e.preventDefault();
      const intention = document.getElementById('inputIntention').value.trim();
      const why = document.getElementById('inputWhy').value.trim();
      const friction = document.getElementById('inputFriction').value;
      const stepZero = document.getElementById('inputStepZero').value.trim();
      const duration = parseInt(document.getElementById('inputDurationVal').value, 10) || 45;
      const horizon = document.getElementById('inputHorizon').value.trim() || 'Flexible Window';
      const customReward = document.getElementById('inputCustomReward').value.trim();

      const stepInputs = document.querySelectorAll('#modalStepList input');
      const steps = [];
      stepInputs.forEach((inp, idx) => {
        if (inp.value.trim()) {
          steps.push({
            id: `step-${Date.now()}-${idx}`,
            text: inp.value.trim(),
            done: false
          });
        }
      });

      const newProcess = {
        id: `process-${Date.now()}`,
        intention,
        why,
        friction,
        stepZero,
        duration,
        horizon,
        customReward,
        steps,
        createdAt: Date.now()
      };

      processes.unshift(newProcess);
      saveProcesses();
      closeCreateModal();
      renderDashboard();
    }

    function saveProcesses() {
      localStorage.setItem(STORAGE_KEY_PROCESSES, JSON.stringify(processes));
      updateMetricsDashboard();
    }

    function saveChronicle() {
      localStorage.setItem(STORAGE_KEY_CHRONICLE, JSON.stringify(chronicle));
      updateMetricsDashboard();
    }

    function saveBadges() {
      localStorage.setItem(STORAGE_KEY_BADGES, JSON.stringify(badges));
      updateMetricsDashboard();
    }

    let sighTimerId = null;
    let pendingProcessId = null;

    function initiateProcessSession(processId) {
      pendingProcessId = processId;
      const p = processes.find(item => item.id === processId);
      if (!p) return;

      const modal = document.getElementById('somaticModal');
      modal.classList.remove('opacity-0', 'pointer-events-none');
      runSighAnimationLoop();
      lucide.createIcons();
    }

    function runSighAnimationLoop() {
      const phaseElem = document.getElementById('breathPhaseText');
      const countElem = document.getElementById('breathCountdown');
      let second = 0;

      clearInterval(sighTimerId);
      sighTimerId = setInterval(() => {
        second = (second + 1) % 7;
        countElem.innerText = 7 - second;

        if (second <= 2) {
          phaseElem.innerText = "Inhale 1: Breathe in through nose...";
          phaseElem.style.color = "var(--accent-color)";
        } else if (second === 3) {
          phaseElem.innerText = "Inhale 2: Quick extra sniff...";
          phaseElem.style.color = "#38bdf8";
        } else {
          phaseElem.innerText = "Long exhale through mouth...";
          phaseElem.style.color = "#a7f3d0";
        }
      }, 1000);
    }

    function skipSomaticGate() {
      clearInterval(sighTimerId);
      document.getElementById('somaticModal').classList.add('opacity-0', 'pointer-events-none');
      launchFlowTunnel(pendingProcessId);
    }

    function enterFlowTunnelNow() {
      clearInterval(sighTimerId);
      document.getElementById('somaticModal').classList.add('opacity-0', 'pointer-events-none');
      launchFlowTunnel(pendingProcessId);
    }

    function launchFlowTunnel(processId) {
      const process = processes.find(p => p.id === processId);
      if (!process) return;

      currentSession.processId = processId;
      currentSession.secondsElapsed = 0;
      currentSession.targetSeconds = (process.duration || 45) * 60;
      currentSession.timerRunning = true;
      currentSession.stepZeroDone = false;
      currentSession.customReward = process.customReward || '';

      document.getElementById('tunnelIntentionTitle').innerText = process.intention;
      document.getElementById('tunnelWhyText').innerText = `"${process.why}"`;
      document.getElementById('tunnelStepZeroText').innerText = process.stepZero;
      document.getElementById('tunnelStepZeroBanner').classList.remove('hidden');

      renderTunnelSteps(process);
      updateTunnelTimerDisplay();

      clearInterval(currentSession.intervalId);
      currentSession.intervalId = setInterval(() => {
        if (currentSession.timerRunning) {
          currentSession.secondsElapsed++;
          updateTunnelTimerDisplay();
        }
      }, 1000);

      const tunnel = document.getElementById('flowTunnelOverlay');
      tunnel.classList.remove('opacity-0', 'pointer-events-none');
      lucide.createIcons();
    }

    function dismissStepZero() {
      currentSession.stepZeroDone = true;
      document.getElementById('tunnelStepZeroBanner').classList.add('hidden');
      sparkleMicroCelebration();
    }

    function toggleTunnelTimer() {
      currentSession.timerRunning = !currentSession.timerRunning;
      const icon = document.getElementById('tunnelPauseIcon');
      const status = document.getElementById('tunnelTimerStatus');
      if (currentSession.timerRunning) {
        icon.setAttribute('data-lucide', 'pause');
        status.innerText = 'In The Flow';
      } else {
        icon.setAttribute('data-lucide', 'play');
        status.innerText = 'Paused';
      }
      lucide.createIcons();
    }

    function addFiveMinutes() {
      currentSession.targetSeconds += 5 * 60;
      updateTunnelTimerDisplay();
    }

    function updateTunnelTimerDisplay() {
      const remaining = Math.max(0, currentSession.targetSeconds - currentSession.secondsElapsed);
      const mins = Math.floor(remaining / 60);
      const secs = remaining % 60;
      document.getElementById('tunnelTimerDisplay').innerText = 
        `${String(mins).padStart(2, '0')}:${String(secs).padStart(2, '0')}`;

      const circle = document.getElementById('tunnelTimerCircle');
      const totalCircumference = 790;
      const progressFraction = Math.min(1, currentSession.secondsElapsed / currentSession.targetSeconds);
      circle.style.strokeDashoffset = totalCircumference * (1 - progressFraction);
    }

    function renderTunnelSteps(process) {
      const container = document.getElementById('tunnelStepsList');
      container.innerHTML = '';
      
      let doneCount = 0;
      process.steps.forEach((step, idx) => {
        if (step.done) doneCount++;
        const div = document.createElement('div');
        div.className = `p-3 rounded-xl border transition-all flex items-center justify-between cursor-pointer ${
          step.done ? 'bg-emerald-500/10 border-emerald-500/30 text-emerald-200' : 'bg-black/40 border-theme/50 text-slate-300 hover:border-theme-accent'
        }`;
        div.onclick = () => toggleTunnelStep(process.id, idx);
        div.innerHTML = `
          <div class="flex items-center gap-3">
            <div class="w-5 h-5 rounded-lg border flex items-center justify-center ${step.done ? 'bg-emerald-500 border-emerald-400 text-black' : 'border-theme/60'}">
              ${step.done ? '<i data-lucide="check" class="w-3.5 h-3.5 stroke-[3]"></i>' : ''}
            </div>
            <span class="text-xs sm:text-sm ${step.done ? 'line-through opacity-70' : ''}">${step.text}</span>
          </div>
          <span class="text-[10px] font-mono uppercase px-2 py-0.5 rounded bg-white/5 text-theme-textMuted">Step ${idx + 1}</span>
        `;
        container.appendChild(div);
      });

      document.getElementById('tunnelStepsRatio').innerText = `${doneCount} / ${process.steps.length} Steps`;
      lucide.createIcons();
    }

    function toggleTunnelStep(processId, stepIdx) {
      const p = processes.find(item => item.id === processId);
      if (!p) return;
      p.steps[stepIdx].done = !p.steps[stepIdx].done;
      saveProcesses();
      renderTunnelSteps(p);
      if (p.steps[stepIdx].done) {
        sparkleMicroCelebration();
      }
    }

    const collectibleBadgesCatalog = [
      { title: "Master of the Craft", subtitle: "Patient & Deliberate", icon: "💎", desc: "Honored every micro-step without rushing." },
      { title: "Friction Slayer", subtitle: "Overcame Hesitation", icon: "⚔️", desc: "Beat the initial dread with the 30-Second Kickstart." },
      { title: "Deep Diver", subtitle: "Unbroken Immersion", icon: "🌊", desc: "Stayed in high-quality focus without task switching." },
      { title: "Steady Hand", subtitle: "Process Over Perfection", icon: "🛡️", desc: "Focused on presence rather than judging the result." },
      { title: "Quiet Force", subtitle: "Gentle Consistency", icon: "🌱", desc: "Showed up and cast an unmistakable identity vote." }
    ];

    const wisdomCapsulesCatalog = [
      { quote: "We are what we repeatedly do. Excellence, then, is not an act, but a habit.", author: "Will Durant" },
      { quote: "Do not spoil what you have by desiring what you have not; remember that what you now have was once among the things you only hoped for.", author: "Epicurus" },
      { quote: "The secret to getting ahead is getting started.", author: "Mark Twain" },
      { quote: "Nature does not hurry, yet everything is accomplished.", author: "Lao Tzu" },
      { quote: "Small deeds done are better than great deeds planned.", author: "Peter Marshall" }
    ];

    const fallbackRealRewards = [
      "Treat yourself to a warm cup of herbal tea or coffee.",
      "Step outside for 5 minutes of sunlight and deep breathing.",
      "Listen to your favorite song with your eyes closed.",
      "Enjoy a square of dark chocolate slowly.",
      "Take 5 unhurried minutes to stretch your back and arms."
    ];

    let celebrationVisualType = 'crackworks';
    let celebrationAnimId = null;
    let lastUnlockedBadge = null;

    function triggerProcessCompletion() {
      clearInterval(currentSession.intervalId);
      const process = processes.find(p => p.id === currentSession.processId);
      const minutesSpent = Math.max(1, Math.round(currentSession.secondsElapsed / 60));
      const totalSteps = process ? process.steps.length : 1;
      const completedSteps = process ? process.steps.filter(s => s.done).length : 1;

      // Select Badge & Wisdom
      const randomBadge = collectibleBadgesCatalog[Math.floor(Math.random() * collectibleBadgesCatalog.length)];
      const randomWisdom = wisdomCapsulesCatalog[Math.floor(Math.random() * wisdomCapsulesCatalog.length)];
      const rewardText = (currentSession.customReward && currentSession.customReward.trim().length > 0)
        ? currentSession.customReward
        : fallbackRealRewards[Math.floor(Math.random() * fallbackRealRewards.length)];

      const newBadge = {
        id: `badge-${Date.now()}`,
        title: randomBadge.title,
        subtitle: randomBadge.subtitle,
        icon: randomBadge.icon,
        desc: randomBadge.desc,
        processName: process ? process.intention : 'Focused Flow',
        minutes: minutesSpent,
        stepsRatio: `${completedSteps}/${totalSteps}`,
        timestamp: Date.now()
      };

      badges.unshift(newBadge);
      saveBadges();
      lastUnlockedBadge = newBadge;

      // Save Chronicle
      chronicle.unshift({
        id: `chronicle-${Date.now()}`,
        intention: process ? process.intention : 'Mindful Practice',
        why: process ? process.why : '',
        duration: minutesSpent,
        type: 'completion',
        note: `Completed session: earned '${newBadge.title}' badge.`,
        timestamp: Date.now()
      });
      saveChronicle();

      // Close Tunnel
      document.getElementById('flowTunnelOverlay').classList.add('opacity-0', 'pointer-events-none');

      // Populate Reward Chest Modal
      document.getElementById('badgeTitle').innerText = newBadge.title;
      document.getElementById('badgeSubtitle').innerText = newBadge.subtitle;
      document.getElementById('badgeIconBox').innerText = newBadge.icon;
      document.getElementById('badgeMinutesText').innerText = `${minutesSpent}m`;
      document.getElementById('badgeStepsText').innerText = `${completedSteps}/${totalSteps}`;
      document.getElementById('badgeProcessName').innerText = `"${newBadge.processName}"`;
      document.getElementById('badgeDateText').innerText = new Date().toLocaleDateString();

      document.getElementById('celebrationRealReward').innerText = rewardText;
      document.getElementById('wisdomQuoteText').innerText = `"${randomWisdom.quote}"`;
      document.getElementById('wisdomAuthorText').innerText = `— ${randomWisdom.author}`;
      document.getElementById('copyBadgeBtnText').innerText = 'Copy Victory Card';

      // Open celebration modal
      const overlay = document.getElementById('celebrationOverlay');
      const box = document.getElementById('celebrationBox');
      overlay.classList.remove('opacity-0', 'pointer-events-none');
      box.classList.remove('scale-90');
      box.classList.add('scale-100');

      playCelebrationChime();
      startCelebrationCanvasEngine(celebrationVisualType);
      lucide.createIcons();
    }

    function switchCelebrationVisual(type) {
      celebrationVisualType = type;
      ['crackworks', 'stars', 'aurora'].forEach(t => {
        const btn = document.getElementById(`btnAnim${t.charAt(0).toUpperCase() + t.slice(1)}`);
        if (btn) {
          if (t === type) {
            btn.className = 'px-2.5 py-1 rounded-lg bg-theme-accent text-black font-semibold';
          } else {
            btn.className = 'px-2.5 py-1 rounded-lg text-theme-textMuted hover:text-white';
          }
        }
      });
      cancelAnimationFrame(celebrationAnimId);
      startCelebrationCanvasEngine(type);
    }

    function dismissCelebration() {
      cancelAnimationFrame(celebrationAnimId);
      const overlay = document.getElementById('celebrationOverlay');
      const box = document.getElementById('celebrationBox');
      overlay.classList.add('opacity-0', 'pointer-events-none');
      box.classList.add('scale-90');
      box.classList.remove('scale-100');
      renderDashboard();
    }

    function copyBadgeVictoryText() {
      if (!lastUnlockedBadge) return;
      const text = `🏆 PRAXIS Victory Card!\n` +
        `Badge: ${lastUnlockedBadge.icon} ${lastUnlockedBadge.title} (${lastUnlockedBadge.subtitle})\n` +
        `Process: "${lastUnlockedBadge.processName}"\n` +
        `Time in Flow: ${lastUnlockedBadge.minutes} minutes\n` +
        `Steps Honored: ${lastUnlockedBadge.stepsRatio}\n` +
        `"Excellence is not an act, but a habit."`;

      const tempInp = document.createElement('textarea');
      tempInp.value = text;
      document.body.appendChild(tempInp);
      tempInp.select();
      document.execCommand('copy');
      document.body.removeChild(tempInp);

      document.getElementById('copyBadgeBtnText').innerText = 'Copied to Clipboard!';
      setTimeout(() => {
        const btn = document.getElementById('copyBadgeBtnText');
        if (btn) btn.innerText = 'Copy Victory Card';
      }, 2500);
    }

    function startCelebrationCanvasEngine(type) {
      const canvas = document.getElementById('fireworksCanvas');
      const ctx = canvas.getContext('2d');
      canvas.width = window.innerWidth;
      canvas.height = window.innerHeight;

      let particles = [];
      let frame = 0;

      if (type === 'crackworks') {
        const colors = ['#2dd4bf', '#f59e0b', '#34d399', '#818cf8', '#f43f5e', '#fbbf24', '#ffffff'];
        function burst(x, y) {
          for (let i = 0; i < 70; i++) {
            const angle = Math.random() * Math.PI * 2;
            const speed = Math.random() * 8 + 2;
            particles.push({
              x, y,
              vx: Math.cos(angle) * speed,
              vy: Math.sin(angle) * speed,
              color: colors[Math.floor(Math.random() * colors.length)],
              radius: Math.random() * 2.5 + 1.2,
              alpha: 1,
              decay: Math.random() * 0.018 + 0.012
            });
          }
        }
        burst(canvas.width * 0.3, canvas.height * 0.4);
        burst(canvas.width * 0.7, canvas.height * 0.35);

        function drawCrackworks() {
          ctx.fillStyle = 'rgba(0, 0, 0, 0.18)';
          ctx.fillRect(0, 0, canvas.width, canvas.height);
          frame++;
          if (frame % 35 === 0) {
            burst(Math.random() * canvas.width * 0.8 + canvas.width * 0.1, Math.random() * canvas.height * 0.5 + 80);
          }
          for (let i = particles.length - 1; i >= 0; i--) {
            const p = particles[i];
            ctx.save();
            ctx.globalAlpha = p.alpha;
            ctx.fillStyle = p.color;
            ctx.beginPath();
            ctx.arc(p.x, p.y, p.radius, 0, Math.PI * 2);
            ctx.fill();
            ctx.restore();
            p.x += p.vx;
            p.y += p.vy;
            p.vy += 0.08;
            p.vx *= 0.985;
            p.alpha -= p.decay;
            if (p.alpha <= 0) particles.splice(i, 1);
          }
          celebrationAnimId = requestAnimationFrame(drawCrackworks);
        }
        drawCrackworks();

      } else if (type === 'stars') {
        for (let i = 0; i < 90; i++) {
          particles.push({
            x: Math.random() * canvas.width,
            y: Math.random() * canvas.height,
            length: Math.random() * 12 + 6,
            speed: Math.random() * 5 + 3,
            alpha: Math.random() * 0.8 + 0.2
          });
        }
        function drawStars() {
          ctx.fillStyle = 'rgba(0, 0, 0, 0.2)';
          ctx.fillRect(0, 0, canvas.width, canvas.height);
          particles.forEach(s => {
            ctx.save();
            ctx.strokeStyle = '#fbbf24';
            ctx.lineWidth = 1.5;
            ctx.globalAlpha = s.alpha;
            ctx.beginPath();
            ctx.moveTo(s.x, s.y);
            ctx.lineTo(s.x - s.length, s.y + s.length);
            ctx.stroke();
            ctx.restore();
            s.x -= s.speed;
            s.y += s.speed;
            if (s.x < 0 || s.y > canvas.height) {
              s.x = Math.random() * canvas.width + canvas.width * 0.2;
              s.y = -10;
            }
          });
          celebrationAnimId = requestAnimationFrame(drawStars);
        }
        drawStars();

      } else if (type === 'aurora') {
        let angle = 0;
        function drawAurora() {
          ctx.fillStyle = 'rgba(0, 0, 0, 0.12)';
          ctx.fillRect(0, 0, canvas.width, canvas.height);
          angle += 0.02;
          const gradient = ctx.createLinearGradient(0, 0, canvas.width, canvas.height);
          gradient.addColorStop(0, 'rgba(45, 212, 191, 0.25)');
          gradient.addColorStop(0.5, 'rgba(129, 140, 248, 0.25)');
          gradient.addColorStop(1, 'rgba(52, 211, 153, 0.25)');

          ctx.fillStyle = gradient;
          ctx.beginPath();
          ctx.moveTo(0, canvas.height * 0.4 + Math.sin(angle) * 40);
          for (let x = 0; x < canvas.width; x += 30) {
            const y = canvas.height * 0.4 + Math.sin(angle + x * 0.005) * 50;
            ctx.lineTo(x, y);
          }
          ctx.lineTo(canvas.width, canvas.height);
          ctx.lineTo(0, canvas.height);
          ctx.closePath();
          ctx.fill();

          celebrationAnimId = requestAnimationFrame(drawAurora);
        }
        drawAurora();
      }
    }

    let seedAnimId = null;

    function promptHaltEarly() {
      clearInterval(currentSession.intervalId);
      document.getElementById('flowTunnelOverlay').classList.add('opacity-0', 'pointer-events-none');

      const modal = document.getElementById('seedModal');
      const box = document.getElementById('seedBox');
      document.getElementById('inputZeigarnikNote').value = '';

      modal.classList.remove('opacity-0', 'pointer-events-none');
      box.classList.remove('scale-90');
      box.classList.add('scale-100');

      startBotanicalSeedCanvas();
      lucide.createIcons();
    }

    function startBotanicalSeedCanvas() {
      const canvas = document.getElementById('seedCanvas');
      const ctx = canvas.getContext('2d');
      canvas.width = window.innerWidth;
      canvas.height = window.innerHeight;

      const seeds = [];
      for (let i = 0; i < 50; i++) {
        seeds.push({
          x: Math.random() * canvas.width,
          y: Math.random() * canvas.height,
          radius: Math.random() * 2.5 + 1.5,
          speedY: Math.random() * 0.8 + 0.3,
          speedX: (Math.random() - 0.5) * 0.6,
          opacity: Math.random() * 0.7 + 0.2
        });
      }

      function draw() {
        ctx.clearRect(0, 0, canvas.width, canvas.height);

        seeds.forEach(s => {
          ctx.save();
          ctx.globalAlpha = s.opacity;
          ctx.fillStyle = '#6ee7b7';
          ctx.strokeStyle = '#34d399';
          ctx.lineWidth = 1;

          ctx.beginPath();
          ctx.arc(s.x, s.y, s.radius, 0, Math.PI * 2);
          ctx.fill();

          ctx.beginPath();
          ctx.moveTo(s.x, s.y);
          ctx.lineTo(s.x - 4, s.y - 8);
          ctx.moveTo(s.x, s.y);
          ctx.lineTo(s.x + 4, s.y - 8);
          ctx.stroke();

          ctx.restore();

          s.y -= s.speedY;
          s.x += s.speedX;

          if (s.y < -20) {
            s.y = canvas.height + 20;
            s.x = Math.random() * canvas.width;
          }
        });

        seedAnimId = requestAnimationFrame(draw);
      }
      draw();
    }

    function saveCleanHaltAndClose() {
      const process = processes.find(p => p.id === currentSession.processId);
      const minutesSpent = Math.max(1, Math.round(currentSession.secondsElapsed / 60));
      const note = document.getElementById('inputZeigarnikNote').value.trim() || 'Preserved stamina. Seed resting peacefully.';

      chronicle.unshift({
        id: `chronicle-${Date.now()}`,
        intention: process ? process.intention : 'Exploration',
        why: process ? process.why : '',
        duration: minutesSpent,
        type: 'seed',
        note: note,
        timestamp: Date.now()
      });
      saveChronicle();

      cancelAnimationFrame(seedAnimId);
      const modal = document.getElementById('seedModal');
      const box = document.getElementById('seedBox');
      modal.classList.add('opacity-0', 'pointer-events-none');
      box.classList.add('scale-90');
      box.classList.remove('scale-100');

      renderDashboard();
    }

    function sparkleMicroCelebration() {
      try {
        initWebAudio();
        const now = webAudioContext.currentTime;
        const osc = webAudioContext.createOscillator();
        const g = webAudioContext.createGain();
        osc.frequency.setValueAtTime(880, now);
        osc.frequency.exponentialRampToValueAtTime(1320, now + 0.12);
        g.gain.setValueAtTime(0.08, now);
        g.gain.linearRampToValueAtTime(0.0001, now + 0.2);
        osc.connect(g);
        g.connect(webAudioContext.destination);
        osc.start(now);
        osc.stop(now + 0.22);
      } catch(e) {}
    }

    function setDashboardTab(tab) {
      activeDashboardTab = tab;
      
      const btnActive = document.getElementById('tabActiveBtn');
      const btnBookmarks = document.getElementById('tabBookmarksBtn');
      const btnChronicle = document.getElementById('tabChronicleBtn');

      const gridActive = document.getElementById('activeProcessesGrid');
      const viewBookmarks = document.getElementById('bookmarksView');
      const viewChronicle = document.getElementById('chronicleView');

      [btnActive, btnBookmarks, btnChronicle].forEach(b => {
        b.className = 'px-4 py-2 rounded-xl font-medium text-theme-textMuted hover:text-white transition-all';
      });

      gridActive.classList.add('hidden');
      viewBookmarks.classList.add('hidden');
      viewChronicle.classList.add('hidden');

      if (tab === 'active') {
        btnActive.className = 'px-4 py-2 rounded-xl font-medium transition-all bg-white/10 text-theme-accent border border-theme';
        gridActive.classList.remove('hidden');
      } else if (tab === 'bookmarks') {
        btnBookmarks.className = 'px-4 py-2 rounded-xl font-medium transition-all bg-white/10 text-emerald-300 border border-theme';
        viewBookmarks.classList.remove('hidden');
      } else {
        btnChronicle.className = 'px-4 py-2 rounded-xl font-medium transition-all bg-white/10 text-amber-300 border border-theme';
        viewChronicle.classList.remove('hidden');
      }

      renderDashboard();
    }

    function deleteProcess(id, e) {
      e.stopPropagation();
      processes = processes.filter(p => p.id !== id);
      saveProcesses();
      renderDashboard();
    }

    function toggleStepDirect(procId, stepIdx, e) {
      e.stopPropagation();
      const p = processes.find(item => item.id === procId);
      if (!p) return;
      p.steps[stepIdx].done = !p.steps[stepIdx].done;
      saveProcesses();
      if (p.steps[stepIdx].done) {
        sparkleMicroCelebration();
      }
      renderDashboard();
    }

    function renderDashboard() {
      const grid = document.getElementById('activeProcessesGrid');
      const bookmarksView = document.getElementById('bookmarksView');
      const chronicleView = document.getElementById('chronicleView');

      const seedsCount = chronicle.filter(c => c.type === 'seed').length;
      document.getElementById('activeCountBadge').innerText = processes.length;
      document.getElementById('bookmarksCountBadge').innerText = seedsCount;
      document.getElementById('trophyCountBadge').innerText = badges.length;

      // Active Grid
      if (processes.length === 0) {
        grid.innerHTML = `
          <div class="col-span-full glass-surface rounded-3xl p-12 text-center">
            <div class="w-14 h-14 rounded-2xl bg-white/[0.03] border border-theme flex items-center justify-center mx-auto mb-3 text-theme-accent">
              <i data-lucide="compass" class="w-7 h-7"></i>
            </div>
            <h3 class="font-serif text-xl text-slate-100 font-medium">Your Mindful Space is Clear</h3>
            <p class="text-xs text-theme-textMuted max-w-sm mx-auto mt-1 mb-5">Create a task with a gentle 30-second kickstart so you never feel intimidated by starting.</p>
            <button onclick="openCreateModal()" class="px-5 py-2.5 rounded-xl font-mono text-xs uppercase tracking-wide font-semibold text-black transition" style="background-color: var(--accent-color);">
              Create First Process
            </button>
          </div>
        `;
      } else {
        grid.innerHTML = processes.map(p => {
          const completedSteps = p.steps.filter(s => s.done).length;
          const totalSteps = p.steps.length;
          const pct = totalSteps > 0 ? Math.round((completedSteps / totalSteps) * 100) : 0;

          return `
            <div class="glass-surface rounded-3xl p-5 sm:p-6 transition-all duration-300 flex flex-col justify-between group relative border border-theme">
              <div>
                <div class="flex items-center justify-between gap-2 mb-3">
                  <span class="px-2.5 py-1 rounded-lg bg-white/5 border border-theme text-[10px] font-mono uppercase tracking-wider text-theme-accent">
                    ${p.horizon || 'Flexible Window'}
                  </span>
                  <div class="flex items-center gap-1.5">
                    <span class="text-[11px] font-mono text-theme-textMuted flex items-center gap-1">
                      <i data-lucide="clock" class="w-3 h-3 text-theme-accent"></i> ${p.duration}m
                    </span>
                    <button onclick="deleteProcess('${p.id}', event)" class="opacity-0 group-hover:opacity-100 p-1.5 rounded-lg text-theme-textMuted hover:text-rose-400 hover:bg-white/5 transition" title="Delete Task">
                      <i data-lucide="trash-2" class="w-3.5 h-3.5"></i>
                    </button>
                  </div>
                </div>

                <h3 class="font-serif text-lg font-medium text-slate-100 group-hover:text-theme-accent transition">
                  ${p.intention}
                </h3>

                <div class="mt-2.5 p-3 rounded-2xl bg-black/40 border border-theme/40 text-xs">
                  <span class="text-[10px] font-mono uppercase text-theme-accent block mb-0.5">The Real Reason:</span>
                  <p class="text-theme-textMuted italic leading-relaxed">"${p.why}"</p>
                </div>

                <div class="mt-2.5 px-3 py-1.5 rounded-xl bg-amber-500/10 border border-amber-500/20 text-[11px] text-amber-200 flex items-center gap-2">
                  <span class="font-mono text-[9px] uppercase px-1.5 py-0.5 rounded bg-amber-500/20 text-amber-300 font-bold">30s Kickstart</span>
                  <span class="truncate">${p.stepZero}</span>
                </div>

                <div class="mt-4 space-y-1.5">
                  <div class="flex items-center justify-between text-[10px] font-mono uppercase tracking-wider text-theme-textMuted">
                    <span>Friendly Steps</span>
                    <span class="text-theme-accent">${completedSteps}/${totalSteps}</span>
                  </div>
                  ${p.steps.map((st, sIdx) => `
                    <div onclick="toggleStepDirect('${p.id}', ${sIdx}, event)" class="p-2 rounded-xl text-xs flex items-center gap-2 cursor-pointer transition ${st.done ? 'bg-emerald-500/10 text-emerald-300 line-through' : 'bg-white/[0.02] text-theme-textMuted hover:bg-white/5'}">
                      <div class="w-4 h-4 rounded border flex items-center justify-center shrink-0 ${st.done ? 'border-emerald-400 bg-emerald-500 text-black' : 'border-theme/60'}">
                        ${st.done ? '<i data-lucide="check" class="w-3 h-3 stroke-[3]"></i>' : ''}
                      </div>
                      <span class="truncate text-xs">${st.text}</span>
                    </div>
                  `).join('')}
                </div>
              </div>

              <div class="mt-5 pt-4 border-t border-theme/40 flex items-center justify-between">
                <div class="flex items-center gap-2">
                  <div class="w-16 h-1.5 rounded-full bg-black/60 overflow-hidden border border-theme/40">
                    <div class="h-full rounded-full transition-all duration-500" style="width: ${pct}%; background-color: var(--accent-color);"></div>
                  </div>
                  <span class="text-[10px] font-mono text-theme-textMuted">${pct}%</span>
                </div>

                <button onclick="initiateProcessSession('${p.id}')" class="px-4 py-2 rounded-xl text-xs font-mono uppercase tracking-wider font-semibold text-black transition flex items-center gap-1.5 shadow-md" style="background-color: var(--accent-color);">
                  <i data-lucide="play" class="w-3 h-3 fill-current"></i>
                  <span>Enter Focus</span>
                </button>
              </div>

            </div>
          `;
        }).join('');
      }

      // Mental Bookmarks View
      const seedItems = chronicle.filter(c => c.type === 'seed');
      if (seedItems.length === 0) {
        bookmarksView.innerHTML = `
          <div class="glass-surface rounded-3xl p-12 text-center max-w-xl mx-auto">
            <div class="w-12 h-12 rounded-2xl bg-emerald-500/10 border border-emerald-500/20 text-emerald-300 flex items-center justify-center mx-auto mb-3">
              <i data-lucide="bookmark" class="w-6 h-6"></i>
            </div>
            <h3 class="font-serif text-lg text-slate-100 font-medium">No Mental Bookmarks Stored</h3>
            <p class="text-xs text-theme-textMuted mt-1">Whenever you pause early, your quick note will be stored here so your brain can relax without stressing over forgotten details.</p>
          </div>
        `;
      } else {
        bookmarksView.innerHTML = `
          <div class="max-w-3xl mx-auto space-y-3.5">
            <div class="flex items-center justify-between px-2">
              <span class="text-xs font-mono uppercase tracking-wider text-theme-accent">Mental Bookmarks (Saved for Tomorrow)</span>
              <span class="text-[11px] font-mono text-theme-textMuted">${seedItems.length} Notes Saved</span>
            </div>
            ${seedItems.map(item => `
              <div class="glass-surface rounded-2xl p-4 sm:p-5 border-l-4 border-l-emerald-400 space-y-2">
                <div class="flex items-center justify-between">
                  <h4 class="font-serif text-base text-slate-100 font-medium">${item.intention}</h4>
                  <span class="text-[10px] font-mono text-theme-textMuted">${new Date(item.timestamp).toLocaleDateString()}</span>
                </div>
                <div class="p-3 rounded-xl bg-black/50 border border-theme/50 text-xs text-emerald-200 font-mono">
                  <span class="text-[10px] text-theme-textMuted uppercase block mb-0.5">Where You Left Off:</span>
                  "${item.note}"
                </div>
                <div class="text-[10px] text-theme-textMuted font-mono">
                  ${item.duration} minutes of high-value practice invested.
                </div>
              </div>
            `).join('')}
          </div>
        `;
      }

      // Trophy Room & Chronicle View
      if (badges.length === 0) {
        chronicleView.innerHTML = `
          <div class="glass-surface rounded-3xl p-12 text-center max-w-xl mx-auto">
            <div class="w-12 h-12 rounded-2xl bg-amber-500/10 border border-amber-500/20 text-amber-300 flex items-center justify-center mx-auto mb-3">
              <i data-lucide="award" class="w-6 h-6"></i>
            </div>
            <h3 class="font-serif text-lg text-slate-100 font-medium">Your Badge Trophy Room is Waiting</h3>
            <p class="text-xs text-theme-textMuted mt-1">Complete your first mindful process to unlock unique collectible badges, celebratory fireworks, and guilt-free brain treats!</p>
          </div>
        `;
      } else {
        chronicleView.innerHTML = `
          <div class="space-y-4">
            <div class="flex items-center justify-between px-2">
              <span class="text-xs font-mono uppercase tracking-wider text-theme-accent">Unlocked Identity Badges (${badges.length})</span>
              <button onclick="clearBadges()" class="text-[11px] font-mono text-theme-textMuted hover:text-rose-400 transition">Clear Badges</button>
            </div>
            
            <div class="grid grid-cols-1 sm:grid-cols-2 lg:grid-cols-3 gap-4">
              ${badges.map(b => `
                <div class="glass-surface rounded-2xl p-5 border border-theme relative overflow-hidden flex flex-col justify-between">
                  <div class="flex items-start justify-between">
                    <div class="flex items-center gap-3">
                      <span class="text-3xl">${b.icon}</span>
                      <div>
                        <span class="text-[10px] font-mono uppercase text-amber-400 block">${b.subtitle}</span>
                        <h4 class="font-serif text-base text-slate-100 font-semibold">${b.title}</h4>
                      </div>
                    </div>
                  </div>

                  <p class="text-xs text-theme-textMuted my-3 italic">"${b.processName}"</p>

                  <div class="pt-3 border-t border-theme/40 flex items-center justify-between text-[11px] font-mono text-theme-textMuted">
                    <span>${b.minutes} min flow</span>
                    <span class="text-theme-accent">${b.stepsRatio} steps</span>
                  </div>
                </div>
              `).join('')}
            </div>
          </div>
        `;
      }

      lucide.createIcons();
    }

    function clearBadges() {
      badges = [];
      saveBadges();
      renderDashboard();
    }

    function updateMetricsDashboard() {
      const totalMinutes = chronicle.reduce((acc, c) => acc + (c.duration || 0), 0);
      const identityVotes = badges.length;
      const seedsCount = chronicle.filter(c => c.type === 'seed').length;
      
      document.getElementById('statArenaTime').innerText = `${totalMinutes} min`;
      document.getElementById('statIdentityVotes').innerText = `${identityVotes}`;
      document.getElementById('statSeedsCount').innerText = `${seedsCount}`;
      document.getElementById('statBookmarksCount').innerText = `${seedsCount}`;
    }

    function openScienceInPlainEnglishModal() {
      const modal = document.getElementById('plainEnglishModal');
      const box = document.getElementById('plainEnglishBox');
      modal.classList.remove('opacity-0', 'pointer-events-none');
      box.classList.remove('scale-95');
      box.classList.add('scale-100');
    }

    function closeScienceInPlainEnglishModal() {
      const modal = document.getElementById('plainEnglishModal');
      const box = document.getElementById('plainEnglishBox');
      modal.classList.add('opacity-0', 'pointer-events-none');
      box.classList.add('scale-95');
      box.classList.remove('scale-100');
    }

    function ensureInitialData() {
      if (processes.length === 0 && chronicle.length === 0) {
        processes = [
          {
            id: 'sample-p1',
            intention: 'Sketch 3 clean layouts for personal portfolio',
            why: 'To bring creative ideas to life and enjoy designing without pressure.',
            friction: 'ambiguity',
            stepZero: 'Grab a blank sheet of paper and an ink pen',
            duration: 25,
            horizon: 'Morning Creative Time',
            customReward: 'Enjoy a warm cup of coffee outside',
            steps: [
              { id: 's1', text: 'Turn phone face-down and put on quiet sounds', done: false },
              { id: 's2', text: 'Draw 3 rough boxes for headers and cards', done: false },
              { id: 's3', text: 'Pick your favorite draft with a relaxed smile', done: false }
            ],
            createdAt: Date.now()
          }
        ];
        saveProcesses();
      }
    }

    window.addEventListener('DOMContentLoaded', () => {
      const savedTheme = localStorage.getItem(STORAGE_KEY_THEME) || 'teal';
      setTheme(savedTheme);
      ensureInitialData();
      updateFrictionTip();
      renderDashboard();
      updateMetricsDashboard();
      lucide.createIcons();

      window.addEventListener('resize', () => {
        const fwCanvas = document.getElementById('fireworksCanvas');
        if (fwCanvas) {
          fwCanvas.width = window.innerWidth;
          fwCanvas.height = window.innerHeight;
        }
        const seedCanvas = document.getElementById('seedCanvas');
        if (seedCanvas) {
          seedCanvas.width = window.innerWidth;
          seedCanvas.height = window.innerHeight;
        }
      });
    });
  </script>
</body>
</html>
