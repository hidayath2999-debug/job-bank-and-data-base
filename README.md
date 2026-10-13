<!DOCTYPE html>
<html lang="en" class="scroll-smooth">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>JobVault Pro - Job Bank & Resume Database Platform</title>
    
    <!-- Tailwind CSS -->
    <script src="https://cdn.tailwindcss.com"></script>
    
    <!-- FontAwesome Icons -->
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    
    <!-- Google Fonts (Inter) -->
    <link rel="preconnect" href="https://fonts.googleapis.com">
    <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
    <link href="https://fonts.googleapis.com/css2?family=Inter:wght@300;400;500;600;700;800&display=swap" rel="stylesheet">

    <script>
        tailwind.config = {
            theme: {
                extend: {
                    colors: {
                        navy: {
                            800: '#0b132b',
                            900: '#070d1f',
                            950: '#030712'
                        },
                        teal: {
                            400: '#2dd4bf',
                            500: '#14b8a6',
                            600: '#0d9488',
                            700: '#0f766e'
                        }
                    },
                    fontFamily: {
                        sans: ['Inter', 'sans-serif']
                    }
                }
            }
        }
    </script>
    
    <style>
        /* Custom scrollbars and subtle ambient glow effects */
        ::-webkit-scrollbar {
            width: 8px;
        }
        ::-webkit-scrollbar-track {
            background: #070d1f;
        }
        ::-webkit-scrollbar-thumb {
            background: #1e293b;
            border-radius: 4px;
        }
        ::-webkit-scrollbar-thumb:hover {
            background: #0d9488;
        }
        .glow-effect {
            box-shadow: 0 0 25px -5px rgba(20, 184, 166, 0.25);
        }
        .glass-panel {
            background: rgba(15, 23, 42, 0.75);
            backdrop-filter: blur(12px);
            border: 1px solid rgba(255, 255, 255, 0.08);
        }
    </style>
</head>
<body class="bg-slate-950 text-slate-100 font-sans min-h-screen flex flex-col justify-between selection:bg-teal-500 selection:text-slate-950">

    <header class="sticky top-0 z-40 w-full glass-panel border-b border-slate-800/80">
        <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8 h-20 flex items-center justify-between">
            
            <!-- Brand Logo -->
            <div class="flex items-center space-x-3 cursor-pointer" onclick="switchView('jobs')">
                <div class="w-10 h-10 rounded-xl bg-gradient-to-tr from-teal-500 to-emerald-400 flex items-center justify-center text-slate-950 font-black text-xl shadow-lg shadow-teal-500/20">
                    <i class="fa-solid fa-vault"></i>
                </div>
                <div>
                    <span class="text-xl font-bold tracking-tight text-white">JobVault <span class="text-teal-400">Pro</span></span>
                    <span class="block text-[10px] text-slate-400 -mt-1 tracking-widest uppercase font-semibold">Enterprise Hiring</span>
                </div>
            </div>

            <!-- Desktop Navigation -->
            <nav class="hidden md:flex items-center space-x-8 text-sm font-medium text-slate-300">
                <button id="nav-jobs" onclick="switchView('jobs')" class="hover:text-teal-400 transition-colors py-2 border-b-2 border-teal-400 text-teal-400 font-semibold">Browse Jobs</button>
                <button id="nav-resumes" onclick="switchView('resumes')" class="hover:text-teal-400 transition-colors py-2 border-b-2 border-transparent">Resume Database <span class="ml-1 text-[10px] bg-teal-500/20 text-teal-300 px-1.5 py-0.5 rounded border border-teal-500/30">PRO</span></button>
                <a href="#pricing" class="hover:text-teal-400 transition-colors py-2">Pricing Plans</a>
                <button onclick="openSubscriptionModal('Recruiter Pro Tier', 149)" class="hover:text-teal-400 transition-colors py-2">Employer Portal</button>
            </nav>

            <!-- CTA Buttons -->
            <div class="hidden sm:flex items-center space-x-4">
                <button onclick="showToast('Signed in as Employer / Recruiter')" class="px-4 py-2 text-sm font-medium text-slate-300 hover:text-white transition-colors">Log In</button>
                <button onclick="openPostJobModal()" class="px-4 py-2 text-sm font-semibold rounded-lg bg-teal-500 hover:bg-teal-400 text-slate-950 transition-all transform active:scale-95 shadow-md shadow-teal-500/20">
                    <i class="fa-solid fa-plus mr-1.5"></i> Post a Job
                </button>
            </div>

            <!-- Mobile Hamburger Button -->
            <button id="mobile-menu-btn" onclick="toggleMobileMenu()" class="md:hidden text-slate-300 hover:text-white p-2">
                <i class="fa-solid fa-bars text-xl"></i>
            </button>
        </div>

        <!-- Mobile Menu Dropdown -->
        <div id="mobile-menu" class="hidden md:hidden bg-slate-900/95 border-b border-slate-800 px-4 pt-2 pb-6 space-y-3">
            <button onclick="switchView('jobs'); toggleMobileMenu();" class="block w-full text-left py-2 text-slate-200 hover:text-teal-400 font-medium">Browse Jobs</button>
            <button onclick="switchView('resumes'); toggleMobileMenu();" class="block w-full text-left py-2 text-slate-200 hover:text-teal-400 font-medium">Resume Database (Pro)</button>
            <a href="#pricing" onclick="toggleMobileMenu()" class="block py-2 text-slate-200 hover:text-teal-400 font-medium">Pricing Plans</a>
            <div class="pt-2 border-t border-slate-800 flex flex-col space-y-2">
                <button onclick="openPostJobModal(); toggleMobileMenu();" class="w-full py-2.5 rounded-lg bg-teal-500 text-slate-950 font-bold text-center">Post a Job</button>
            </div>
        </div>
    </header>

    <main class="flex-grow">
        <section class="relative bg-gradient-to-b from-navy-900 via-slate-950 to-slate-950 py-16 lg:py-24 px-4 overflow-hidden">
            <!-- Background Radial Glow -->
            <div class="absolute top-1/4 left-1/2 -translate-x-1/2 -translate-y-1/2 w-[600px] h-[300px] bg-teal-500/10 blur-[120px] rounded-full pointer-events-none"></div>

            <div class="max-w-5xl mx-auto text-center relative z-10">
                <span class="inline-flex items-center gap-2 px-3 py-1.5 rounded-full bg-teal-500/10 border border-teal-500/30 text-teal-300 text-xs font-semibold uppercase tracking-wider mb-6">
                    <span class="w-2 h-2 rounded-full bg-teal-400 animate-pulse"></span> Next-Gen Talent & Job Matching
                </span>
                
                <h1 id="hero-title" class="text-3xl sm:text-5xl lg:text-6xl font-extrabold tracking-tight text-white leading-tight">
                    Connecting Top Talent with <br class="hidden sm:inline"><span class="bg-gradient-to-r from-teal-400 via-emerald-400 to-cyan-400 bg-clip-text text-transparent">World-Class Tech Teams</span>
                </h1>
                
                <p id="hero-subtitle" class="mt-4 text-slate-400 text-base sm:text-lg max-w-2xl mx-auto">
                    Explore over 12,000+ verified active job postings or unlock our premium database of top 1% vetted developers, designers, and managers.
                </p>

                <!-- Search Component Card -->
                <div class="mt-8 bg-slate-900/90 border border-slate-800 p-3 sm:p-4 rounded-2xl shadow-2xl backdrop-blur-xl max-w-4xl mx-auto">
                    <form id="search-form" onsubmit="handleSearch(event)" class="grid grid-cols-1 sm:grid-cols-2 lg:grid-cols-4 gap-3">
                        <!-- Keyword Input -->
                        <div class="relative">
                            <i class="fa-solid fa-magnifying-glass absolute left-3.5 top-1/2 -translate-y-1/2 text-slate-500"></i>
                            <input type="text" id="search-keyword" placeholder="Job title, skill, or company" class="w-full bg-slate-950/80 border border-slate-800 focus:border-teal-500 focus:ring-1 focus:ring-teal-500 text-slate-200 text-sm rounded-xl pl-10 pr-3 py-3 outline-none transition-all placeholder:text-slate-500">
                        </div>

                        <!-- Category Select -->
                        <div class="relative">
                            <i class="fa-solid fa-layer-group absolute left-3.5 top-1/2 -translate-y-1/2 text-slate-500"></i>
                            <select id="search-category" class="w-full bg-slate-950/80 border border-slate-800 focus:border-teal-500 focus:ring-1 focus:ring-teal-500 text-slate-200 text-sm rounded-xl pl-10 pr-3 py-3 outline-none transition-all appearance-none">
                                <option value="">All Categories</option>
                                <option value="Engineering">Engineering</option>
                                <option value="Design">UI/UX & Design</option>
                                <option value="Product">Product Management</option>
                                <option value="Data">Data & AI</option>
                                <option value="Marketing">Marketing & Sales</option>
                            </select>
                            <i class="fa-solid fa-chevron-down absolute right-3.5 top-1/2 -translate-y-1/2 text-slate-500 text-xs pointer-events-none"></i>
                        </div>

                        <!-- Location Select -->
                        <div class="relative">
                            <i class="fa-solid fa-location-dot absolute left-3.5 top-1/2 -translate-y-1/2 text-slate-500"></i>
                            <select id="search-location" class="w-full bg-slate-950/80 border border-slate-800 focus:border-teal-500 focus:ring-1 focus:ring-teal-500 text-slate-200 text-sm rounded-xl pl-10 pr-3 py-3 outline-none transition-all appearance-none">
                                <option value="">Any Location</option>
                                <option value="Remote">Remote</option>
                                <option value="San Francisco, CA">San Francisco, CA</option>
                                <option value="New York, NY">New York, NY</option>
                                <option value="London, UK">London, UK</option>
                            </select>
                            <i class="fa-solid fa-chevron-down absolute right-3.5 top-1/2 -translate-y-1/2 text-slate-500 text-xs pointer-events-none"></i>
                        </div>

                        <!-- Submit Button -->
                        <div>
                            <button type="submit" class="w-full h-full bg-teal-500 hover:bg-teal-400 text-slate-950 font-bold text-sm rounded-xl py-3 px-6 transition-all flex items-center justify-center space-x-2 shadow-lg shadow-teal-500/20 active:scale-[0.98]">
                                <i class="fa-solid fa-filter"></i>
                                <span>Filter Results</span>
                            </button>
                        </div>
                    </form>
                </div>
            </div>
        </section>

        <section class="border-y border-slate-800/80 bg-slate-900/40 py-8 px-4">
            <div class="max-w-7xl mx-auto grid grid-cols-2 md:grid-cols-4 gap-6 text-center">
                <div class="p-3">
                    <p class="text-2xl sm:text-3xl font-extrabold text-white">12,850+</p>
                    <p class="text-xs sm:text-sm font-medium text-slate-400 mt-1"><i class="fa-solid fa-briefcase text-teal-400 mr-1.5"></i>Active Job Postings</p>
                </div>
                <div class="p-3">
                    <p class="text-2xl sm:text-3xl font-extrabold text-white">45,000+</p>
                    <p class="text-xs sm:text-sm font-medium text-slate-400 mt-1"><i class="fa-solid fa-id-card text-teal-400 mr-1.5"></i>Verified Resumes</p>
                </div>
                <div class="p-3">
                    <p class="text-2xl sm:text-3xl font-extrabold text-white">3,200+</p>
                    <p class="text-xs sm:text-sm font-medium text-slate-400 mt-1"><i class="fa-solid fa-building text-teal-400 mr-1.5"></i>Hiring Companies</p>
                </div>
                <div class="p-3">
                    <p class="text-2xl sm:text-3xl font-extrabold text-white">98.4%</p>
                    <p class="text-xs sm:text-sm font-medium text-slate-400 mt-1"><i class="fa-solid fa-circle-check text-teal-400 mr-1.5"></i>Placement Success</p>
                </div>
            </div>
        </section>

        <!-- Main Content Area: Tabs Container -->
        <section class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8 py-12">
            
            <!-- View Selector Tabs Switcher -->
            <div class="flex items-center justify-between border-b border-slate-800 pb-4 mb-8">
                <div class="flex space-x-3 bg-slate-900 p-1.5 rounded-xl border border-slate-800">
                    <button id="tab-jobs-btn" onclick="switchView('jobs')" class="px-5 py-2.5 rounded-lg text-sm font-bold transition-all bg-teal-500 text-slate-950 shadow-md">
                        <i class="fa-solid fa-list-check mr-2"></i>Job Listings
                    </button>
                    <button id="tab-resumes-btn" onclick="switchView('resumes')" class="px-5 py-2.5 rounded-lg text-sm font-semibold transition-all text-slate-400 hover:text-white">
                        <i class="fa-solid fa-user-gear mr-2"></i>Resume Database <span class="bg-teal-500/20 text-teal-300 text-[10px] px-2 py-0.5 rounded ml-1 border border-teal-500/30">EMPLOYERS</span>
                    </button>
                </div>

                <!-- Database Access Badge Status -->
                <div id="db-status-badge" class="hidden sm:flex items-center space-x-2 text-xs bg-slate-900 border border-slate-800 px-3 py-1.5 rounded-lg">
                    <span id="access-dot" class="w-2 h-2 rounded-full bg-amber-400"></span>
                    <span id="access-text" class="text-slate-300">Employer Database Status: <strong class="text-amber-400 font-semibold">Locked (Free Plan)</strong></span>
                </div>
            </div>

            <div id="view-jobs" class="space-y-6">
                <div class="flex items-center justify-between">
                    <h2 class="text-xl font-bold text-white flex items-center gap-2">
                        <span>Latest Featured Job Positions</span>
                        <span id="job-count-badge" class="text-xs font-semibold bg-slate-800 text-teal-400 px-2.5 py-1 rounded-full border border-slate-700">6 Available</span>
                    </h2>
                    <div class="text-xs text-slate-400">
                        Sorted by: <span class="text-slate-200 font-medium">Most Recent</span>
                    </div>
                </div>

                <!-- Job Cards Container -->
                <div id="job-cards-list" class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-6">
                    <!-- Populated dynamically via JS -->
                </div>
            </div>

            <div id="view-resumes" class="hidden space-y-8">
                <!-- Advanced Filters for Resume DB -->
                <div class="bg-slate-900/80 border border-slate-800 p-6 rounded-2xl">
                    <div class="flex flex-col md:flex-row md:items-center justify-between pb-4 mb-4 border-b border-slate-800/80 gap-4">
                        <div>
                            <h3 class="text-lg font-bold text-white flex items-center gap-2">
                                <i class="fa-solid fa-sliders text-teal-400"></i> Advanced Candidate Filters
                            </h3>
                            <p class="text-xs text-slate-400">Filter top tech talents across verified profiles in real-time.</p>
                        </div>
                        <button onclick="resetResumeFilters()" class="text-xs text-teal-400 hover:text-teal-300 font-medium self-start md:self-auto">
                            <i class="fa-solid fa-arrow-rotate-left mr-1"></i> Reset Filters
                        </button>
                    </div>

                    <div class="grid grid-cols-1 sm:grid-cols-2 lg:grid-cols-4 gap-4">
                        <div>
                            <label class="block text-xs font-semibold text-slate-400 mb-1.5">Key Skill Tag</label>
                            <select id="filter-resume-skill" onchange="renderResumes()" class="w-full bg-slate-950 border border-slate-800 rounded-lg px-3 py-2 text-sm text-slate-200 focus:border-teal-500 outline-none">
                                <option value="">All Skills</option>
                                <option value="React">React / Next.js</option>
                                <option value="Python">Python / AI</option>
                                <option value="UI/UX">Figma / UI/UX</option>
                                <option value="Node.js">Node.js / Backend</option>
                                <option value="AWS">AWS / DevOps</option>
                            </select>
                        </div>

                        <div>
                            <label class="block text-xs font-semibold text-slate-400 mb-1.5">Min Experience</label>
                            <select id="filter-resume-exp" onchange="renderResumes()" class="w-full bg-slate-950 border border-slate-800 rounded-lg px-3 py-2 text-sm text-slate-200 focus:border-teal-500 outline-none">
                                <option value="0">Any Experience</option>
                                <option value="3">3+ Years</option>
                                <option value="5">5+ Years</option>
                                <option value="8">8+ Years</option>
                            </select>
                        </div>

                        <div>
                            <label class="block text-xs font-semibold text-slate-400 mb-1.5">Availability</label>
                            <select id="filter-resume-avail" onchange="renderResumes()" class="w-full bg-slate-950 border border-slate-800 rounded-lg px-3 py-2 text-sm text-slate-200 focus:border-teal-500 outline-none">
                                <option value="">Any Status</option>
                                <option value="Immediate">Immediate (2 Weeks)</option>
                                <option value="1 Month">Within 1 Month</option>
                            </select>
                        </div>

                        <div>
                            <label class="block text-xs font-semibold text-slate-400 mb-1.5">Min Salary Expectation</label>
                            <select id="filter-resume-salary" onchange="renderResumes()" class="w-full bg-slate-950 border border-slate-800 rounded-lg px-3 py-2 text-sm text-slate-200 focus:border-teal-500 outline-none">
                                <option value="0">Any Salary</option>
                                <option value="90000">$90k+/yr</option>
                                <option value="120000">$120k+/yr</option>
                                <option value="150000">$150k+/yr</option>
                            </select>
                        </div>
                    </div>
                </div>

                <!-- Resume Grid -->
                <div id="resume-cards-list" class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-6">
                    <!-- Populated dynamically via JS -->
                </div>
            </div>

        </section>

        <section id="pricing" class="bg-slate-900/60 border-t border-slate-800/80 py-20 px-4">
            <div class="max-w-7xl mx-auto">
                <div class="text-center max-w-3xl mx-auto mb-16">
                    <h2 class="text-3xl font-extrabold text-white">Employer & Recruiter Subscription Plans</h2>
                    <p class="text-slate-400 mt-3 text-sm sm:text-base">Unlock direct access to top talent, instant candidate contact information, and unlimited job postings.</p>
                </div>

                <div class="grid grid-cols-1 md:grid-cols-3 gap-8 items-stretch">
                    
                    <!-- Starter Plan -->
                    <div class="bg-slate-950 border border-slate-800 rounded-2xl p-8 flex flex-col justify-between hover:border-slate-700 transition-all">
                        <div>
                            <h3 class="text-lg font-bold text-white">Starter Employers</h3>
                            <p class="text-xs text-slate-400 mt-1">Perfect for single job postings</p>
                            <div class="mt-6 flex items-baseline">
                                <span class="text-4xl font-extrabold text-white">$49</span>
                                <span class="text-slate-400 text-sm ml-2">/ job post</span>
                            </div>
                            <ul class="mt-6 space-y-3 text-sm text-slate-300">
                                <li class="flex items-center"><i class="fa-solid fa-check text-teal-400 mr-2.5"></i> 1 Active Job Posting for 30 Days</li>
                                <li class="flex items-center"><i class="fa-solid fa-check text-teal-400 mr-2.5"></i> Basic Applicant Dashboard</li>
                                <li class="flex items-center"><i class="fa-solid fa-check text-teal-400 mr-2.5"></i> Standard Support</li>
                                <li class="flex items-center text-slate-500"><i class="fa-solid fa-xmark mr-2.5 text-slate-600"></i> Locked Resume Database Access</li>
                                <li class="flex items-center text-slate-500"><i class="fa-solid fa-xmark mr-2.5 text-slate-600"></i> Direct Candidate Messaging</li>
                            </ul>
                        </div>
                        <button onclick="openSubscriptionModal('Starter Plan', 49)" class="mt-8 w-full py-3 px-4 rounded-xl border border-teal-500/50 hover:bg-teal-500/10 text-teal-400 font-bold text-sm transition-colors text-center">
                            Select Starter
                        </button>
                    </div>

                    <!-- Recruiter Pro Plan (Featured) -->
                    <div class="bg-gradient-to-b from-slate-900 to-slate-950 border-2 border-teal-500 rounded-2xl p-8 flex flex-col justify-between shadow-2xl shadow-teal-500/10 relative transform md:-translate-y-2">
                        <div class="absolute -top-3.5 left-1/2 -translate-x-1/2 bg-teal-500 text-slate-950 text-xs font-black uppercase tracking-wider px-3 py-1 rounded-full shadow-md">
                            Most Popular Choice
                        </div>
                        <div>
                            <h3 class="text-lg font-bold text-white">Recruiter Pro</h3>
                            <p class="text-xs text-teal-300/80 mt-1">Full database & unlimited posting</p>
                            <div class="mt-6 flex items-baseline">
                                <span class="text-4xl font-extrabold text-white">$149</span>
                                <span class="text-slate-400 text-sm ml-2">/ month</span>
                            </div>
                            <ul class="mt-6 space-y-3 text-sm text-slate-200">
                                <li class="flex items-center"><i class="fa-solid fa-circle-check text-teal-400 mr-2.5"></i> <strong>Unlimited Active Job Postings</strong></li>
                                <li class="flex items-center"><i class="fa-solid fa-circle-check text-teal-400 mr-2.5"></i> <strong>Full Resume Database Unlock</strong></li>
                                <li class="flex items-center"><i class="fa-solid fa-circle-check text-teal-400 mr-2.5"></i> Direct Candidate Email & Phone</li>
                                <li class="flex items-center"><i class="fa-solid fa-circle-check text-teal-400 mr-2.5"></i> AI Resume Match Insights</li>
                                <li class="flex items-center"><i class="fa-solid fa-circle-check text-teal-400 mr-2.5"></i> Priority Search Placement</li>
                            </ul>
                        </div>
                        <button onclick="openSubscriptionModal('Recruiter Pro Tier', 149)" class="mt-8 w-full py-3.5 px-4 rounded-xl bg-teal-500 hover:bg-teal-400 text-slate-950 font-extrabold text-sm transition-all shadow-lg shadow-teal-500/25 text-center active:scale-95">
                            Subscribe Pro Access Now
                        </button>
                    </div>

                    <!-- Enterprise Plan -->
                    <div class="bg-slate-950 border border-slate-800 rounded-2xl p-8 flex flex-col justify-between hover:border-slate-700 transition-all">
                        <div>
                            <h3 class="text-lg font-bold text-white">Enterprise Global</h3>
                            <p class="text-xs text-slate-400 mt-1">Custom solutions for agency teams</p>
                            <div class="mt-6 flex items-baseline">
                                <span class="text-4xl font-extrabold text-white">$399</span>
                                <span class="text-slate-400 text-sm ml-2">/ month</span>
                            </div>
                            <ul class="mt-6 space-y-3 text-sm text-slate-300">
                                <li class="flex items-center"><i class="fa-solid fa-check text-teal-400 mr-2.5"></i> Everything in Recruiter Pro</li>
                                <li class="flex items-center"><i class="fa-solid fa-check text-teal-400 mr-2.5"></i> Dedicated Account Manager</li>
                                <li class="flex items-center"><i class="fa-solid fa-check text-teal-400 mr-2.5"></i> Multi-seat Recruiter Licenses (10 seats)</li>
                                <li class="flex items-center"><i class="fa-solid fa-check text-teal-400 mr-2.5"></i> Custom ATS Integration API</li>
                            </ul>
                        </div>
                        <button onclick="openSubscriptionModal('Enterprise Global', 399)" class="mt-8 w-full py-3 px-4 rounded-xl border border-slate-700 hover:bg-slate-800 text-white font-bold text-sm transition-colors text-center">
                            Subscribe Enterprise
                        </button>
                    </div>

                </div>
            </div>
        </section>
    </main>

    <footer class="bg-slate-950 border-t border-slate-800/80 py-12 px-4 text-slate-400 text-sm">
        <div class="max-w-7xl mx-auto grid grid-cols-1 md:grid-cols-4 gap-8">
            <div class="space-y-3">
                <div class="flex items-center space-x-2">
                    <div class="w-8 h-8 rounded-lg bg-teal-500 flex items-center justify-center text-slate-950 font-bold text-lg">
                        <i class="fa-solid fa-vault"></i>
                    </div>
                    <span class="text-lg font-bold text-white">JobVault Pro</span>
                </div>
                <p class="text-xs text-slate-400 leading-relaxed">
                    The premier job bank and candidate intelligence network powering high-growth software teams worldwide.
                </p>
            </div>
            <div>
                <h4 class="text-xs font-bold text-white uppercase tracking-wider mb-3">Job Seekers</h4>
                <ul class="space-y-2 text-xs">
                    <li><a href="#" onclick="switchView('jobs')" class="hover:text-teal-400 transition-colors">Browse All Jobs</a></li>
                    <li><a href="#" onclick="showToast('Upload feature ready for logged-in candidates')" class="hover:text-teal-400 transition-colors">Submit Resume</a></li>
                    <li><a href="#" class="hover:text-teal-400 transition-colors">Salary Calculators</a></li>
                </ul>
            </div>
            <div>
                <h4 class="text-xs font-bold text-white uppercase tracking-wider mb-3">Employers</h4>
                <ul class="space-y-2 text-xs">
                    <li><a href="#" onclick="switchView('resumes')" class="hover:text-teal-400 transition-colors">Search Candidate Database</a></li>
                    <li><a href="#pricing" class="hover:text-teal-400 transition-colors">Pricing & Plans</a></li>
                    <li><a href="#" onclick="openPostJobModal()" class="hover:text-teal-400 transition-colors">Post Job Posting</a></li>
                </ul>
            </div>
            <div>
                <h4 class="text-xs font-bold text-white uppercase tracking-wider mb-3">Security & Payment</h4>
                <p class="text-xs text-slate-500 mb-3">Protected by 256-bit SSL Encryption and Stripe PCI compliance standards.</p>
                <div class="flex space-x-3 text-slate-400 text-lg">
                    <i class="fa-brands fa-cc-visa"></i>
                    <i class="fa-brands fa-cc-mastercard"></i>
                    <i class="fa-brands fa-cc-stripe"></i>
                    <i class="fa-brands fa-cc-paypal"></i>
                </div>
            </div>
        </div>
        <div class="max-w-7xl mx-auto mt-8 pt-6 border-t border-slate-900 text-center text-xs text-slate-600">
            &copy; 2026 JobVault Pro Network Inc. All rights reserved. Interactive Demo Platform.
        </div>
    </footer>

    <div id="job-modal" class="fixed inset-0 z-50 hidden bg-slate-950/80 backdrop-blur-md flex items-center justify-center p-4">
        <div class="bg-slate-900 border border-slate-800 rounded-2xl max-w-lg w-full p-6 shadow-2xl relative animate-fadeIn">
            <button onclick="closeModal('job-modal')" class="absolute top-4 right-4 text-slate-400 hover:text-white text-lg p-2">
                <i class="fa-solid fa-xmark"></i>
            </button>
            <div id="job-modal-body">
                <!-- Dynamically filled by JS -->
            </div>
        </div>
    </div>

    <div id="post-job-modal" class="fixed inset-0 z-50 hidden bg-slate-950/80 backdrop-blur-md flex items-center justify-center p-4">
        <div class="bg-slate-900 border border-slate-800 rounded-2xl max-w-xl w-full p-6 shadow-2xl relative">
            <button onclick="closeModal('post-job-modal')" class="absolute top-4 right-4 text-slate-400 hover:text-white text-lg p-2">
                <i class="fa-solid fa-xmark"></i>
            </button>
            <h3 class="text-xl font-bold text-white mb-2">Post a New Job Opportunity</h3>
            <p class="text-xs text-slate-400 mb-6">Reach over 45,000 active candidates looking for their next move.</p>
            
            <form onsubmit="handlePostJobSubmit(event)" class="space-y-4">
                <div>
                    <label class="block text-xs font-semibold text-slate-300 mb-1">Job Title</label>
                    <input type="text" required id="post-title" placeholder="e.g. Senior Full Stack React Developer" class="w-full bg-slate-950 border border-slate-800 rounded-xl px-3.5 py-2.5 text-sm text-slate-200 focus:border-teal-500 outline-none">
                </div>
                <div class="grid grid-cols-2 gap-4">
                    <div>
                        <label class="block text-xs font-semibold text-slate-300 mb-1">Company Name</label>
                        <input type="text" required id="post-company" placeholder="e.g. Acme Corp" class="w-full bg-slate-950 border border-slate-800 rounded-xl px-3.5 py-2.5 text-sm text-slate-200 focus:border-teal-500 outline-none">
                    </div>
                    <div>
                        <label class="block text-xs font-semibold text-slate-300 mb-1">Category</label>
                        <select id="post-category" class="w-full bg-slate-950 border border-slate-800 rounded-xl px-3 py-2.5 text-sm text-slate-200 focus:border-teal-500 outline-none">
                            <option value="Engineering">Engineering</option>
                            <option value="Design">Design / UI</option>
                            <option value="Product">Product</option>
                            <option value="Data">Data / AI</option>
                        </select>
                    </div>
                </div>
                <div class="grid grid-cols-2 gap-4">
                    <div>
                        <label class="block text-xs font-semibold text-slate-300 mb-1">Location</label>
                        <input type="text" required id="post-location" placeholder="e.g. Remote / SF" class="w-full bg-slate-950 border border-slate-800 rounded-xl px-3.5 py-2.5 text-sm text-slate-200 focus:border-teal-500 outline-none">
                    </div>
                    <div>
                        <label class="block text-xs font-semibold text-slate-300 mb-1">Salary Range</label>
                        <input type="text" required id="post-salary" placeholder="e.g. $130k - $160k" class="w-full bg-slate-950 border border-slate-800 rounded-xl px-3.5 py-2.5 text-sm text-slate-200 focus:border-teal-500 outline-none">
                    </div>
                </div>
                <div>
                    <label class="block text-xs font-semibold text-slate-300 mb-1">Job Description</label>
                    <textarea rows="3" required id="post-desc" placeholder="Provide key responsibilities and tech stack requirements..." class="w-full bg-slate-950 border border-slate-800 rounded-xl px-3.5 py-2.5 text-sm text-slate-200 focus:border-teal-500 outline-none"></textarea>
                </div>
                <div class="pt-2 flex justify-end gap-3">
                    <button type="button" onclick="closeModal('post-job-modal')" class="px-4 py-2.5 text-sm text-slate-400 hover:text-white">Cancel</button>
                    <button type="submit" class="px-5 py-2.5 bg-teal-500 hover:bg-teal-400 text-slate-950 font-bold text-sm rounded-xl">Publish Job Listing</button>
                </div>
            </form>
        </div>
    </div>

    <div id="payment-modal" class="fixed inset-0 z-50 hidden bg-slate-950/85 backdrop-blur-md flex items-center justify-center p-4 overflow-y-auto">
        <div class="bg-slate-900 border border-slate-800 rounded-2xl max-w-xl w-full p-6 sm:p-8 shadow-2xl relative my-8">
            <button onclick="closeModal('payment-modal')" class="absolute top-4 right-4 text-slate-400 hover:text-white text-lg p-2">
                <i class="fa-solid fa-xmark"></i>
            </button>

            <!-- Modal Header -->
            <div class="flex items-center space-x-3 pb-4 border-b border-slate-800">
                <div class="w-10 h-10 rounded-xl bg-teal-500/20 text-teal-400 flex items-center justify-center text-lg font-bold border border-teal-500/30">
                    <i class="fa-solid fa-shield-halved"></i>
                </div>
                <div>
                    <h3 class="text-lg font-bold text-white">Secure Payment Gateway</h3>
                    <p class="text-xs text-slate-400">256-bit Encrypted Checkout • Cancel Anytime</p>
                </div>
            </div>

            <!-- Order Summary Banner -->
            <div class="my-6 bg-slate-950 border border-slate-800/80 p-4 rounded-xl flex items-center justify-between">
                <div>
                    <span class="text-xs text-slate-400 block">Selected Package</span>
                    <span id="pay-plan-name" class="font-bold text-teal-300 text-sm">Recruiter Pro Plan</span>
                </div>
                <div class="text-right">
                    <span class="text-xs text-slate-400 block">Total Due Now</span>
                    <span id="pay-plan-price" class="font-extrabold text-white text-xl">$149.00</span>
                </div>
            </div>

            <!-- Payment Method Tabs -->
            <div class="mb-6">
                <label class="block text-xs font-semibold text-slate-400 mb-2">Select Payment Method</label>
                <div class="grid grid-cols-3 gap-3">
                    <button type="button" onclick="setPaymentMethod('card')" id="pay-tab-card" class="py-2.5 px-3 rounded-xl border text-xs font-bold flex items-center justify-center gap-2 transition-all border-teal-500 bg-teal-500/10 text-teal-300">
                        <i class="fa-solid fa-credit-card"></i> Card
                    </button>
                    <button type="button" onclick="setPaymentMethod('paypal')" id="pay-tab-paypal" class="py-2.5 px-3 rounded-xl border text-xs font-bold flex items-center justify-center gap-2 transition-all border-slate-800 bg-slate-950 text-slate-400 hover:border-slate-700">
                        <i class="fa-brands fa-paypal"></i> PayPal
                    </button>
                    <button type="button" onclick="setPaymentMethod('stripe')" id="pay-tab-stripe" class="py-2.5 px-3 rounded-xl border text-xs font-bold flex items-center justify-center gap-2 transition-all border-slate-800 bg-slate-950 text-slate-400 hover:border-slate-700">
                        <i class="fa-brands fa-stripe"></i> Stripe Pay
                    </button>
                </div>
            </div>

            <!-- Credit Card Form Section -->
            <form id="payment-form" onsubmit="processPayment(event)" class="space-y-4">
                
                <div id="card-fields-container" class="space-y-4">
                    <div>
                        <label class="block text-xs font-semibold text-slate-300 mb-1">Cardholder Name</label>
                        <input type="text" required id="card-name" placeholder="John Doe" class="w-full bg-slate-950 border border-slate-800 rounded-xl px-3.5 py-2.5 text-sm text-slate-200 focus:border-teal-500 outline-none">
                    </div>

                    <div>
                        <label class="block text-xs font-semibold text-slate-300 mb-1">Card Number</label>
                        <div class="relative">
                            <input type="text" id="card-number" required maxlength="19" placeholder="4532 •••• •••• 8892" oninput="formatCardNumber(this)" class="w-full bg-slate-950 border border-slate-800 rounded-xl pl-3.5 pr-12 py-2.5 text-sm text-slate-200 focus:border-teal-500 outline-none font-mono">
                            <i id="card-brand-icon" class="fa-brands fa-cc-visa absolute right-3.5 top-1/2 -translate-y-1/2 text-slate-400 text-lg"></i>
                        </div>
                    </div>

                    <div class="grid grid-cols-2 gap-4">
                        <div>
                            <label class="block text-xs font-semibold text-slate-300 mb-1">Expiration Date</label>
                            <input type="text" id="card-exp" maxlength="5" required placeholder="MM/YY" oninput="formatExpDate(this)" class="w-full bg-slate-950 border border-slate-800 rounded-xl px-3.5 py-2.5 text-sm text-slate-200 focus:border-teal-500 outline-none font-mono">
                        </div>
                        <div>
                            <label class="block text-xs font-semibold text-slate-300 mb-1">CVC / CVV</label>
                            <input type="password" id="card-cvc" maxlength="4" required placeholder="123" class="w-full bg-slate-950 border border-slate-800 rounded-xl px-3.5 py-2.5 text-sm text-slate-200 focus:border-teal-500 outline-none font-mono">
                        </div>
                    </div>
                </div>

                <div id="alt-pay-notice" class="hidden text-center py-6 bg-slate-950 border border-slate-800 rounded-xl">
                    <p class="text-sm text-slate-300">You will be redirected to complete payment securely with <span id="alt-provider-name" class="font-bold text-teal-400">PayPal</span>.</p>
                </div>

                <!-- Complete Button -->
                <button type="submit" id="pay-submit-btn" class="w-full mt-4 py-3.5 rounded-xl bg-teal-500 hover:bg-teal-400 text-slate-950 font-bold text-sm transition-all flex items-center justify-center space-x-2 shadow-lg shadow-teal-500/20 active:scale-98">
                    <i id="pay-btn-icon" class="fa-solid fa-lock"></i>
                    <span id="pay-btn-text">Complete Payment & Unlock</span>
                </button>
            </form>
        </div>
    </div>

    <div id="toast" class="fixed bottom-6 right-6 z-50 hidden bg-slate-900 border border-teal-500/40 text-slate-100 px-4 py-3 rounded-xl shadow-2xl flex items-center space-x-3 transform transition-all duration-300">
        <i class="fa-solid fa-circle-check text-teal-400 text-lg"></i>
        <span id="toast-message" class="text-sm font-medium">Notification message</span>
    </div>

    <script>
        // State variables
        let currentView = 'jobs';
        let isDatabaseUnlocked = false;
        let selectedPaymentMethod = 'card';
        let currentSubPrice = 149;

        // Mock Job Postings Dataset
        let jobsData = [
            {
                id: 1,
                title: "Senior Full Stack Engineer (React/Node)",
                company: "CloudScale Systems",
                location: "Remote",
                salary: "$140,000 - $175,000 / yr",
                category: "Engineering",
                posted: "2 hours ago",
                tags: ["React", "TypeScript", "Node.js", "AWS"],
                desc: "We are seeking a seasoned Full Stack Engineer to architect scalable distributed systems. Experience with high-traffic GraphQL endpoints and microservices is highly preferred."
            },
            {
                id: 2,
                title: "Lead UI/UX Product Designer",
                company: "Nexus Design Labs",
                location: "San Francisco, CA",
                salary: "$130,000 - $160,000 / yr",
                category: "Design",
                posted: "5 hours ago",
                tags: ["Figma", "Design Systems", "User Research", "Prototyping"],
                desc: "Lead the user experience for our enterprise analytics suite. You will collaborate directly with product leads and engineering to craft intuitive UI components."
            },
            {
                id: 3,
                title: "AI & Machine Learning Data Scientist",
                company: "NeuralTech Dynamics",
                location: "New York, NY",
                salary: "$160,000 - $200,000 / yr",
                category: "Data",
                posted: "1 day ago",
                tags: ["Python", "PyTorch", "LLMs", "Data Pipelines"],
                desc: "Join our core AI research group. You will train custom domain LLMs, build automated feature engineering pipelines, and optimize real-time inference latency."
            },
            {
                id: 4,
                title: "Principal Product Manager",
                company: "FinFlow Global",
                location: "Remote",
                salary: "$150,000 - $185,000 / yr",
                category: "Product",
                posted: "2 days ago",
                tags: ["Fintech", "Agile", "Roadmapping", "SQL"],
                desc: "Drive the roadmap for our next-generation payment processing platform serving millions of global enterprise users."
            },
            {
                id: 5,
                title: "DevOps & Cloud Infrastructure Architect",
                company: "Vanguard Security",
                location: "London, UK",
                salary: "$125,000 - $155,000 / yr",
                category: "Engineering",
                posted: "3 days ago",
                tags: ["Kubernetes", "Terraform", "CI/CD", "AWS"],
                desc: "Manage high-availability cloud infrastructure across multi-region Kubernetes clusters with zero-downtime deployment pipelines."
            },
            {
                id: 6,
                title: "Senior Growth Marketing Manager",
                company: "Pulse Media",
                location: "San Francisco, CA",
                salary: "$110,000 - $140,000 / yr",
                category: "Marketing",
                posted: "3 days ago",
                tags: ["SEO", "Paid Ads", "Analytics", "Funnel Optimization"],
                desc: "Own developer acquisition funnels, performance marketing strategy, and multi-channel lifecycle user conversion."
            }
        ];

        // Mock Resumes / Candidates Dataset
        let resumesData = [
            {
                id: 101,
                name: "Alex Rivera",
                title: "Senior Full-Stack Architect",
                experience: 7,
                location: "San Francisco, CA",
                availability: "Immediate",
                expectedSalary: 155000,
                skills: ["React", "Node.js", "TypeScript", "AWS"],
                email: "alex.rivera@devvault-verified.com",
                phone: "+1 (555) 382-9102",
                summary: "7+ years building enterprise SaaS architectures with high throughput React & Node stacks. Former Lead at TechScale."
            },
            {
                id: 102,
                name: "Elena Rostova",
                title: "Lead AI/ML Research Engineer",
                experience: 6,
                location: "Remote",
                availability: "Immediate",
                expectedSalary: 165000,
                skills: ["Python", "PyTorch", "AWS", "LLMs"],
                email: "elena.r@neuralnet-expert.io",
                phone: "+1 (555) 721-4409",
                summary: "Specialized in computer vision and fine-tuning open-source LLM architectures for high-speed API deployment."
            },
            {
                id: 103,
                name: "Marcus Vance",
                title: "Senior Product Designer (UI/UX)",
                experience: 5,
                location: "New York, NY",
                availability: "1 Month",
                expectedSalary: 135000,
                skills: ["UI/UX", "Figma", "Design Systems"],
                email: "marcus.design@craftwork.org",
                phone: "+1 (555) 890-1123",
                summary: "Expert in complex design systems and modern accessibility standards. Created UI kits used by 10k+ developers."
            },
            {
                id: 104,
                name: "David Chen",
                title: "Cloud Native DevOps Lead",
                experience: 8,
                location: "Remote",
                availability: "Immediate",
                expectedSalary: 160000,
                skills: ["AWS", "Kubernetes", "Docker", "Python"],
                email: "d.chen@cloudops-pro.com",
                phone: "+1 (555) 234-8871",
                summary: "Certified AWS Solutions Architect with deep Kubernetes hands-on experience and multi-cloud infrastructure automation."
            },
            {
                id: 105,
                name: "Sophia Martinez",
                title: "Backend Go / Node.js Engineer",
                experience: 4,
                location: "London, UK",
                availability: "1 Month",
                expectedSalary: 115000,
                skills: ["Node.js", "Go", "PostgreSQL", "Docker"],
                email: "sophia.m@backend-craft.io",
                phone: "+44 20 7946 0912",
                summary: "Focus on microservices development, high-performance database indexing, and RESTful API optimizations."
            }
        ];

        window.addEventListener('DOMContentLoaded', () => {
            renderJobs(jobsData);
            renderResumes();
        });

        // View Switcher (Jobs vs Resumes)
        function switchView(view) {
            currentView = view;
            const jobsView = document.getElementById('view-jobs');
            const resumesView = document.getElementById('view-resumes');
            const jobsTabBtn = document.getElementById('tab-jobs-btn');
            const resumesTabBtn = document.getElementById('tab-resumes-btn');
            const navJobs = document.getElementById('nav-jobs');
            const navResumes = document.getElementById('nav-resumes');
            const heroTitle = document.getElementById('hero-title');

            if (view === 'jobs') {
                jobsView.classList.remove('hidden');
                resumesView.classList.add('hidden');
                
                jobsTabBtn.className = "px-5 py-2.5 rounded-lg text-sm font-bold transition-all bg-teal-500 text-slate-950 shadow-md";
                resumesTabBtn.className = "px-5 py-2.5 rounded-lg text-sm font-semibold transition-all text-slate-400 hover:text-white";

                navJobs.className = "hover:text-teal-400 transition-colors py-2 border-b-2 border-teal-400 text-teal-400 font-semibold";
                navResumes.className = "hover:text-teal-400 transition-colors py-2 border-b-2 border-transparent text-slate-300";

                heroTitle.innerHTML = `Connecting Top Talent with <br class="hidden sm:inline"><span class="bg-gradient-to-r from-teal-400 via-emerald-400 to-cyan-400 bg-clip-text text-transparent">World-Class Tech Teams</span>`;
            } else {
                jobsView.classList.add('hidden');
                resumesView.classList.remove('hidden');

                resumesTabBtn.className = "px-5 py-2.5 rounded-lg text-sm font-bold transition-all bg-teal-500 text-slate-950 shadow-md";
                jobsTabBtn.className = "px-5 py-2.5 rounded-lg text-sm font-semibold transition-all text-slate-400 hover:text-white";

                navResumes.className = "hover:text-teal-400 transition-colors py-2 border-b-2 border-teal-400 text-teal-400 font-semibold";
                navJobs.className = "hover:text-teal-400 transition-colors py-2 border-b-2 border-transparent text-slate-300";

                heroTitle.innerHTML = `Verified Candidate <br class="hidden sm:inline"><span class="bg-gradient-to-r from-teal-400 via-emerald-400 to-cyan-400 bg-clip-text text-transparent">Resume & Talent Vault</span>`;
            }
        }

        // Render Job Cards
        function renderJobs(list) {
            const container = document.getElementById('job-cards-list');
            document.getElementById('job-count-badge').textContent = `${list.length} Available`;

            if (list.length === 0) {
                container.innerHTML = `
                    <div class="col-span-full py-12 text-center bg-slate-900/50 rounded-2xl border border-slate-800">
                        <i class="fa-solid fa-folder-open text-4xl text-slate-600 mb-3"></i>
                        <p class="text-slate-300 font-medium">No job listings found matching your filters.</p>
                        <button onclick="resetSearch()" class="mt-3 text-xs text-teal-400 hover:underline">Clear all search parameters</button>
                    </div>
                `;
                return;
            }

            container.innerHTML = list.map(job => `
                <div class="bg-slate-900 border border-slate-800/90 hover:border-teal-500/50 rounded-2xl p-6 transition-all hover:shadow-xl hover:shadow-teal-500/5 flex flex-col justify-between group">
                    <div>
                        <div class="flex items-start justify-between gap-3 mb-3">
                            <span class="text-[11px] font-bold uppercase tracking-wider text-teal-400 bg-teal-500/10 px-2.5 py-1 rounded-md border border-teal-500/20">
                                ${job.category}
                            </span>
                            <span class="text-xs text-slate-500"><i class="fa-regular fa-clock mr-1"></i>${job.posted}</span>
                        </div>
                        
                        <h3 class="text-lg font-bold text-white group-hover:text-teal-300 transition-colors leading-snug">${job.title}</h3>
                        <p class="text-sm font-medium text-slate-400 mt-1"><i class="fa-solid fa-building text-slate-500 mr-1.5"></i>${job.company}</p>

                        <div class="mt-4 flex flex-wrap gap-2">
                            <span class="text-xs text-slate-300 bg-slate-950 px-2.5 py-1 rounded-lg border border-slate-800">
                                <i class="fa-solid fa-location-dot text-slate-500 mr-1"></i>${job.location}
                            </span>
                            <span class="text-xs text-emerald-400 bg-emerald-500/10 px-2.5 py-1 rounded-lg border border-emerald-500/20 font-semibold">
                                ${job.salary}
                            </span>
                        </div>

                        <p class="mt-4 text-xs text-slate-400 line-clamp-2 leading-relaxed">
                            ${job.desc}
                        </p>

                        <!-- Skill Tags -->
                        <div class="mt-4 flex flex-wrap gap-1.5">
                            ${job.tags.map(t => `<span class="text-[10px] bg-slate-800/80 text-slate-300 px-2 py-0.5 rounded">${t}</span>`).join('')}
                        </div>
                    </div>

                    <div class="mt-6 pt-4 border-t border-slate-800/80 flex items-center justify-between">
                        <button onclick="openApplyModal(${job.id})" class="w-full py-2.5 rounded-xl bg-slate-800 hover:bg-teal-500 hover:text-slate-950 text-slate-200 font-bold text-xs transition-all flex items-center justify-center gap-2">
                            <span>Quick Apply Position</span>
                            <i class="fa-solid fa-arrow-right text-xs"></i>
                        </button>
                    </div>
                </div>
            `).join('');
        }

        // Render Resume Database Cards
        function renderResumes() {
            const container = document.getElementById('resume-cards-list');
            const skillFilter = document.getElementById('filter-resume-skill').value;
            const expFilter = parseInt(document.getElementById('filter-resume-exp').value) || 0;
            const availFilter = document.getElementById('filter-resume-avail').value;
            const salaryFilter = parseInt(document.getElementById('filter-resume-salary').value) || 0;

            let filtered = resumesData.filter(r => {
                if (skillFilter && !r.skills.includes(skillFilter)) return false;
                if (r.experience < expFilter) return false;
                if (availFilter && r.availability !== availFilter) return false;
                if (r.expectedSalary < salaryFilter) return false;
                return true;
            });

            if (filtered.length === 0) {
                container.innerHTML = `
                    <div class="col-span-full py-12 text-center bg-slate-900/50 rounded-2xl border border-slate-800">
                        <i class="fa-solid fa-user-slash text-4xl text-slate-600 mb-3"></i>
                        <p class="text-slate-300 font-medium">No candidate resumes match the active filters.</p>
                        <button onclick="resetResumeFilters()" class="mt-3 text-xs text-teal-400 hover:underline">Reset Candidate Filters</button>
                    </div>
                `;
                return;
            }

            container.innerHTML = filtered.map(r => `
                <div class="bg-slate-900 border border-slate-800 rounded-2xl p-6 transition-all hover:border-slate-700 flex flex-col justify-between relative overflow-hidden">
                    
                    ${!isDatabaseUnlocked ? `
                        <div class="absolute top-3 right-3 bg-amber-500/10 text-amber-400 border border-amber-500/30 text-[10px] font-bold px-2.5 py-1 rounded-full flex items-center gap-1">
                            <i class="fa-solid fa-lock text-[10px]"></i> Contact Locked
                        </div>
                    ` : `
                        <div class="absolute top-3 right-3 bg-emerald-500/10 text-emerald-400 border border-emerald-500/30 text-[10px] font-bold px-2.5 py-1 rounded-full flex items-center gap-1">
                            <i class="fa-solid fa-lock-open text-[10px]"></i> Full Access
                        </div>
                    `}

                    <div>
                        <!-- Candidate Header & Avatar -->
                        <div class="flex items-center space-x-3 mb-4">
                            <div class="w-12 h-12 rounded-full bg-gradient-to-tr from-teal-500 to-indigo-600 flex items-center justify-center font-bold text-white text-lg shadow-md">
                                ${r.name.split(' ').map(n=>n[0]).join('')}
                            </div>
                            <div>
                                <h3 class="text-base font-bold text-white">${r.name}</h3>
                                <p class="text-xs text-teal-400 font-medium">${r.title}</p>
                            </div>
                        </div>

                        <div class="grid grid-cols-2 gap-2 text-xs mb-4 bg-slate-950 p-3 rounded-xl border border-slate-800/80">
                            <div>
                                <span class="text-slate-500 block">Experience</span>
                                <span class="font-semibold text-slate-200">${r.experience} Years</span>
                            </div>
                            <div>
                                <span class="text-slate-500 block">Expectation</span>
                                <span class="font-semibold text-slate-200">$${(r.expectedSalary/1000).toFixed(0)}k/year</span>
                            </div>
                            <div class="mt-1">
                                <span class="text-slate-500 block">Location</span>
                                <span class="font-semibold text-slate-200">${r.location}</span>
                            </div>
                            <div class="mt-1">
                                <span class="text-slate-500 block">Notice Period</span>
                                <span class="font-semibold text-emerald-400">${r.availability}</span>
                            </div>
                        </div>

                        <p class="text-xs text-slate-400 mb-4 line-clamp-2">${r.summary}</p>

                        <!-- Candidate Skills -->
                        <div class="flex flex-wrap gap-1.5 mb-4">
                            ${r.skills.map(s => `<span class="text-[10px] bg-teal-500/10 text-teal-300 border border-teal-500/20 px-2 py-0.5 rounded-md">${s}</span>`).join('')}
                        </div>
                    </div>

                    <!-- Lock / Unlock Interactive Area -->
                    <div class="pt-4 border-t border-slate-800">
                        ${isDatabaseUnlocked ? `
                            <div class="space-y-2 bg-slate-950/60 p-3 rounded-xl border border-emerald-500/20 text-xs">
                                <p class="text-slate-300"><i class="fa-solid fa-envelope text-teal-400 mr-2"></i>${r.email}</p>
                                <p class="text-slate-300"><i class="fa-solid fa-phone text-teal-400 mr-2"></i>${r.phone}</p>
                                <button onclick="showToast('Candidate Resume PDF downloading...')" class="w-full mt-2 py-2 rounded-lg bg-teal-500 hover:bg-teal-400 text-slate-950 font-bold text-xs">
                                    <i class="fa-solid fa-download mr-1"></i> Download Verified Resume
                                </button>
                            </div>
                        ` : `
                            <div class="text-center p-3 bg-slate-950/80 rounded-xl border border-slate-800">
                                <p class="text-[11px] text-slate-400 mb-2">Subscribe to Recruiter Pro to view candidate contact details & full CV.</p>
                                <button onclick="openSubscriptionModal('Recruiter Pro Tier', 149)" class="w-full py-2 bg-gradient-to-r from-teal-500 to-emerald-500 hover:from-teal-400 hover:to-emerald-400 text-slate-950 font-extrabold text-xs rounded-lg shadow-md transition-all">
                                    <i class="fa-solid fa-key mr-1"></i> Unlock Candidate Info ($149/mo)
                                </button>
                            </div>
                        `}
                    </div>

                </div>
            `).join('');
        }

        function handleSearch(e) {
            e.preventDefault();
            const keyword = document.getElementById('search-keyword').value.toLowerCase().trim();
            const category = document.getElementById('search-category').value;
            const location = document.getElementById('search-location').value;

            if (currentView === 'resumes') {
                switchView('jobs');
            }

            const filtered = jobsData.filter(j => {
                const matchKw = !keyword || j.title.toLowerCase().includes(keyword) || j.company.toLowerCase().includes(keyword) || j.tags.some(t => t.toLowerCase().includes(keyword));
                const matchCat = !category || j.category === category;
                const matchLoc = !location || j.location.includes(location);
                return matchKw && matchCat && matchLoc;
            });

            renderJobs(filtered);
            showToast(`Found ${filtered.length} matching job opportunities`);
        }

        function resetSearch() {
            document.getElementById('search-form').reset();
            renderJobs(jobsData);
        }

        function resetResumeFilters() {
            document.getElementById('filter-resume-skill').value = "";
            document.getElementById('filter-resume-exp').value = "0";
            document.getElementById('filter-resume-avail').value = "";
            document.getElementById('filter-resume-salary').value = "0";
            renderResumes();
        }

        function openApplyModal(jobId) {
            const job = jobsData.find(j => j.id === jobId);
            if (!job) return;

            const modalBody = document.getElementById('job-modal-body');
            modalBody.innerHTML = `
                <div class="mb-4">
                    <span class="text-xs font-bold text-teal-400 uppercase tracking-wider">${job.category}</span>
                    <h3 class="text-xl font-bold text-white mt-1">${job.title}</h3>
                    <p class="text-sm text-slate-400">${job.company} • ${job.location}</p>
                </div>

                <div class="bg-slate-950 p-4 rounded-xl border border-slate-800 text-xs text-slate-300 space-y-2 mb-6">
                    <p><strong>Salary:</strong> ${job.salary}</p>
                    <p><strong>Posted:</strong> ${job.posted}</p>
                    <p class="pt-2 text-slate-400 border-t border-slate-900">${job.desc}</p>
                </div>

                <form onsubmit="handleApplySubmit(event)" class="space-y-4">
                    <div>
                        <label class="block text-xs font-semibold text-slate-300 mb-1">Full Name</label>
                        <input type="text" required placeholder="Jane Doe" class="w-full bg-slate-950 border border-slate-800 rounded-xl px-3.5 py-2 text-sm text-slate-200 outline-none focus:border-teal-500">
                    </div>
                    <div>
                        <label class="block text-xs font-semibold text-slate-300 mb-1">Email Address</label>
                        <input type="email" required placeholder="jane@example.com" class="w-full bg-slate-950 border border-slate-800 rounded-xl px-3.5 py-2 text-sm text-slate-200 outline-none focus:border-teal-500">
                    </div>
                    <div>
                        <label class="block text-xs font-semibold text-slate-300 mb-1">LinkedIn / Portfolio URL</label>
                        <input type="url" required placeholder="https://linkedin.com/in/username" class="w-full bg-slate-950 border border-slate-800 rounded-xl px-3.5 py-2 text-sm text-slate-200 outline-none focus:border-teal-500">
                    </div>
                    <button type="submit" class="w-full py-3 bg-teal-500 hover:bg-teal-400 text-slate-950 font-bold text-sm rounded-xl transition-all shadow-lg shadow-teal-500/20">
                        Submit Application Now
                    </button>
                </form>
            `;

            document.getElementById('job-modal').classList.remove('hidden');
        }

        function openPostJobModal() {
            document.getElementById('post-job-modal').classList.remove('hidden');
        }

        function handlePostJobSubmit(e) {
            e.preventDefault();
            const newJob = {
                id: Date.now(),
                title: document.getElementById('post-title').value,
                company: document.getElementById('post-company').value,
                category: document.getElementById('post-category').value,
                location: document.getElementById('post-location').value,
                salary: document.getElementById('post-salary').value,
                posted: "Just now",
                tags: ["Full-Time", "Verified"],
                desc: document.getElementById('post-desc').value
            };

            jobsData.unshift(newJob);
            renderJobs(jobsData);
            closeModal('post-job-modal');
            showToast('Job listing successfully published to JobVault!');
        }

        function handleApplySubmit(e) {
            e.preventDefault();
            closeModal('job-modal');
            showToast('Application sent successfully to employer!');
        }

        function openSubscriptionModal(planName, price) {
            currentSubPrice = price;
            document.getElementById('pay-plan-name').textContent = planName;
            document.getElementById('pay-plan-price').textContent = `$${price}.00`;
            document.getElementById('payment-modal').classList.remove('hidden');
        }

        function closeModal(modalId) {
            document.getElementById(modalId).classList.add('hidden');
        }

        function setPaymentMethod(method) {
            selectedPaymentMethod = method;
            const cardTab = document.getElementById('pay-tab-card');
            const paypalTab = document.getElementById('pay-tab-paypal');
            const stripeTab = document.getElementById('pay-tab-stripe');

            const cardFields = document.getElementById('card-fields-container');
            const altNotice = document.getElementById('alt-pay-notice');
            const altProviderName = document.getElementById('alt-provider-name');
            const btnText = document.getElementById('pay-btn-text');

            // Reset tabs styling
            [cardTab, paypalTab, stripeTab].forEach(t => {
                t.className = "py-2.5 px-3 rounded-xl border text-xs font-bold flex items-center justify-center gap-2 transition-all border-slate-800 bg-slate-950 text-slate-400 hover:border-slate-700";
            });

            if (method === 'card') {
                cardTab.className = "py-2.5 px-3 rounded-xl border text-xs font-bold flex items-center justify-center gap-2 transition-all border-teal-500 bg-teal-500/10 text-teal-300";
                cardFields.classList.remove('hidden');
                altNotice.classList.add('hidden');
                btnText.textContent = `Complete Payment & Unlock ($${currentSubPrice})`;
            } else {
                const targetTab = method === 'paypal' ? paypalTab : stripeTab;
                targetTab.className = "py-2.5 px-3 rounded-xl border text-xs font-bold flex items-center justify-center gap-2 transition-all border-teal-500 bg-teal-500/10 text-teal-300";
                cardFields.classList.add('hidden');
                altNotice.classList.remove('hidden');
                altProviderName.textContent = method === 'paypal' ? 'PayPal Checkout' : 'Stripe Direct';
                btnText.textContent = `Proceed to ${method === 'paypal' ? 'PayPal' : 'Stripe'}`;
            }
        }

        function formatCardNumber(input) {
            let val = input.value.replace(/\D/g, '');
            val = val.substring(0, 16);
            let formatted = val.match(/.{1,4}/g)?.join(' ') || val;
            input.value = formatted;

            // Brand icon swap simulation
            const icon = document.getElementById('card-brand-icon');
            if (val.startsWith('4')) {
                icon.className = "fa-brands fa-cc-visa absolute right-3.5 top-1/2 -translate-y-1/2 text-blue-400 text-lg";
            } else if (val.startsWith('5')) {
                icon.className = "fa-brands fa-cc-mastercard absolute right-3.5 top-1/2 -translate-y-1/2 text-amber-400 text-lg";
            } else {
                icon.className = "fa-solid fa-credit-card absolute right-3.5 top-1/2 -translate-y-1/2 text-slate-400 text-lg";
            }
        }

        function formatExpDate(input) {
            let val = input.value.replace(/\D/g, '');
            if (val.length >= 2) {
                input.value = val.substring(0, 2) + '/' + val.substring(2, 4);
            } else {
                input.value = val;
            }
        }

        function processPayment(e) {
            e.preventDefault();
            const btn = document.getElementById('pay-submit-btn');
            const icon = document.getElementById('pay-btn-icon');
            const btnText = document.getElementById('pay-btn-text');

            // Simulate Processing Loading State
            btn.disabled = true;
            icon.className = "fa-solid fa-spinner animate-spin";
            btnText.textContent = "Verifying & Processing Payment...";

            setTimeout(() => {
                btn.disabled = false;
                icon.className = "fa-solid fa-lock";
                btnText.textContent = "Complete Payment & Unlock";

                // Unlock database access state
                isDatabaseUnlocked = true;
                
                // Update Badge in Header/UI
                const badgeDot = document.getElementById('access-dot');
                const badgeText = document.getElementById('access-text');
                badgeDot.className = "w-2 h-2 rounded-full bg-emerald-400 animate-pulse";
                badgeText.innerHTML = `Employer Database Status: <strong class="text-emerald-400 font-semibold">Pro Unlocked</strong>`;

                closeModal('payment-modal');
                switchView('resumes');
                renderResumes();

                showToast('Payment Successful! Full Candidate Resume Database Unlocked.');
            }, 2000);
        }

        function showToast(message) {
            const toast = document.getElementById('toast');
            const msg = document.getElementById('toast-message');
            msg.textContent = message;

            toast.classList.remove('hidden');
            setTimeout(() => {
                toast.classList.add('hidden');
            }, 4000);
        }

        function toggleMobileMenu() {
            const menu = document.getElementById('mobile-menu');
            menu.classList.toggle('hidden');
        }
    </script>
</body>
</html>
