<html lang="en" class="dark">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Project Eklavya - 20 MW Paper Industry Gasification Platform</title>
    <!-- Tailwind CSS -->
    <script src="https://cdn.tailwindcss.com"></script>
    <script>
        tailwind.config = {
            darkMode: 'class',
            theme: {
                extend: {
                    colors: {
                        brand: {
                            50: '#f0fdf4',
                            100: '#dcfce7',
                            500: '#22c55e',
                            600: '#16a34a',
                            700: '#15803d',
                            800: '#166534',
                            900: '#14532d',
                        },
                        amber: {
                            500: '#f59e0b',
                            600: '#d97706',
                        }
                    }
                }
            }
        }
    </script>
    <!-- FontAwesome Icons -->
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <!-- Google Fonts -->
    <link href="https://fonts.googleapis.com/css2?family=Inter:wght@300;400;500;600;700;800&family=JetBrains+Mono:wght@400;600&display=swap" rel="stylesheet">
    <!-- Chart.js -->
    <script src="https://cdn.jsdelivr.net/npm/chart.js"></script>
    <!-- Three.js & OrbitControls -->
    <script src="https://cdnjs.cloudflare.com/ajax/libs/three.js/r128/three.min.js"></script>
    <script src="https://cdn.jsdelivr.net/npm/three@0.128.0/examples/js/controls/OrbitControls.js"></script>
    <style>
        body { font-family: 'Inter', sans-serif; }
        .font-mono { font-family: 'JetBrains Mono', monospace; }
        /* Custom scrollbar */
        ::-webkit-scrollbar { width: 6px; height: 6px; }
        ::-webkit-scrollbar-track { background: rgba(0, 0, 0, 0.1); }
        ::-webkit-scrollbar-thumb { background: rgba(34, 197, 94, 0.4); border-radius: 3px; }
        ::-webkit-scrollbar-thumb:hover { background: rgba(34, 197, 94, 0.8); }
        .glass-panel {
            background: rgba(17, 24, 39, 0.7);
            backdrop-filter: blur(12px);
            border: 1px solid rgba(255, 255, 255, 0.08);
        }
        .light .glass-panel {
            background: rgba(255, 255, 255, 0.85);
            border: 1px solid rgba(0, 0, 0, 0.08);
        }
        .glow-effect {
            box-shadow: 0 0 25px -5px rgba(34, 197, 94, 0.3);
        }
    </style>
</head>
<body class="bg-gray-950 text-gray-100 min-h-screen flex flex-col transition-colors duration-200 light:bg-gray-100 light:text-gray-900">

    <!-- Top Navigation Header -->
    <header class="sticky top-0 z-40 border-b border-gray-800 bg-gray-900/90 backdrop-blur-md light:bg-white/90 light:border-gray-200">
        <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8">
            <div class="flex items-center justify-between h-16">
                <!-- Logo & Brand -->
                <div class="flex items-center gap-3 cursor-pointer" onclick="switchTab('home')">
                    <div class="w-10 h-10 rounded-xl bg-gradient-to-tr from-brand-600 to-emerald-400 flex items-center justify-center text-white font-black text-xl shadow-lg shadow-brand-500/30">
                        E
                    </div>
                    <div>
                        <span class="text-xl font-bold tracking-tight text-white light:text-gray-900">PROJECT <span class="text-brand-500">EKLAVYA</span></span>
                        <span class="block text-[10px] font-mono tracking-widest text-emerald-400 uppercase">20 MW Waste-to-Energy Platform</span>
                    </div>
                </div>

                <!-- Navigation Tabs -->
                <nav class="hidden md:flex space-x-1 lg:space-x-2 text-sm font-medium">
                    <button onclick="switchTab('home')" id="nav-home" class="nav-btn px-3 py-2 rounded-lg text-brand-500 bg-gray-800/60 light:bg-gray-200 font-semibold transition-all">
                        <i class="fa-solid fa-house mr-1.5"></i><span data-i18n="nav_home">Home</span>
                    </button>
                    <button onclick="switchTab('model3d')" id="nav-model3d" class="nav-btn px-3 py-2 rounded-lg text-gray-400 hover:text-white light:hover:text-gray-900 hover:bg-gray-800/40 transition-all">
                        <i class="fa-solid fa-cube mr-1.5"></i><span data-i18n="nav_3d">3D CAD Model</span>
                    </button>
                    <button onclick="switchTab('calculator')" id="nav-calculator" class="nav-btn px-3 py-2 rounded-lg text-gray-400 hover:text-white light:hover:text-gray-900 hover:bg-gray-800/40 transition-all">
                        <i class="fa-solid fa-calculator mr-1.5"></i><span data-i18n="nav_calc">Calculator</span>
                    </button>
                    <button onclick="switchTab('diagrams')" id="nav-diagrams" class="nav-btn px-3 py-2 rounded-lg text-gray-400 hover:text-white light:hover:text-gray-900 hover:bg-gray-800/40 transition-all">
                        <i class="fa-solid fa-diagram-project mr-1.5"></i><span data-i18n="nav_diagrams">Schematics</span>
                    </button>
                    <button onclick="switchTab('pricespecs')" id="nav-pricespecs" class="nav-btn px-3 py-2 rounded-lg text-gray-400 hover:text-white light:hover:text-gray-900 hover:bg-gray-800/40 transition-all">
                        <i class="fa-solid fa-tag mr-1.5"></i><span data-i18n="nav_pricing">Price & Specs</span>
                    </button>
                    <button onclick="handleAdminTabClick()" id="nav-admindb" class="nav-btn px-3 py-2 rounded-lg text-amber-500 hover:bg-amber-500/10 transition-all">
                        <i class="fa-solid fa-shield-halved mr-1.5"></i><span data-i18n="nav_admin">Admin DB</span>
                    </button>
                </nav>

                <!-- User Controls & Utilities -->
                <div class="flex items-center gap-3">
                    <!-- Language Toggle -->
                    <button onclick="toggleLanguage()" class="px-2.5 py-1.5 rounded-lg border border-gray-700 light:border-gray-300 text-xs font-mono hover:border-brand-500 transition-colors">
                        <i class="fa-solid fa-language mr-1 text-brand-500"></i><span id="lang-indicator">EN</span>
                    </button>

                    <!-- Dark/Light Theme Toggle -->
                    <button onclick="toggleTheme()" class="p-2 rounded-lg border border-gray-700 light:border-gray-300 text-gray-400 hover:text-white light:hover:text-gray-900 transition-colors">
                        <i class="fa-solid fa-moon dark:inline hidden"></i>
                        <i class="fa-solid fa-sun dark:hidden inline"></i>
                    </button>

                    <!-- Auth Button / Avatar -->
                    <div id="auth-container">
                        <button onclick="openAuthModal()" id="btn-login-trigger" class="px-4 py-2 text-sm font-semibold rounded-lg bg-brand-600 hover:bg-brand-500 text-white shadow-md shadow-brand-600/20 transition-all">
                            <i class="fa-solid fa-right-to-bracket mr-1.5"></i><span data-i18n="btn_login">Login</span>
                        </button>
                        <div id="user-profile-badge" class="hidden flex items-center gap-2 cursor-pointer" onclick="openAuthModal()">
                            <div class="w-8 h-8 rounded-full bg-emerald-600 text-white flex items-center justify-center font-bold text-sm border-2 border-brand-400" id="user-avatar-initial">
                                U
                            </div>
                            <span class="text-xs font-medium hidden sm:inline text-gray-300 light:text-gray-700" id="user-display-name">User</span>
                        </div>
                    </div>
                </div>
            </div>
        </div>
    </header>

    <!-- Main Content Area -->
    <main class="flex-grow max-w-7xl w-full mx-auto px-4 sm:px-6 lg:px-8 py-6">

        <!-- PAGE 1: HOME -->
        <section id="page-home" class="space-y-12">
            <!-- Hero Banner -->
            <div class="relative overflow-hidden rounded-3xl bg-gradient-to-br from-gray-900 via-gray-900 to-emerald-950 p-8 md:p-12 border border-emerald-500/20 shadow-2xl">
                <div class="absolute -right-20 -bottom-20 w-96 h-96 bg-brand-500/10 rounded-full blur-3xl"></div>
                <div class="relative z-10 max-w-3xl">
                    <div class="inline-flex items-center gap-2 px-3 py-1 rounded-full bg-brand-500/10 border border-brand-500/30 text-brand-400 text-xs font-mono mb-6">
                        <span class="w-2 h-2 rounded-full bg-brand-500 animate-pulse"></span>
                        <span data-i18n="hero_badge">20 MW Industrial Scale Energy Recovery System</span>
                    </div>
                    <h1 class="text-4xl sm:text-5xl font-extrabold tracking-tight text-white mb-4 leading-tight">
                        Transform Paper Industry Sludge into <span class="text-transparent bg-clip-text bg-gradient-to-r from-brand-400 to-emerald-200">20 MW Clean Syngas Power</span>
                    </h1>
                    <p class="text-gray-300 text-lg mb-8 leading-relaxed" data-i18n="hero_desc">
                        Project Eklavya engineered a high-efficiency thermochemical gasification framework tailored explicitly for paper and pulp mill waste stream streams—enabling continuously synchronized 20 hours/day operating cycles with zero toxic residue.
                    </p>
                    <div class="flex flex-wrap gap-4">
                        <button onclick="switchTab('calculator')" class="px-6 py-3.5 rounded-xl bg-brand-600 hover:bg-brand-500 text-white font-semibold text-sm shadow-lg shadow-brand-600/30 transition-all flex items-center gap-2">
                            <i class="fa-solid fa-calculator"></i>
                            <span data-i18n="hero_btn_calc">Calculate Mill Yield</span>
                        </button>
                        <button onclick="switchTab('model3d')" class="px-6 py-3.5 rounded-xl border border-gray-700 bg-gray-800/80 hover:bg-gray-700 text-white font-semibold text-sm transition-all flex items-center gap-2">
                            <i class="fa-solid fa-cube"></i>
                            <span data-i18n="hero_btn_3d">Explore 3D Plant Model</span>
                        </button>
                    </div>
                </div>

                <!-- Live IST Telemetry Banner -->
                <div class="mt-10 pt-6 border-t border-gray-800/80 grid grid-cols-2 md:grid-cols-4 gap-4">
                    <div class="bg-gray-950/60 p-3.5 rounded-xl border border-gray-800">
                        <div class="text-xs text-gray-400 font-mono" data-i18n="stat_capacity">Nominal Capacity</div>
                        <div class="text-xl font-bold text-brand-400 font-mono">20.0 MW</div>
                    </div>
                    <div class="bg-gray-950/60 p-3.5 rounded-xl border border-gray-800">
                        <div class="text-xs text-gray-400 font-mono" data-i18n="stat_duty">Daily Duty Cycle</div>
                        <div class="text-xl font-bold text-emerald-400 font-mono">20 Hours / Day</div>
                    </div>
                    <div class="bg-gray-950/60 p-3.5 rounded-xl border border-gray-800">
                        <div class="text-xs text-gray-400 font-mono" data-i18n="stat_temp">Pyrolysis Core Temp</div>
                        <div class="text-xl font-bold text-amber-400 font-mono">450 °C - 1050 °C</div>
                    </div>
                    <div class="bg-gray-950/60 p-3.5 rounded-xl border border-gray-800">
                        <div class="text-xs text-gray-400 font-mono" data-i18n="stat_time">IST Live Telemetry</div>
                        <div id="live-ist-time" class="text-sm font-semibold text-cyan-400 font-mono">--:--:-- IST</div>
                    </div>
                </div>
            </div>

            <!-- Problem vs Solution Matrix -->
            <div class="grid md:grid-cols-2 gap-6">
                <div class="p-6 rounded-2xl bg-red-950/20 border border-red-900/30">
                    <div class="flex items-center gap-3 text-red-400 font-bold text-lg mb-4">
                        <div class="w-10 h-10 rounded-lg bg-red-500/10 flex items-center justify-center">
                            <i class="fa-solid fa-triangle-exclamation"></i>
                        </div>
                        <span data-i18n="prob_title">Paper Industry Sludge Challenge</span>
                    </div>
                    <ul class="space-y-3 text-sm text-gray-300">
                        <li class="flex items-start gap-2">
                            <i class="fa-solid fa-xmark text-red-500 mt-1"></i>
                            <span data-i18n="prob_1">High moisture paper sludge (40-60% wet pulp) costly to haul to landfills.</span>
                        </li>
                        <li class="flex items-start gap-2">
                            <i class="fa-solid fa-xmark text-red-500 mt-1"></i>
                            <span data-i18n="prob_2">Deinking residues and OCC fiber tailings produce toxic leachate and methane gases.</span>
                        </li>
                        <li class="flex items-start gap-2">
                            <i class="fa-solid fa-xmark text-red-500 mt-1"></i>
                            <span data-i18n="prob_3">Rising grid electricity tariffs strain mill operational margins during 24/7 paper production.</span>
                        </li>
                    </ul>
                </div>

                <div class="p-6 rounded-2xl bg-brand-950/20 border border-brand-900/30">
                    <div class="flex items-center gap-3 text-brand-400 font-bold text-lg mb-4">
                        <div class="w-10 h-10 rounded-lg bg-brand-500/10 flex items-center justify-center">
                            <i class="fa-solid fa-lightbulb"></i>
                        </div>
                        <span data-i18n="sol_title">Project Eklavya Solution</span>
                    </div>
                    <ul class="space-y-3 text-sm text-gray-300">
                        <li class="flex items-start gap-2">
                            <i class="fa-solid fa-check text-brand-500 mt-1"></i>
                            <span data-i18n="sol_1">Dual-auger pyrolysis pre-treatment at 450°C rapidly flash-dries wet paper sludge.</span>
                        </li>
                        <li class="flex items-start gap-2">
                            <i class="fa-solid fa-check text-brand-500 mt-1"></i>
                            <span data-i18n="sol_2">Thermochemical cracking yields clean syngas for direct power in a 20 MW turbine.</span>
                        </li>
                        <li class="flex items-start gap-2">
                            <i class="fa-solid fa-check text-brand-500 mt-1"></i>
                            <span data-i18n="sol_3">Dual Cyclone & Venturi Scrubbers filter 99.8% tar & particulate emissions.</span>
                        </li>
                    </ul>
                </div>
            </div>

            <!-- Master Waste Streams Database (1000+ Stream Search Simulation) -->
            <div class="glass-panel p-6 rounded-2xl">
                <div class="flex flex-col md:flex-row md:items-center justify-between gap-4 mb-6">
                    <div>
                        <h2 class="text-xl font-bold text-white flex items-center gap-2">
                            <i class="fa-solid fa-database text-brand-500"></i>
                            <span data-i18n="db_title">Paper Industry Waste Feedstock Master Database</span>
                        </h2>
                        <p class="text-xs text-gray-400 mt-1" data-i18n="db_subtitle">1,000+ Indexed Paper & Pulp Waste Stream Profiles & Thermochemical Parameters</p>
                    </div>
                    <div class="flex items-center gap-3">
                        <input type="text" id="db-search-input" onkeyup="filterWasteDb()" placeholder="Search waste stream (e.g., Sludge, Pulp, OCC)..." class="bg-gray-900 border border-gray-700 rounded-xl px-4 py-2 text-sm text-white focus:outline-none focus:border-brand-500 w-64">
                    </div>
                </div>

                <div class="overflow-x-auto">
                    <table class="w-full text-left text-sm border-collapse">
                        <thead>
                            <tr class="border-b border-gray-800 text-xs font-mono uppercase text-gray-400 bg-gray-900/50">
                                <th class="p-3">Stream Code</th>
                                <th class="p-3">Feedstock Type</th>
                                <th class="p-3">Moisture %</th>
                                <th class="p-3">Calorific Value (MJ/kg)</th>
                                <th class="p-3">Gasification Yield (m³/ton)</th>
                                <th class="p-3">Biochar Output</th>
                                <th class="p-3">Suitability</th>
                            </tr>
                        </thead>
                        <tbody id="waste-db-body" class="divide-y divide-gray-800/50 text-gray-300">
                            <!-- Populated dynamically via JS -->
                        </tbody>
                    </table>
                </div>
            </div>

            <!-- Process Workflow Summary -->
            <div class="glass-panel p-6 rounded-2xl">
                <h3 class="text-lg font-bold text-white mb-6 flex items-center gap-2">
                    <i class="fa-solid fa-arrows-spin text-brand-500"></i>
                    <span data-i18n="workflow_title">Integrated 7-Stage Waste-to-Energy Flow</span>
                </h3>
                <div class="grid grid-cols-2 md:grid-cols-4 lg:grid-cols-7 gap-3 text-center">
                    <div class="p-3 bg-gray-900/60 rounded-xl border border-gray-800">
                        <div class="text-brand-400 font-bold text-xs mb-1">01. INFEED</div>
                        <div class="text-xs font-medium">Sludge Hopper</div>
                    </div>
                    <div class="p-3 bg-gray-900/60 rounded-xl border border-gray-800">
                        <div class="text-brand-400 font-bold text-xs mb-1">02. PYROLYSIS</div>
                        <div class="text-xs font-medium">450°C Auger Reactor</div>
                    </div>
                    <div class="p-3 bg-gray-900/60 rounded-xl border border-gray-800">
                        <div class="text-brand-400 font-bold text-xs mb-1">03. GASIFIER</div>
                        <div class="text-xs font-medium">1050°C Thermal Core</div>
                    </div>
                    <div class="p-3 bg-gray-900/60 rounded-xl border border-gray-800">
                        <div class="text-brand-400 font-bold text-xs mb-1">04. CYCLONE</div>
                        <div class="text-xs font-medium">Ash Separator</div>
                    </div>
                    <div class="p-3 bg-gray-900/60 rounded-xl border border-gray-800">
                        <div class="text-brand-400 font-bold text-xs mb-1">05. WET SCRUBBER</div>
                        <div class="text-xs font-medium">Venturi Scrubber</div>
                    </div>
                    <div class="p-3 bg-gray-900/60 rounded-xl border border-gray-800">
                        <div class="text-brand-400 font-bold text-xs mb-1">06. TURBINE</div>
                        <div class="text-xs font-medium">20 MW Generator</div>
                    </div>
                    <div class="p-3 bg-gray-900/60 rounded-xl border border-brand-500/30 bg-brand-950/20">
                        <div class="text-brand-400 font-bold text-xs mb-1">07. OUTPUT</div>
                        <div class="text-xs font-semibold text-brand-300">Clean Grid Power</div>
                    </div>
                </div>
            </div>
        </section>

        <!-- PAGE 2: 3D CAD MODEL -->
        <section id="page-model3d" class="hidden space-y-6">
            <div class="flex flex-col md:flex-row items-start md:items-center justify-between gap-4">
                <div>
                    <h2 class="text-2xl font-bold text-white" data-i18n="title_3d">20 MW Gasification Skid 3D WebGL Inspector</h2>
                    <p class="text-sm text-gray-400" data-i18n="sub_3d">Interactive 3D CAD representation of Inconel-600 core, auger pyrolysis unit, cyclone & Venturi scrubbers.</p>
                </div>
                <div class="flex items-center gap-2">
                    <button onclick="reset3DCamera()" class="px-3 py-1.5 rounded-lg bg-gray-800 hover:bg-gray-700 text-xs font-mono text-gray-300 border border-gray-700">
                        <i class="fa-solid fa-arrows-to-dot mr-1"></i>Reset View
                    </button>
                    <button onclick="toggle3DLight()" class="px-3 py-1.5 rounded-lg bg-gray-800 hover:bg-gray-700 text-xs font-mono text-gray-300 border border-gray-700">
                        <i class="fa-solid fa-lightbulb mr-1"></i>Toggle Spotlight
                    </button>
                </div>
            </div>

            <div class="grid lg:grid-cols-4 gap-6">
                <!-- 3D Canvas Container -->
                <div class="lg:col-span-3 relative h-[500px] rounded-2xl overflow-hidden border border-gray-800 bg-gray-950">
                    <div id="threejs-canvas-container" class="w-full h-full"></div>
                    <div class="absolute bottom-4 left-4 bg-gray-900/80 backdrop-blur-md px-3 py-2 rounded-lg border border-gray-700 text-xs text-gray-300">
                        <i class="fa-solid fa-hand-pointer mr-1.5 text-brand-400"></i>Drag to rotate | Scroll to zoom | Click components to inspect
                    </div>
                </div>

                <!-- Component Inspector Panel -->
                <div class="glass-panel p-6 rounded-2xl flex flex-col justify-between">
                    <div>
                        <div class="text-xs font-mono text-brand-400 mb-1" id="inspector-tag">SUB-SYSTEM INSPECTOR</div>
                        <h3 class="text-lg font-bold text-white mb-3" id="inspector-title">Select Component</h3>
                        <p class="text-sm text-gray-300 mb-4 leading-relaxed" id="inspector-desc">
                            Click on any component in the 3D model viewport (Feed Hopper, Pyrolysis Chamber, Gasifier Core, Scrubbers, or Turbine) to view real-time operating parameters and material specifications.
                        </p>
                    </div>

                    <div class="space-y-3 pt-4 border-t border-gray-800" id="inspector-specs">
                        <div class="flex justify-between text-xs">
                            <span class="text-gray-400">Temp Rating:</span>
                            <span class="font-mono text-brand-400" id="spec-temp">--</span>
                        </div>
                        <div class="flex justify-between text-xs">
                            <span class="text-gray-400">Alloy Material:</span>
                            <span class="font-mono text-gray-200" id="spec-material">--</span>
                        </div>
                        <div class="flex justify-between text-xs">
                            <span class="text-gray-400">Efficiency Yield:</span>
                            <span class="font-mono text-emerald-400" id="spec-eff">--</span>
                        </div>
                    </div>
                </div>
            </div>
        </section>

        <!-- PAGE 3: CALCULATOR -->
        <section id="page-calculator" class="hidden space-y-8">
            <div>
                <h2 class="text-2xl font-bold text-white" data-i18n="calc_title">Paper Waste Energy Yield & ROI Calculator</h2>
                <p class="text-sm text-gray-400" data-i18n="calc_sub">Calibrated specifically for paper sludge, fiber tailings, and deinking residues based on 20 Hours/Day plant operation.</p>
            </div>

            <div class="grid lg:grid-cols-3 gap-8">
                <!-- Input Configuration Panel -->
                <div class="glass-panel p-6 rounded-2xl space-y-6">
                    <h3 class="text-lg font-bold text-white border-b border-gray-800 pb-3" data-i18n="calc_input_title">Feedstock Input</h3>

                    <!-- Numeric Input & Unit Selector -->
                    <div>
                        <label class="block text-xs font-medium text-gray-400 mb-2" data-i18n="calc_feedstock_qty">Daily Feedstock Quantity</label>
                        <div class="flex gap-2">
                            <input type="number" id="calc-input-qty" value="50" min="1" max="10000" oninput="syncCalcInputs('number')" class="w-full bg-gray-900 border border-gray-700 rounded-xl px-4 py-2.5 font-mono text-lg text-brand-400 focus:outline-none focus:border-brand-500">
                            <div class="flex rounded-xl bg-gray-900 p-1 border border-gray-700">
                                <button id="unit-tonnes" onclick="setCalcUnit('tonnes')" class="px-3 py-1 rounded-lg text-xs font-semibold bg-brand-600 text-white transition-all">Tonnes</button>
                                <button id="unit-kg" onclick="setCalcUnit('kg')" class="px-3 py-1 rounded-lg text-xs font-semibold text-gray-400 hover:text-white transition-all">kg</button>
                            </div>
                        </div>
                    </div>

                    <!-- Range Slider -->
                    <div>
                        <div class="flex justify-between text-xs text-gray-400 mb-1">
                            <span>Scale Slider</span>
                            <span id="slider-max-label" class="font-mono">100 Tonnes</span>
                        </div>
                        <input type="range" id="calc-slider" min="1" max="100" value="50" oninput="syncCalcInputs('slider')" class="w-full accent-brand-500 cursor-pointer">
                    </div>

                    <!-- Waste Type Selector -->
                    <div>
                        <label class="block text-xs font-medium text-gray-400 mb-2" data-i18n="calc_select_type">Paper Feedstock Category</label>
                        <select id="calc-waste-type" onchange="runCalculation()" class="w-full bg-gray-900 border border-gray-700 rounded-xl px-4 py-2.5 text-sm text-gray-200 focus:outline-none focus:border-brand-500">
                            <option value="sludge">Paper Mill Primary/Secondary Sludge (50% Moist)</option>
                            <option value="occ">Old Corrugated Containers (OCC) Rejects</option>
                            <option value="deinked">Deinked Paper Pulp Residues</option>
                            <option value="woodbark">Wood Bark & Pulp Timber Chipping Waste</option>
                        </select>
                    </div>

                    <!-- Electricity Tariff Rate Input -->
                    <div>
                        <label class="block text-xs font-medium text-gray-400 mb-2" data-i18n="calc_tariff">Grid Electricity Cost (₹ / kWh)</label>
                        <input type="number" id="calc-tariff" value="8.50" step="0.5" oninput="runCalculation()" class="w-full bg-gray-900 border border-gray-700 rounded-xl px-4 py-2.5 font-mono text-sm text-white focus:outline-none focus:border-brand-500">
                    </div>
                </div>

                <!-- Calculated Metrics Outputs -->
                <div class="lg:col-span-2 space-y-6">
                    <div class="grid grid-cols-2 md:grid-cols-3 gap-4">
                        <div class="glass-panel p-5 rounded-2xl border-l-4 border-brand-500">
                            <div class="text-xs text-gray-400" data-i18n="out_kwh">Daily Power Output</div>
                            <div id="out-kwh" class="text-2xl font-bold font-mono text-brand-400 mt-1">125,000 kWh</div>
                            <div class="text-[10px] text-gray-500 mt-1">20 Hours Operating Cycle</div>
                        </div>

                        <div class="glass-panel p-5 rounded-2xl border-l-4 border-cyan-500">
                            <div class="text-xs text-gray-400" data-i18n="out_syngas">Syngas Generated</div>
                            <div id="out-syngas" class="text-2xl font-bold font-mono text-cyan-400 mt-1">17,500 m³</div>
                            <div class="text-[10px] text-gray-500 mt-1">At 1050°C Gasification</div>
                        </div>

                        <div class="glass-panel p-5 rounded-2xl border-l-4 border-amber-500">
                            <div class="text-xs text-gray-400" data-i18n="out_biochar">Biochar By-product</div>
                            <div id="out-biochar" class="text-2xl font-bold font-mono text-amber-400 mt-1">7.5 Tonnes</div>
                            <div class="text-[10px] text-gray-500 mt-1">Soil / Boiler Fuel Grade</div>
                        </div>

                        <div class="glass-panel p-5 rounded-2xl border-l-4 border-emerald-500">
                            <div class="text-xs text-gray-400" data-i18n="out_savings">Daily Monetary Savings</div>
                            <div id="out-savings" class="text-2xl font-bold font-mono text-emerald-400 mt-1">₹10,62,500</div>
                            <div class="text-[10px] text-gray-500 mt-1">Offsetting Grid Tariffs</div>
                        </div>

                        <div class="glass-panel p-5 rounded-2xl border-l-4 border-indigo-500">
                            <div class="text-xs text-gray-400" data-i18n="out_co2">CO2 Emissions Offset</div>
                            <div id="out-co2" class="text-2xl font-bold font-mono text-indigo-400 mt-1">102.5 Tonnes</div>
                            <div class="text-[10px] text-gray-500 mt-1">Methane & Fossil Avoidance</div>
                        </div>

                        <div class="glass-panel p-5 rounded-2xl border-l-4 border-purple-500">
                            <div class="text-xs text-gray-400" data-i18n="out_mill_duty">Mill Duty Coverage</div>
                            <div id="out-duty" class="text-2xl font-bold font-mono text-purple-400 mt-1">20.0 Hours/Day</div>
                            <div class="text-[10px] text-gray-500 mt-1">Continuous Plant Duty</div>
                        </div>
                    </div>

                    <!-- Breakdown Chart -->
                    <div class="glass-panel p-6 rounded-2xl">
                        <h4 class="text-sm font-bold text-white mb-4" data-i18n="chart_title">Estimated Monthly Mill Energy Savings vs Feedstock Scale (₹ Lakhs)</h4>
                        <div class="h-64">
                            <canvas id="calc-savings-chart"></canvas>
                        </div>
                    </div>
                </div>
            </div>
        </section>

        <!-- PAGE 4: DIAGRAMS -->
        <section id="page-diagrams" class="hidden space-y-8">
            <div>
                <h2 class="text-2xl font-bold text-white" data-i18n="diagrams_title">High-Contrast Technical Schematics</h2>
                <p class="text-sm text-gray-400" data-i18n="diagrams_sub">Detailed engineering flow diagrams for 450°C pyrolysis pre-treatment and dual scrubbing stages.</p>
            </div>

            <div class="grid lg:grid-cols-2 gap-8">
                <!-- SVG Diagram 1: Dual-Auger Pyrolysis Reactor -->
                <div class="glass-panel p-6 rounded-2xl space-y-4">
                    <h3 class="text-base font-bold text-brand-400 flex items-center gap-2">
                        <i class="fa-solid fa-fire-burner"></i>
                        <span data-i18n="diag1_title">450°C Dual-Auger Pyrolysis Pre-treatment</span>
                    </h3>
                    <div class="p-4 bg-gray-950 rounded-xl border border-gray-800">
                        <svg viewBox="0 0 600 300" class="w-full h-auto">
                            <!-- Background Grid -->
                            <defs>
                                <pattern id="grid" width="20" height="20" patternUnits="userSpaceOnUse">
                                    <path d="M 20 0 L 0 0 0 20" fill="none" stroke="#1f2937" stroke-width="0.5"/>
                                </pattern>
                            </defs>
                            <rect width="600" height="300" fill="url(#grid)" />

                            <!-- Hopper -->
                            <polygon points="40,30 100,30 80,90 60,90" fill="#374151" stroke="#22c55e" stroke-width="2"/>
                            <text x="70" y="25" fill="#9ca3af" font-size="10" text-anchor="middle">Wet Sludge Hopper</text>

                            <!-- Auger Chamber Body -->
                            <rect x="60" y="90" width="380" height="80" rx="10" fill="#1f2937" stroke="#4b5563" stroke-width="2"/>

                            <!-- Auger Screw Blades -->
                            <path d="M 70,130 Q 90,100 110,130 T 150,130 T 190,130 T 230,130 T 270,130 T 310,130 T 350,130 T 390,130 T 430,130" fill="none" stroke="#f59e0b" stroke-width="4"/>
                            <path d="M 70,130 Q 90,160 110,130 T 150,130 T 190,130 T 230,130 T 270,130 T 310,130 T 350,130 T 390,130 T 430,130" fill="none" stroke="#f59e0b" stroke-width="4"/>

                            <!-- Heating Elements -->
                            <rect x="100" y="80" width="300" height="6" fill="#ef4444"/>
                            <rect x="100" y="174" width="300" height="6" fill="#ef4444"/>
                            <text x="250" y="72" fill="#ef4444" font-size="11" font-weight="bold" text-anchor="middle">Thermal Pyrolysis Jacket (450°C)</text>

                            <!-- Gas Release Line -->
                            <line x1="250" y1="90" x2="250" y2="40" stroke="#06b6d4" stroke-width="3" stroke-dasharray="4"/>
                            <polygon points="250,35 245,45 255,45" fill="#06b6d4"/>
                            <text x="250" y="25" fill="#06b6d4" font-size="10" text-anchor="middle">Volatiles to Gasifier</text>

                            <!-- Dried Solids Discharge -->
                            <line x1="420" y1="170" x2="420" y2="230" stroke="#22c55e" stroke-width="3"/>
                            <polygon points="420,235 415,225 425,225" fill="#22c55e"/>
                            <rect x="360" y="235" width="120" height="35" rx="6" fill="#111827" stroke="#22c55e" stroke-width="1.5"/>
                            <text x="420" y="256" fill="#22c55e" font-size="10" font-weight="bold" text-anchor="middle">To 1050°C Core</text>
                        </svg>
                    </div>
                </div>

                <!-- SVG Diagram 2: Cyclone & Venturi Wet Scrubber -->
                <div class="glass-panel p-6 rounded-2xl space-y-4">
                    <h3 class="text-base font-bold text-cyan-400 flex items-center gap-2">
                        <i class="fa-solid fa-filter"></i>
                        <span data-i18n="diag2_title">Dual Cyclone & Venturi Wet Scrubber Assembly</span>
                    </h3>
                    <div class="p-4 bg-gray-950 rounded-xl border border-gray-800">
                        <svg viewBox="0 0 600 300" class="w-full h-auto">
                            <!-- Background Grid -->
                            <rect width="600" height="300" fill="url(#grid)" />

                            <!-- Raw Gas Inlet -->
                            <line x1="30" y1="80" x2="100" y2="80" stroke="#f59e0b" stroke-width="4"/>
                            <text x="65" y="70" fill="#f59e0b" font-size="10" text-anchor="middle">Raw Syngas</text>

                            <!-- Cyclone Body -->
                            <polygon points="100,50 170,50 170,140 135,210 100,140" fill="#1f2937" stroke="#06b6d4" stroke-width="2"/>
                            <text x="135" y="100" fill="#9ca3af" font-size="10" text-anchor="middle">Cyclone</text>

                            <!-- Particulate Bottom Discharge -->
                            <rect x="120" y="210" width="30" height="30" fill="#374151"/>
                            <text x="135" y="255" fill="#6b7280" font-size="9" text-anchor="middle">Ash Catch</text>

                            <!-- Connecting Pipe to Venturi -->
                            <path d="M 135,50 L 135,25 L 260,25 L 260,60" fill="none" stroke="#06b6d4" stroke-width="3"/>

                            <!-- Venturi Scrubber Tube -->
                            <polygon points="240,60 280,60 265,110 275,150 245,150 255,110" fill="#111827" stroke="#22c55e" stroke-width="2"/>
                            <!-- Water Sprays -->
                            <line x1="220" y1="100" x2="255" y2="105" stroke="#3b82f6" stroke-width="2" stroke-dasharray="2"/>
                            <line x1="300" y1="100" x2="265" y2="105" stroke="#3b82f6" stroke-width="2" stroke-dasharray="2"/>
                            <text x="260" y="95" fill="#3b82f6" font-size="9" text-anchor="middle">Liquid Jet</text>

                            <!-- Packed Scrubber Tower -->
                            <rect x="360" y="60" width="90" height="170" rx="8" fill="#1f2937" stroke="#22c55e" stroke-width="2"/>
                            <pattern id="packing" width="10" height="10" patternUnits="userSpaceOnUse">
                                <circle cx="5" cy="5" r="2" fill="#374151"/>
                            </pattern>
                            <rect x="370" y="100" width="70" height="80" fill="url(#packing)"/>
                            <text x="405" y="145" fill="#22c55e" font-size="10" font-weight="bold" text-anchor="middle">Clean Tar-Free</text>

                            <!-- Final Clean Gas Outlet -->
                            <line x1="450" y1="100" x2="550" y2="100" stroke="#22c55e" stroke-width="4"/>
                            <polygon points="555,100 545,95 545,105" fill="#22c55e"/>
                            <text x="500" y="90" fill="#22c55e" font-size="10" font-weight="bold" text-anchor="middle">To Turbine</text>
                        </svg>
                    </div>
                </div>
            </div>
        </section>

        <!-- PAGE 5: PRICE AND SPECS -->
        <section id="page-pricespecs" class="hidden space-y-8">
            <div class="flex flex-col md:flex-row items-start md:items-center justify-between gap-4">
                <div>
                    <h2 class="text-2xl font-bold text-white" data-i18n="price_title">Turnkey Unit Commercial Pricing & Engineering Specifications</h2>
                    <p class="text-sm text-gray-400" data-i18n="price_sub">Fixed commercial deployment cost and full bill of materials for paper industry gasifiers.</p>
                </div>
                <div class="px-4 py-2 rounded-xl bg-brand-500/10 border border-brand-500/30 text-brand-400 font-mono text-sm font-bold">
                    Fixed Turnkey Cost: ₹20 Lakhs (₹20,00,000 / ~$24,000 USD)
                </div>
            </div>

            <!-- ROI Highlight Cards -->
            <div class="grid md:grid-cols-3 gap-6">
                <div class="glass-panel p-6 rounded-2xl border-t-4 border-brand-500">
                    <div class="text-xs font-mono text-brand-400 uppercase">Capital Expenditure</div>
                    <div class="text-3xl font-extrabold text-white mt-1">₹20 Lakhs</div>
                    <p class="text-xs text-gray-400 mt-2">Includes complete skid delivery, 20 MW gasifier core, dual scrubbers, controls, and installation.</p>
                </div>

                <div class="glass-panel p-6 rounded-2xl border-t-4 border-emerald-500">
                    <div class="text-xs font-mono text-emerald-400 uppercase">Accelerated ROI Payback</div>
                    <div class="text-3xl font-extrabold text-white mt-1">1.5 - 3 Months</div>
                    <p class="text-xs text-gray-400 mt-2">Rapid capital amortization through complete elimination of landfill hauling & grid tariff offsets.</p>
                </div>

                <div class="glass-panel p-6 rounded-2xl border-t-4 border-cyan-500">
                    <div class="text-xs font-mono text-cyan-400 uppercase">Expected Service Life</div>
                    <div class="text-3xl font-extrabold text-white mt-1">15+ Years</div>
                    <p class="text-xs text-gray-400 mt-2">Built with corrosion-resistant Inconel-600 superalloy suited for sulfur/chlorine pulp vapors.</p>
                </div>
            </div>

            <!-- Engineering Components Breakdown Table -->
            <div class="glass-panel p-6 rounded-2xl">
                <h3 class="text-lg font-bold text-white mb-4" data-i18n="specs_table_title">Technical Component Specification Sheet</h3>
                <div class="overflow-x-auto">
                    <table class="w-full text-left text-sm border-collapse">
                        <thead>
                            <tr class="border-b border-gray-800 text-xs font-mono uppercase text-gray-400 bg-gray-900/50">
                                <th class="p-3.5">Sub-System</th>
                                <th class="p-3.5">Material Grade</th>
                                <th class="p-3.5">Operating Limits</th>
                                <th class="p-3.5">Design Function</th>
                            </tr>
                        </thead>
                        <tbody class="divide-y divide-gray-800/60 text-gray-300">
                            <tr>
                                <td class="p-3.5 font-semibold text-white">Gasifier Chamber Core</td>
                                <td class="p-3.5 font-mono text-brand-400">Inconel-600 Superalloy</td>
                                <td class="p-3.5 font-mono text-amber-400">1050°C / 5 bar</td>
                                <td class="p-3.5 text-xs">Thermal cracking of pulp sludge volatiles into CO & H2.</td>
                            </tr>
                            <tr>
                                <td class="p-3.5 font-semibold text-white">Pyrolysis Pre-treatment Auger</td>
                                <td class="p-3.5 font-mono text-brand-400">SS-310 High-Temp Steel</td>
                                <td class="p-3.5 font-mono text-amber-400">450°C continuous</td>
                                <td class="p-3.5 text-xs">Flash evaporation of paper sludge moisture content.</td>
                            </tr>
                            <tr>
                                <td class="p-3.5 font-semibold text-white">Dual Cyclone Separator</td>
                                <td class="p-3.5 font-mono text-brand-400">SS-316L Stainless</td>
                                <td class="p-3.5 font-mono text-amber-400">600°C</td>
                                <td class="p-3.5 text-xs">Centrifugal extraction of fine fly ash and particulates.</td>
                            </tr>
                            <tr>
                                <td class="p-3.5 font-semibold text-white">Venturi Wet Scrubber Assembly</td>
                                <td class="p-3.5 font-mono text-brand-400">Hastelloy C-276 Liner</td>
                                <td class="p-3.5 font-mono text-amber-400">99.8% filtration</td>
                                <td class="p-3.5 text-xs">Removal of acidic gases, water-soluble tars, and chlorine traces.</td>
                            </tr>
                            <tr>
                                <td class="p-3.5 font-semibold text-white">20 MW Syngas Power Turbine</td>
                                <td class="p-3.5 font-mono text-brand-400">Heavy Industrial Gas Turbine</td>
                                <td class="p-3.5 font-mono text-emerald-400">20.0 MW continuous</td>
                                <td class="p-3.5 text-xs">High-efficiency power generation fed into paper mill microgrid.</td>
                            </tr>
                        </tbody>
                    </table>
                </div>
            </div>
        </section>

        <!-- PAGE 6: ADMIN MASTER DATABASE (Gated) -->
        <section id="page-admindb" class="hidden space-y-8">
            <div class="flex items-center justify-between">
                <div>
                    <div class="inline-flex items-center gap-2 px-3 py-1 rounded-full bg-amber-500/10 border border-amber-500/30 text-amber-400 text-xs font-mono mb-2">
                        <i class="fa-solid fa-lock text-amber-500"></i> MASTER SECURITY ACCESS GRANTED
                    </div>
                    <h2 class="text-2xl font-bold text-white">Project Eklavya - Admin Master Database</h2>
                </div>
                <button onclick="exportAdminSessionCSV()" class="px-4 py-2 rounded-xl bg-emerald-600 hover:bg-emerald-500 text-white text-xs font-bold transition-all flex items-center gap-2">
                    <i class="fa-solid fa-file-csv"></i> Export Session Logs CSV
                </button>
            </div>

            <!-- Admin KPIs -->
            <div class="grid grid-cols-2 md:grid-cols-4 gap-4">
                <div class="glass-panel p-4 rounded-xl">
                    <div class="text-xs text-gray-400 font-mono">System Status</div>
                    <div class="text-lg font-bold text-brand-400 font-mono">ONLINE / OPTIMAL</div>
                </div>
                <div class="glass-panel p-4 rounded-xl">
                    <div class="text-xs text-gray-400 font-mono">Total Platform Users</div>
                    <div id="admin-user-count" class="text-lg font-bold text-white font-mono">1</div>
                </div>
                <div class="glass-panel p-4 rounded-xl">
                    <div class="text-xs text-gray-400 font-mono">Master Security Key</div>
                    <div class="text-xs font-mono text-amber-400 truncate">eklavyaisthebest15_18_15_28_22_best_devs</div>
                </div>
                <div class="glass-panel p-4 rounded-xl">
                    <div class="text-xs text-gray-400 font-mono">20 MW Fleet Duty</div>
                    <div class="text-lg font-bold text-cyan-400 font-mono">20 Hours / Day</div>
                </div>
            </div>

            <!-- Registered Sessions Table -->
            <div class="glass-panel p-6 rounded-2xl">
                <h3 class="text-lg font-bold text-white mb-4">User Activity & Session Tracking Logs</h3>
                <div class="overflow-x-auto">
                    <table class="w-full text-left text-sm border-collapse">
                        <thead>
                            <tr class="border-b border-gray-800 text-xs font-mono uppercase text-gray-400 bg-gray-900/50">
                                <th class="p-3">User ID</th>
                                <th class="p-3">Name</th>
                                <th class="p-3">Email / Mill Name</th>
                                <th class="p-3">Role</th>
                                <th class="p-3">Last Active (IST)</th>
                            </tr>
                        </thead>
                        <tbody id="admin-sessions-body" class="divide-y divide-gray-800/60 text-gray-300">
                            <!-- JS Populated -->
                        </tbody>
                    </table>
                </div>
            </div>
        </section>

    </main>

    <!-- Floating AI Chatbot Operator Component -->
    <div class="fixed bottom-6 right-6 z-50">
        <!-- Chatbot Trigger Button -->
        <button onclick="toggleChatbot()" id="chat-toggle-btn" class="w-14 h-14 rounded-full bg-gradient-to-tr from-brand-600 to-emerald-400 text-white flex items-center justify-center shadow-2xl hover:scale-105 transition-all">
            <i class="fa-solid fa-robot text-xl"></i>
        </button>

        <!-- Chatbot Window -->
        <div id="chatbot-window" class="hidden absolute bottom-16 right-0 w-80 sm:w-96 h-[480px] glass-panel rounded-2xl shadow-2xl border border-gray-800 flex flex-col overflow-hidden">
            <!-- Header -->
            <div class="p-4 bg-gray-900/90 border-b border-gray-800 flex items-center justify-between">
                <div class="flex items-center gap-2.5">
                    <div class="w-8 h-8 rounded-lg bg-brand-500/20 text-brand-400 flex items-center justify-center font-bold text-sm">
                        <i class="fa-solid fa-brain"></i>
                    </div>
                    <div>
                        <div class="text-xs font-bold text-white">EKLAVYA AI OPERATOR</div>
                        <div class="text-[10px] text-brand-400 font-mono">10,000+ Paper Waste Trained</div>
                    </div>
                </div>
                <button onclick="toggleChatbot()" class="text-gray-400 hover:text-white">
                    <i class="fa-solid fa-xmark"></i>
                </button>
            </div>

            <!-- Messages Log -->
            <div id="chat-messages" class="flex-grow p-4 overflow-y-auto space-y-3 text-xs">
                <div class="p-3 rounded-xl bg-gray-900/80 border border-gray-800 text-gray-200">
                    Hello! I am your Project Eklavya AI technical assistant. Ask me anything about paper sludge, 450°C pyrolysis, wet scrubbers, ₹20 Lakh pricing, or 20 MW plant operations.
                </div>
            </div>

            <!-- Input Box -->
            <div class="p-3 bg-gray-900/90 border-t border-gray-800 flex gap-2">
                <input type="text" id="chat-input" onkeydown="if(event.key==='Enter') sendChatMessage()" placeholder="Ask AI Operator..." class="flex-grow bg-gray-950 border border-gray-700 rounded-xl px-3 py-2 text-xs text-white focus:outline-none focus:border-brand-500">
                <button onclick="sendChatMessage()" class="px-3 py-2 rounded-xl bg-brand-600 hover:bg-brand-500 text-white text-xs font-bold transition-all">
                    <i class="fa-solid fa-paper-plane"></i>
                </button>
            </div>
        </div>
    </div>

    <!-- Login / Registration Modal -->
    <div id="auth-modal" class="hidden fixed inset-0 z-50 bg-black/70 backdrop-blur-sm flex items-center justify-center p-4">
        <div class="glass-panel w-full max-w-md rounded-2xl p-6 border border-gray-800 relative">
            <button onclick="closeAuthModal()" class="absolute top-4 right-4 text-gray-400 hover:text-white">
                <i class="fa-solid fa-xmark"></i>
            </button>

            <!-- Unauthenticated Form -->
            <div id="auth-form-container">
                <h3 class="text-xl font-bold text-white mb-1" id="auth-title">Login to Eklavya</h3>
                <p class="text-xs text-gray-400 mb-6">Access saved calculations & Master DB permissions.</p>

                <div class="space-y-4">
                    <div id="field-name-container" class="hidden">
                        <label class="block text-xs font-medium text-gray-400 mb-1">Full Name / Mill Name</label>
                        <input type="text" id="auth-name" placeholder="Star Paper Mill Pvt Ltd" class="w-full bg-gray-900 border border-gray-700 rounded-xl px-4 py-2.5 text-sm text-white focus:outline-none focus:border-brand-500">
                    </div>

                    <div>
                        <label class="block text-xs font-medium text-gray-400 mb-1">Email Address</label>
                        <input type="email" id="auth-email" placeholder="plantmanager@papermill.com" class="w-full bg-gray-900 border border-gray-700 rounded-xl px-4 py-2.5 text-sm text-white focus:outline-none focus:border-brand-500">
                    </div>

                    <div>
                        <label class="block text-xs font-medium text-gray-400 mb-1">Master Key / Password</label>
                        <input type="password" id="auth-key" placeholder="Enter key for Admin DB..." class="w-full bg-gray-900 border border-gray-700 rounded-xl px-4 py-2.5 text-sm text-white focus:outline-none focus:border-brand-500">
                        <p class="text-[10px] text-gray-500 mt-1">Hint: Use master security key for automatic Admin access.</p>
                    </div>

                    <button onclick="submitAuth()" class="w-full py-3 rounded-xl bg-brand-600 hover:bg-brand-500 text-white font-bold text-sm transition-all mt-2">
                        Submit
                    </button>

                    <div class="text-center text-xs text-gray-400 mt-4">
                        <span id="auth-switch-text">Need an account?</span>
                        <button onclick="toggleAuthMode()" id="auth-switch-btn" class="text-brand-400 font-semibold underline ml-1">Register</button>
                    </div>
                </div>
            </div>

            <!-- Authenticated Profile View -->
            <div id="auth-logged-container" class="hidden text-center space-y-4">
                <div class="w-16 h-16 rounded-full bg-emerald-600 text-white font-bold text-2xl flex items-center justify-center mx-auto border-4 border-brand-400" id="modal-avatar">
                    U
                </div>
                <div>
                    <h4 class="text-lg font-bold text-white" id="modal-user-name">User Name</h4>
                    <p class="text-xs text-gray-400" id="modal-user-email">email@paper.com</p>
                </div>
                <div class="pt-4 border-t border-gray-800 flex justify-center gap-3">
                    <button onclick="logoutUser()" class="px-4 py-2 rounded-xl bg-red-600/20 hover:bg-red-600/40 text-red-400 text-xs font-bold transition-all">
                        Logout
                    </button>
                    <button onclick="closeAuthModal()" class="px-4 py-2 rounded-xl bg-gray-800 hover:bg-gray-700 text-gray-300 text-xs font-bold transition-all">
                        Close
                    </button>
                </div>
            </div>
        </div>
    </div>

    <!-- JavaScript Application Logic -->
    <script>
        // --- MASTER CONFIGURATION & STATE ---
        const MASTER_SECURITY_KEY = "eklavyaisthebest15_18_15_28_22_best_devs";
        let currentLang = 'EN';
        let currentUnit = 'tonnes'; // 'tonnes' or 'kg'
        let currentUser = null;
        let isAuthRegisterMode = false;
        let threeScene, threeCamera, threeRenderer, threeControls, threeComponents = {};
        let savingsChart = null;

        // --- BILINGUAL DICTIONARY ---
        const translations = {
            EN: {
                nav_home: "Home", nav_3d: "3D CAD Model", nav_calc: "Calculator", nav_diagrams: "Schematics",
                nav_pricing: "Price & Specs", nav_admin: "Admin DB", btn_login: "Login",
                hero_badge: "20 MW Industrial Scale Energy Recovery System",
                hero_desc: "Project Eklavya engineered a high-efficiency thermochemical gasification framework tailored explicitly for paper and pulp mill waste streams—enabling continuously synchronized 20 hours/day operating cycles with zero toxic residue.",
                hero_btn_calc: "Calculate Mill Yield", hero_btn_3d: "Explore 3D Plant Model",
                stat_capacity: "Nominal Capacity", stat_duty: "Daily Duty Cycle", stat_temp: "Pyrolysis Core Temp", stat_time: "IST Live Telemetry",
                prob_title: "Paper Industry Sludge Challenge", prob_1: "High moisture paper sludge (40-60% wet pulp) costly to haul to landfills.",
                prob_2: "Deinking residues and OCC fiber tailings produce toxic leachate and methane gases.", prob_3: "Rising grid electricity tariffs strain mill operational margins during 24/7 paper production.",
                sol_title: "Project Eklavya Solution", sol_1: "Dual-auger pyrolysis pre-treatment at 450°C rapidly flash-dries wet paper sludge.",
                sol_2: "Thermochemical cracking yields clean syngas for direct power in a 20 MW turbine.", sol_3: "Dual Cyclone & Venturi Scrubbers filter 99.8% tar & particulate emissions.",
                db_title: "Paper Industry Waste Feedstock Master Database", db_subtitle: "1,000+ Indexed Paper & Pulp Waste Stream Profiles & Thermochemical Parameters",
                workflow_title: "Integrated 7-Stage Waste-to-Energy Flow", title_3d: "20 MW Gasification Skid 3D WebGL Inspector",
                sub_3d: "Interactive 3D CAD representation of Inconel-600 core, auger pyrolysis unit, cyclone & Venturi scrubbers.",
                calc_title: "Paper Waste Energy Yield & ROI Calculator", calc_sub: "Calibrated specifically for paper sludge, fiber tailings, and deinking residues based on 20 Hours/Day plant operation.",
                calc_input_title: "Feedstock Input", calc_feedstock_qty: "Daily Feedstock Quantity", calc_select_type: "Paper Feedstock Category",
                calc_tariff: "Grid Electricity Cost (₹ / kWh)", out_kwh: "Daily Power Output", out_syngas: "Syngas Generated",
                out_biochar: "Biochar By-product", out_savings: "Daily Monetary Savings", out_co2: "CO2 Emissions Offset",
                out_mill_duty: "Mill Duty Coverage", chart_title: "Estimated Monthly Mill Energy Savings vs Feedstock Scale (₹ Lakhs)",
                diagrams_title: "High-Contrast Technical Schematics", diagrams_sub: "Detailed engineering flow diagrams for 450°C pyrolysis pre-treatment and dual scrubbing stages.",
                diag1_title: "450°C Dual-Auger Pyrolysis Pre-treatment", diag2_title: "Dual Cyclone & Venturi Wet Scrubber Assembly",
                price_title: "Turnkey Unit Commercial Pricing & Engineering Specifications", price_sub: "Fixed commercial deployment cost and full bill of materials for paper industry gasifiers.",
                specs_table_title: "Technical Component Specification Sheet"
            },
            HI: {
                nav_home: "मुख्य पृष्ठ", nav_3d: "3D मॉडल", nav_calc: "कैलकुलेटर", nav_diagrams: "आरेख",
                nav_pricing: "मूल्य और विनिर्देश", nav_admin: "एडमिन डेटाबेस", btn_login: "लॉगिन",
                hero_badge: "20 मेगावाट औद्योगिक अपशिष्ट ऊर्जा रिकवरी प्रणाली",
                hero_desc: "प्रोजेक्ट एकलव्य ने कागज और लुगदी मिल के कचरे के लिए एक उच्च दक्षता वाली गैसीकरण प्रणाली तैयार की है—जो प्रतिदिन 20 घंटे का निरंतर संचालन चक्र प्रदान करती है।",
                hero_btn_calc: "ऊर्जा उपज की गणना करें", hero_btn_3d: "3D प्लांट मॉडल देखें",
                stat_capacity: "क्षमता", stat_duty: "दैनिक कार्य चक्र", stat_temp: "पायरोलिसिस तापमान", stat_time: "भारतीय मानक समय (IST)",
                prob_title: "कागज उद्योग की चुनौतियाँ", prob_1: "उच्च नमी वाले कागज के कीचड़ (40-60% गीला लुगदी) का निपटान महंगा है।",
                prob_2: "डी-इंकिंग अवशेष और ओसीसी फाइबर कचरा जहरीली गैसें उत्पन्न करते हैं।", prob_3: "बिजली की बढ़ती दरें 24/7 मिल संचालन को प्रभावित करती हैं।",
                sol_title: "प्रोजेक्ट एकलव्य समाधान", sol_1: "450°C पर डुअल-ऑगर पायरोलिसिस गीले कीचड़ को तेजी से सुखाता है।",
                sol_2: "1050°C गैसीकरण से 20 मेगावाट टर्बाइन के लिए स्वच्छ सिनगैस प्राप्त होती है।", sol_3: "ड्यूल साइक्लोन और वेंचुरी स्क्रबर्स 99.8% हानिकारक उत्सर्जन को फ़िल्टर करते हैं।",
                db_title: "कागज उद्योग अपशिष्ट मास्टर डेटाबेस", db_subtitle: "1,000+ अनुक्रमित कागज और लुगदी अपशिष्ट प्रोफाइल",
                workflow_title: "एककीकृत 7-चरण अपशिष्ट से ऊर्जा प्रवाह", title_3d: "20 मेगावाट गैसीकरण स्किड 3D निरीक्षक",
                sub_3d: "इनकोनेल-600 कोर, पायरोलिसिस यूनिट और वेंचुरी स्क्रबर्स का इंटरएक्टिव 3D CAD दृश्य।",
                calc_title: "कागज अपशिष्ट ऊर्जा और लाभ कैलकुलेटर", calc_sub: "20 घंटे/दिन के संयंत्र संचालन के आधार पर कैलिब्रेटेड।",
                calc_input_title: "कच्चा माल इनपुट", calc_feedstock_qty: "दैनिक कच्चा माल मात्रा", calc_select_type: "कागज अपशिष्ट श्रेणी",
                calc_tariff: "ग्रिड बिजली लागत (₹ / kWh)", out_kwh: "दैनिक बिजली उत्पादन", out_syngas: "उत्पन्न सिनगैस",
                out_biochar: "बायोचार उप-उत्पाद", out_savings: "दैनिक मौद्रिक बचत", out_co2: "CO2 उत्सर्जन में कमी",
                out_mill_duty: "मिल संचालन कवरेज", chart_title: "अनुमानित मासिक बचत (₹ लाख)",
                diagrams_title: "तकनीकी आरेख", diagrams_sub: "450°C पायरोलिसिस और स्क्रबर असेंबली के इंजीनियरिंग फ्लो डायग्राम।",
                diag1_title: "450°C डुअल-ऑगर पायरोलिसिस पूर्व-उपचार", diag2_title: "ड्यूल साइक्लोन और वेंचुरी वेट स्क्रबर असेंबली",
                price_title: "वाणिज्यिक मूल्य निर्धारण और इंजीनियरिंग विनिर्देश", price_sub: "टर्नकी इकाई लागत और तकनीकी घटक ब्रेकडाउन।",
                specs_table_title: "तकनीकी घटक विनिर्देश पत्रक"
            }
        };

        // --- SAMPLE PAPER WASTE DATABASE DATA ---
        const wasteDbSample = [
            { code: "P-SLUDGE-01", name: "Primary Paper Mill Sludge", moisture: "48%", cv: "11.2 MJ/kg", yield: "380 m³/t", biochar: "140 kg/t", status: "Ideal" },
            { code: "P-DEINK-04", name: "Deinked Paper Fiber Residue", moisture: "35%", cv: "14.5 MJ/kg", yield: "450 m³/t", biochar: "110 kg/t", status: "Optimal" },
            { code: "P-OCC-09", name: "Old Corrugated Box (OCC) Rejects", moisture: "20%", cv: "16.8 MJ/kg", yield: "520 m³/t", biochar: "95 kg/t", status: "Optimal" },
            { code: "P-BARK-12", name: "Timber Chipping & Bark Residue", moisture: "42%", cv: "13.1 MJ/kg", yield: "410 m³/t", biochar: "180 kg/t", status: "Good" },
            { code: "P-SEC-02", name: "Biological Secondary Sludge", moisture: "55%", cv: "9.8 MJ/kg", yield: "320 m³/t", biochar: "160 kg/t", status: "Requires Pre-dry" }
        ];

        // --- APP INIT ON WINDOW LOAD ---
        window.onload = function() {
            startLiveIstClock();
            renderWasteDatabase(wasteDbSample);
            initThreeJSModel();
            initSavingsChart();
            runCalculation();
            checkSavedAuth();
        };

        // --- TAB SWITCHING LOGIC ---
        function switchTab(tabId) {
            const tabs = ['home', 'model3d', 'calculator', 'diagrams', 'pricespecs', 'admindb'];
            tabs.forEach(id => {
                const page = document.getElementById(`page-${id}`);
                const nav = document.getElementById(`nav-${id}`);
                if (page) page.classList.add('hidden');
                if (nav) {
                    nav.classList.remove('text-brand-500', 'bg-gray-800/60', 'light:bg-gray-200', 'font-semibold');
                    nav.classList.add('text-gray-400');
                }
            });

            const targetPage = document.getElementById(`page-${tabId}`);
            const targetNav = document.getElementById(`nav-${tabId}`);
            if (targetPage) targetPage.classList.remove('hidden');
            if (targetNav) {
                targetNav.classList.remove('text-gray-400');
                targetNav.classList.add('text-brand-500', 'bg-gray-800/60', 'light:bg-gray-200', 'font-semibold');
            }

            if (tabId === 'model3d' && threeControls) {
                setTimeout(() => { onWindowResize(); }, 100);
            }
        }

        function handleAdminTabClick() {
            if (currentUser && currentUser.isAdmin) {
                switchTab('admindb');
                renderAdminLogs();
            } else {
                openAuthModal();
            }
        }

        // --- BILINGUAL & THEME TOGGLES ---
        function toggleLanguage() {
            currentLang = currentLang === 'EN' ? 'HI' : 'EN';
            document.getElementById('lang-indicator').innerText = currentLang;

            document.querySelectorAll('[data-i18n]').forEach(el => {
                const key = el.getAttribute('data-i18n');
                if (translations[currentLang][key]) {
                    el.innerText = translations[currentLang][key];
                }
            });
        }

        function toggleTheme() {
            document.documentElement.classList.toggle('dark');
            document.documentElement.classList.toggle('light');
        }

        // --- LIVE IST TELEMETRY CLOCK ---
        function startLiveIstClock() {
            setInterval(() => {
                const now = new Date();
                const istOffset = 5.5 * 60 * 60 * 1000;
                const istTime = new Date(now.getTime() + (now.getTimezoneOffset() * 60000) + istOffset);
                const clockEl = document.getElementById('live-ist-time');
                if (clockEl) {
                    clockEl.innerText = istTime.toLocaleTimeString('en-IN') + ' IST';
                }
            }, 1000);
        }

        // --- WASTE DATABASE FILTER ---
        function renderWasteDatabase(data) {
            const tbody = document.getElementById('waste-db-body');
            tbody.innerHTML = '';
            data.forEach(item => {
                const tr = document.createElement('tr');
                tr.className = "hover:bg-gray-800/30 transition-colors";
                tr.innerHTML = `
                    <td class="p-3 font-mono text-xs text-brand-400 font-bold">${item.code}</td>
                    <td class="p-3 font-semibold text-white">${item.name}</td>
                    <td class="p-3 font-mono text-xs">${item.moisture}</td>
                    <td class="p-3 font-mono text-xs text-amber-400">${item.cv}</td>
                    <td class="p-3 font-mono text-xs text-cyan-400">${item.yield}</td>
                    <td class="p-3 font-mono text-xs">${item.biochar}</td>
                    <td class="p-3"><span class="px-2 py-0.5 rounded text-[10px] font-mono bg-brand-500/20 text-brand-300 border border-brand-500/30">${item.status}</span></td>
                `;
                tbody.appendChild(tr);
            });
        }

        function filterWasteDb() {
            const query = document.getElementById('db-search-input').value.toLowerCase();
            const filtered = wasteDbSample.filter(i =>
                i.name.toLowerCase().includes(query) ||
                i.code.toLowerCase().includes(query)
            );
            renderWasteDatabase(filtered);
        }

        // --- 3D WEBGL CAD MODEL (THREE.JS) ---
        function initThreeJSModel() {
            const container = document.getElementById('threejs-canvas-container');
            if (!container) return;

            threeScene = new THREE.Scene();
            threeScene.background = new THREE.Color(0x030712);

            threeCamera = new THREE.PerspectiveCamera(45, container.clientWidth / container.clientHeight, 0.1, 1000);
            threeCamera.position.set(25, 18, 30);

            threeRenderer = new THREE.WebGLRenderer({ antialias: true });
            threeRenderer.setSize(container.clientWidth, container.clientHeight);
            threeRenderer.shadowMap.enabled = true;
            container.appendChild(threeRenderer.domElement);

            threeControls = new THREE.OrbitControls(threeCamera, threeRenderer.domElement);
            threeControls.enableDamping = true;

            // Lighting
            const ambientLight = new THREE.AmbientLight(0xffffff, 0.6);
            threeScene.add(ambientLight);

            const dirLight = new THREE.DirectionalLight(0x22c55e, 1.2);
            dirLight.position.set(20, 40, 20);
            threeScene.add(dirLight);

            // Ground Grid
            const gridHelper = new THREE.GridHelper(50, 50, 0x16a34a, 0x1f2937);
            threeScene.add(gridHelper);

            // Create 20 MW Gasification Components
            // 1. Hopper
            const hopperGeo = new THREE.CylinderGeometry(2, 0.8, 3, 16);
            const hopperMat = new THREE.MeshStandardMaterial({ color: 0x4b5563, metalness: 0.8 });
            const hopper = new THREE.Mesh(hopperGeo, hopperMat);
            hopper.position.set(-12, 4.5, 0);
            threeScene.add(hopper);
            threeComponents.hopper = hopper;

            // 2. Pyrolysis Auger Chamber
            const augerGeo = new THREE.CylinderGeometry(1, 1, 8, 16);
            const augerMat = new THREE.MeshStandardMaterial({ color: 0xd97706, metalness: 0.9, roughness: 0.3 });
            const auger = new THREE.Mesh(augerGeo, augerMat);
            auger.rotation.z = Math.PI / 2;
            auger.position.set(-7, 2, 0);
            threeScene.add(auger);
            threeComponents.auger = auger;

            // 3. Main Gasifier Core (Inconel-600)
            const coreGeo = new THREE.CylinderGeometry(2.5, 2.5, 9, 32);
            const coreMat = new THREE.MeshStandardMaterial({ color: 0x16a34a, metalness: 0.9, roughness: 0.2 });
            const core = new THREE.Mesh(coreGeo, coreMat);
            core.position.set(0, 4.5, 0);
            threeScene.add(core);
            threeComponents.core = core;

            // 4. Cyclone Scrubber
            const cycloneGeo = new THREE.CylinderGeometry(1.2, 0.3, 5, 16);
            const cycloneMat = new THREE.MeshStandardMaterial({ color: 0x06b6d4, metalness: 0.8 });
            const cyclone = new THREE.Mesh(cycloneGeo, cycloneMat);
            cyclone.position.set(6, 3.5, 0);
            threeScene.add(cyclone);
            threeComponents.cyclone = cyclone;

            // 5. Venturi Scrubber Tower
            const towerGeo = new THREE.CylinderGeometry(1.5, 1.5, 7, 24);
            const towerMat = new THREE.MeshStandardMaterial({ color: 0x0284c7, metalness: 0.7 });
            const tower = new THREE.Mesh(towerGeo, towerMat);
            tower.position.set(11, 4.5, 0);
            threeScene.add(tower);
            threeComponents.tower = tower;

            // 6. 20 MW Turbine Generator
            const turbGeo = new THREE.BoxGeometry(6, 3, 4);
            const turbMat = new THREE.MeshStandardMaterial({ color: 0x9333ea, metalness: 0.8 });
            const turbine = new THREE.Mesh(turbGeo, turbMat);
            turbine.position.set(18, 2, 0);
            threeScene.add(turbine);
            threeComponents.turbine = turbine;

            // Raycasting for object selection
            const raycaster = new THREE.Raycaster();
            const mouse = new THREE.Vector2();

            container.addEventListener('click', (event) => {
                const rect = container.getBoundingClientRect();
                mouse.x = ((event.clientX - rect.left) / container.clientWidth) * 2 - 1;
                mouse.y = -((event.clientY - rect.top) / container.clientHeight) * 2 + 1;

                raycaster.setFromCamera(mouse, threeCamera);
                const intersects = raycaster.intersectObjects(threeScene.children);

                if (intersects.length > 0) {
                    const hitObj = intersects[0].object;
                    inspectComponent(hitObj);
                }
            });

            window.addEventListener('resize', onWindowResize);
            animate3D();
        }

        function animate3D() {
            requestAnimationFrame(animate3D);
            if (threeControls) threeControls.update();
            if (threeScene) {
                // Gentle rotation of the core highlight
                if (threeComponents.core) threeComponents.core.rotation.y += 0.005;
            }
            if (threeRenderer && threeScene && threeCamera) {
                threeRenderer.render(threeScene, threeCamera);
            }
        }

        function onWindowResize() {
            const container = document.getElementById('threejs-canvas-container');
            if (!container || !threeCamera || !threeRenderer) return;
            threeCamera.aspect = container.clientWidth / container.clientHeight;
            threeCamera.updateProjectionMatrix();
            threeRenderer.setSize(container.clientWidth, container.clientHeight);
        }

        function reset3DCamera() {
            if (threeCamera && threeControls) {
                threeCamera.position.set(25, 18, 30);
                threeControls.target.set(0, 3, 0);
            }
        }

        function toggle3DLight() {
            // Light toggle stub
        }

        function inspectComponent(obj) {
            const tag = document.getElementById('inspector-tag');
            const title = document.getElementById('inspector-title');
            const desc = document.getElementById('inspector-desc');
            const temp = document.getElementById('spec-temp');
            const mat = document.getElementById('spec-material');
            const eff = document.getElementById('spec-eff');

            if (obj === threeComponents.hopper) {
                title.innerText = "Feed Hopper Sub-System";
                desc.innerText = "Hydraulic sealed feed hopper designed for continuous paper sludge infeed with air-lock system.";
                temp.innerText = "Ambient (25°C)"; mat.innerText = "Carbon Steel A36"; eff.innerText = "99.9% Feed Rate";
            } else if (obj === threeComponents.auger) {
                title.innerText = "450°C Dual-Auger Pyrolysis Reactor";
                desc.innerText = "Flash dries moisture from paper pulp sludge before thermal gasification cracking.";
                temp.innerText = "450 °C"; mat.innerText = "SS-310 Stainless"; eff.innerText = "95% Thermal Sync";
            } else if (obj === threeComponents.core) {
                title.innerText = "Inconel-600 Gasifier Core";
                desc.innerText = "1050°C primary thermochemical reactor converting organic paper fibers into CO & H2 syngas.";
                temp.innerText = "1050 °C"; mat.innerText = "Inconel-600 Alloy"; eff.innerText = "98.5% Conversion";
            } else if (obj === threeComponents.cyclone || obj === threeComponents.tower) {
                title.innerText = "Dual Cyclone & Venturi Wet Scrubber";
                desc.innerText = "Multi-stage gas cleanup unit removing fly ash, particulate matter, and water-soluble tars.";
                temp.innerText = "80 °C - 150 °C"; mat.innerText = "Hastelloy / SS-316L"; eff.innerText = "99.8% Cleanliness";
            } else if (obj === threeComponents.turbine) {
                title.innerText = "20 MW Syngas Turbine Generator";
                desc.innerText = "Heavy industrial gas turbine converting clean syngas directly into mill microgrid power.";
                temp.innerText = "550 °C Exhaust"; mat.innerText = "Nickel Superalloy"; eff.innerText = "20.0 MW Output";
            }
        }

        // --- CALCULATOR LOGIC ---
        function setCalcUnit(unit) {
            currentUnit = unit;
            const btnTonnes = document.getElementById('unit-tonnes');
            const btnKg = document.getElementById('unit-kg');
            const sliderMaxLabel = document.getElementById('slider-max-label');
            const slider = document.getElementById('calc-slider');

            if (unit === 'tonnes') {
                btnTonnes.className = "px-3 py-1 rounded-lg text-xs font-semibold bg-brand-600 text-white transition-all";
                btnKg.className = "px-3 py-1 rounded-lg text-xs font-semibold text-gray-400 hover:text-white transition-all";
                sliderMaxLabel.innerText = "100 Tonnes";
                slider.max = 100;
                document.getElementById('calc-input-qty').value = 50;
            } else {
                btnKg.className = "px-3 py-1 rounded-lg text-xs font-semibold bg-brand-600 text-white transition-all";
                btnTonnes.className = "px-3 py-1 rounded-lg text-xs font-semibold text-gray-400 hover:text-white transition-all";
                sliderMaxLabel.innerText = "100,000 kg";
                slider.max = 100000;
                document.getElementById('calc-input-qty').value = 50000;
            }
            syncCalcInputs('number');
        }

        function syncCalcInputs(source) {
            const numInput = document.getElementById('calc-input-qty');
            const slider = document.getElementById('calc-slider');

            if (source === 'number') {
                slider.value = numInput.value;
            } else {
                numInput.value = slider.value;
            }
            runCalculation();
        }

        function runCalculation() {
            let qty = parseFloat(document.getElementById('calc-input-qty').value) || 0;
            if (currentUnit === 'kg') qty = qty / 1000; // Convert to tonnes for calc baseline

            const wasteType = document.getElementById('calc-waste-type').value;
            const tariff = parseFloat(document.getElementById('calc-tariff').value) || 8.5;

            // Multipliers
            let kwhPerTon = 2500;
            let syngasPerTon = 350;
            let biocharPerTon = 0.15;

            if (wasteType === 'occ') { kwhPerTon = 3200; syngasPerTon = 450; biocharPerTon = 0.10; }
            else if (wasteType === 'deinked') { kwhPerTon = 2800; syngasPerTon = 400; biocharPerTon = 0.12; }
            else if (wasteType === 'woodbark') { kwhPerTon = 2600; syngasPerTon = 370; biocharPerTon = 0.18; }

            const totalKwh = qty * kwhPerTon;
            const totalSyngas = qty * syngasPerTon;
            const totalBiochar = qty * biocharPerTon;
            const dailySavings = totalKwh * tariff;
            const co2Offset = qty * 2.05;
            const millHours = Math.min(20.0, (qty / 50) * 20.0);

            // Update DOM
            document.getElementById('out-kwh').innerText = totalKwh.toLocaleString('en-IN') + ' kWh';
            document.getElementById('out-syngas').innerText = totalSyngas.toLocaleString('en-IN') + ' m³';
            document.getElementById('out-biochar').innerText = totalBiochar.toFixed(1) + ' Tonnes';
            document.getElementById('out-savings').innerText = '₹' + Math.round(dailySavings).toLocaleString('en-IN');
            document.getElementById('out-co2').innerText = co2Offset.toFixed(1) + ' Tonnes';
            document.getElementById('out-duty').innerText = millHours.toFixed(1) + ' Hours/Day';

            updateSavingsChart(qty, tariff, kwhPerTon);
        }

        // --- CHART.JS SAVINGS VISUALIZER ---
        function initSavingsChart() {
            const ctx = document.getElementById('calc-savings-chart');
            if (!ctx) return;

            savingsChart = new Chart(ctx, {
                type: 'bar',
                data: {
                    labels: ['10 Tons', '25 Tons', '50 Tons', '75 Tons', '100 Tons'],
                    datasets: [{
                        label: 'Monthly Savings (₹ Lakhs)',
                        data: [15, 37.5, 75, 112.5, 150],
                        backgroundColor: '#22c55e',
                        borderRadius: 8
                    }]
                },
                options: {
                    responsive: true,
                    maintainAspectRatio: false,
                    plugins: { legend: { labels: { color: '#9ca3af' } } },
                    scales: {
                        x: { ticks: { color: '#9ca3af' }, grid: { color: '#1f2937' } },
                        y: { ticks: { color: '#9ca3af' }, grid: { color: '#1f2937' } }
                    }
                }
            });
        }

        function updateSavingsChart(currentQty, tariff, kwhPerTon) {
            if (!savingsChart) return;
            const scales = [10, 25, 50, 75, 100];
            const dataLakhs = scales.map(s => ((s * kwhPerTon * tariff * 30) / 100000).toFixed(1));

            savingsChart.data.datasets[0].data = dataLakhs;
            savingsChart.update();
        }

        // --- AUTHENTICATION & LOGIN MODAL ---
        function openAuthModal() {
            document.getElementById('auth-modal').classList.remove('hidden');
        }

        function closeAuthModal() {
            document.getElementById('auth-modal').classList.add('hidden');
        }

        function toggleAuthMode() {
            isAuthRegisterMode = !isAuthRegisterMode;
            const nameField = document.getElementById('field-name-container');
            const title = document.getElementById('auth-title');
            const switchBtn = document.getElementById('auth-switch-btn');

            if (isAuthRegisterMode) {
                nameField.classList.remove('hidden');
                title.innerText = "Register Mill Profile";
                switchBtn.innerText = "Login";
            } else {
                nameField.classList.add('hidden');
                title.innerText = "Login to Eklavya";
                switchBtn.innerText = "Register";
            }
        }

        function submitAuth() {
            const email = document.getElementById('auth-email').value || "operator@papermill.com";
            const name = document.getElementById('auth-name').value || "Paper Mill Operator";
            const key = document.getElementById('auth-key').value;

            const isAdmin = (key === MASTER_SECURITY_KEY);

            currentUser = {
                name: name,
                email: email,
                isAdmin: isAdmin,
                loginTime: new Date().toLocaleTimeString('en-IN')
            };

            localStorage.setItem('eklavya_user', JSON.stringify(currentUser));
            updateUserUI();
            closeAuthModal();

            if (isAdmin) {
                switchTab('admindb');
                renderAdminLogs();
            }
        }

        function checkSavedAuth() {
            const saved = localStorage.getItem('eklavya_user');
            if (saved) {
                currentUser = JSON.parse(saved);
                updateUserUI();
            }
        }

        function updateUserUI() {
            if (currentUser) {
                document.getElementById('btn-login-trigger').classList.add('hidden');
                document.getElementById('user-profile-badge').classList.remove('hidden');
                document.getElementById('user-avatar-initial').innerText = currentUser.name.charAt(0).toUpperCase();
                document.getElementById('user-display-name').innerText = currentUser.name;

                document.getElementById('auth-form-container').classList.add('hidden');
                document.getElementById('auth-logged-container').classList.remove('hidden');
                document.getElementById('modal-avatar').innerText = currentUser.name.charAt(0).toUpperCase();
                document.getElementById('modal-user-name').innerText = currentUser.name;
                document.getElementById('modal-user-email').innerText = currentUser.email;
            }
        }

        function logoutUser() {
            currentUser = null;
            localStorage.removeItem('eklavya_user');
            document.getElementById('btn-login-trigger').classList.remove('hidden');
            document.getElementById('user-profile-badge').classList.add('hidden');
            document.getElementById('auth-form-container').classList.remove('hidden');
            document.getElementById('auth-logged-container').classList.add('hidden');
            switchTab('home');
            closeAuthModal();
        }

        // --- ADMIN DB RENDERING ---
        function renderAdminLogs() {
            const tbody = document.getElementById('admin-sessions-body');
            if (!tbody) return;

            tbody.innerHTML = `
                <tr class="hover:bg-gray-800/30">
                    <td class="p-3 font-mono text-xs text-brand-400">USR-8821</td>
                    <td class="p-3 font-semibold text-white">${currentUser ? currentUser.name : "Admin Operator"}</td>
                    <td class="p-3 font-mono text-xs text-gray-300">${currentUser ? currentUser.email : "admin@eklavya.org"}</td>
                    <td class="p-3"><span class="px-2 py-0.5 rounded text-[10px] font-mono bg-amber-500/20 text-amber-300 border border-amber-500/30">MASTER ADMIN</span></td>
                    <td class="p-3 font-mono text-xs text-cyan-400">${currentUser ? currentUser.loginTime : "10:30 AM IST"}</td>
                </tr>
            `;
        }

        function exportAdminSessionCSV() {
            const csvContent = "data:text/csv;charset=utf-8,User ID,Name,Email,Role,Login Time\nUSR-8821," +
                (currentUser ? currentUser.name : "Admin") + "," +
                (currentUser ? currentUser.email : "admin@eklavya.org") + ",Master Admin,10:30 AM IST";

            const encodedUri = encodeURI(csvContent);
            const link = document.createElement("a");
            link.setAttribute("href", encodedUri);
            link.setAttribute("download", "eklavya_admin_sessions.csv");
            document.body.appendChild(link);
            link.click();
            document.body.removeChild(link);
        }

        // --- AI CHATBOT OPERATOR ---
        function toggleChatbot() {
            const win = document.getElementById('chatbot-window');
            win.classList.toggle('hidden');
        }

        function sendChatMessage() {
            const input = document.getElementById('chat-input');
            const msg = input.value.trim();
            if (!msg) return;

            appendChatBubble(msg, 'user');
            input.value = '';

            setTimeout(() => {
                const response = generateAIResponse(msg);
                appendChatBubble(response, 'bot');
            }, 600);
        }

        function appendChatBubble(text, sender) {
            const container = document.getElementById('chat-messages');
            const div = document.createElement('div');
            if (sender === 'user') {
                div.className = "p-3 rounded-xl bg-brand-600 text-white ml-auto max-w-[80%] text-xs";
            } else {
                div.className = "p-3 rounded-xl bg-gray-900 border border-gray-800 text-gray-200 mr-auto max-w-[85%] text-xs space-y-1";
            }
            div.innerText = text;
            container.appendChild(div);
            container.scrollTop = container.scrollHeight;
        }

        function generateAIResponse(prompt) {
            const p = prompt.toLowerCase();
            if (p.includes('price') || p.includes('cost') || p.includes('lakh') || p.includes('₹')) {
                return "Project Eklavya's 20 MW turnkey gasification unit is commercially fixed at ₹20 Lakhs (₹20,00,000 / ~$24,000 USD). This offers an accelerated 1.5 to 3 month payback period.";
            } else if (p.includes('sludge') || p.includes('waste') || p.includes('moisture')) {
                return "Paper sludge typically contains 40-50% moisture. Our 450°C dual-auger pyrolysis pre-treatment flash dries wet fibers before entering the 1050°C Inconel-600 thermochemical core.";
            } else if (p.includes('scrubber') || p.includes('clean') || p.includes('tar')) {
                return "The plant utilizes a dual Cyclone and Venturi Wet Scrubber stage with Hastelloy lining, achieving 99.8% filtration efficiency for fly ash, chlorine, and tars.";
            } else if (p.includes('hours') || p.includes('duty') || p.includes('cycle')) {
                return "The system is engineered for synchronized 20 Hours/Day continuous operating duty, aligned with standard industrial paper mill batch shifts.";
            } else {
                return "Project Eklavya synthesizes paper industry waste (sludge, OCC, deinked residues) into clean 20 MW syngas power. Feel free to ask about our 450°C pyrolysis, ₹20 Lakh pricing, or calculators!";
            }
        }
    </script>
</body>
</html>
