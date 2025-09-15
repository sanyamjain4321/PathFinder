<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="utf-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1" />
    <title>PathFinder — Dashboard</title>
    <link rel="preconnect" href="https://fonts.googleapis.com" />
    <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin />
    <link href="https://fonts.googleapis.com/css2?family=Inter:opsz,wght@14..32,300;14..32,400;14..32,500;14..32,600&display=swap" rel="stylesheet" />
    <script src="https://cdn.tailwindcss.com"></script>
    <script src="https://unpkg.com/lucide@latest"></script>
    <script src="https://cdn.jsdelivr.net/npm/chart.js"></script>
  </head>
  <body class="antialiased bg-zinc-50 text-zinc-900 font-[Inter]">
    <!-- Top Navbar -->
    <header class="sticky top-0 z-40 bg-white/90 backdrop-blur border-b border-zinc-200/80">
      <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8">
        <div class="h-14 flex items-center justify-between">
          <div class="flex items-center gap-3">
            <button id="mobileSidebarToggle" class="md:hidden inline-flex items-center justify-center h-9 w-9 rounded-md ring-1 ring-zinc-200 hover:bg-zinc-50 hover:ring-zinc-300 transition-colors" aria-label="Toggle sidebar">
              <i data-lucide="menu" class="w-4.5 h-4.5 text-zinc-700"></i>
            </button>
            <div class="h-8 w-8 rounded-md bg-zinc-900 text-white grid place-items-center ring-1 ring-zinc-900/10">
              <span class="text-[11px] font-semibold tracking-tight">PF</span>
            </div>
            <span class="hidden sm:inline text-sm text-zinc-600">PathFinder</span>
          </div>

          <nav class="hidden md:flex items-center gap-1">
            <a href="#" class="px-3 py-1.5 text-sm rounded-md text-zinc-700 hover:text-zinc-900 hover:bg-zinc-100 ring-1 ring-transparent hover:ring-zinc-200 transition-colors">Home</a>
            <a href="#" class="px-3 py-1.5 text-sm rounded-md text-zinc-700 hover:text-zinc-900 hover:bg-zinc-100 ring-1 ring-transparent hover:ring-zinc-200 transition-colors">Internship Finder</a>
            <a href="#" class="px-3 py-1.5 text-sm rounded-md text-zinc-900 bg-zinc-100 ring-1 ring-zinc-200 hover:bg-zinc-200/60 transition-colors">Recommendations</a>
            <a href="#" class="px-3 py-1.5 text-sm rounded-md text-zinc-700 hover:text-zinc-900 hover:bg-zinc-100 ring-1 ring-transparent hover:ring-zinc-200 transition-colors">My Applications</a>
            <a href="#" class="px-3 py-1.5 text-sm rounded-md text-zinc-700 hover:text-zinc-900 hover:bg-zinc-100 ring-1 ring-transparent hover:ring-zinc-200 transition-colors">Profile</a>
          </nav>

          <div class="flex items-center gap-2">
            <div class="hidden sm:flex">
              <div class="relative">
                <input type="text" placeholder="Search internships..." class="w-64 md:w-72 rounded-md bg-white ring-1 ring-zinc-200 px-8 py-2 text-sm placeholder:text-zinc-400 focus:outline-none focus:ring-2 focus:ring-zinc-300" />
                <i data-lucide="search" class="w-4 h-4 text-zinc-500 absolute left-2.5 top-1/2 -translate-y-1/2"></i>
              </div>
            </div>
            <div class="relative">
              <button id="profileBtn" class="inline-flex items-center gap-2 rounded-md px-2.5 py-1.5 ring-1 ring-zinc-200 hover:bg-zinc-50 hover:ring-zinc-300 transition-colors">
                <img src="https://images.unsplash.com/photo-1544723795-3fb6469f5b39?q=80&w=256&auto=format&fit=crop" alt="avatar" class="h-6 w-6 rounded-full object-cover" />
                <span class="hidden sm:inline text-sm text-zinc-700">Alex</span>
                <i data-lucide="chevron-down" class="w-4 h-4 text-zinc-500"></i>
              </button>
              <div id="profileMenu" class="hidden absolute right-0 mt-2 w-48 rounded-md bg-white ring-1 ring-zinc-200 shadow-sm overflow-hidden">
                <a href="#" class="flex items-center gap-2 px-3 py-2 text-sm text-zinc-700 hover:bg-zinc-50">
                  <i data-lucide="user" class="w-4 h-4"></i> View Profile
                </a>
                <a href="#" class="flex items-center gap-2 px-3 py-2 text-sm text-zinc-700 hover:bg-zinc-50">
                  <i data-lucide="settings" class="w-4 h-4"></i> Settings
                </a>
                <div class="my-1 border-t border-zinc-200"></div>
                <a href="#" class="flex items-center gap-2 px-3 py-2 text-sm text-red-600 hover:bg-red-50">
                  <i data-lucide="log-out" class="w-4 h-4"></i> Sign out
                </a>
              </div>
            </div>
          </div>
        </div>
      </div>
    </header>

    <!-- Sidebar -->
    <aside id="sidebar" class="fixed top-14 left-0 h-[calc(100vh-56px)] w-72 md:translate-x-0 -translate-x-full md:flex hidden flex-col bg-white border-r border-zinc-200 transition-all duration-200">
      <div class="flex items-center justify-between px-3 py-2 border-b border-zinc-200">
        <span class="text-sm text-zinc-500">Navigation</span>
        <button id="collapseBtn" class="inline-flex items-center justify-center h-8 w-8 rounded-md ring-1 ring-zinc-200 hover:bg-zinc-50 hover:ring-zinc-300 transition-colors" aria-label="Collapse sidebar">
          <i data-lucide="panel-left-close" class="w-4 h-4 text-zinc-700"></i>
        </button>
      </div>
      <nav class="flex-1 overflow-y-auto py-2">
        <a href="#" class="group flex items-center gap-3 px-3 py-2 mx-2 rounded-md text-sm text-zinc-800 bg-zinc-100 ring-1 ring-zinc-200 hover:bg-zinc-200/60 transition-colors">
          <i data-lucide="layout-dashboard" class="w-4.5 h-4.5 text-zinc-700"></i>
          <span class="sidebar-label truncate">Overview</span>
        </a>
        <a href="#" class="group flex items-center gap-3 px-3 py-2 mx-2 rounded-md text-sm text-zinc-700 hover:text-zinc-900 hover:bg-zinc-50 ring-1 ring-transparent hover:ring-zinc-200 transition-colors">
          <i data-lucide="wand-2" class="w-4.5 h-4.5 text-zinc-700"></i>
          <span class="sidebar-label truncate">Recommendations</span>
        </a>
        <a href="#" class="group flex items-center gap-3 px-3 py-2 mx-2 rounded-md text-sm text-zinc-700 hover:text-zinc-900 hover:bg-zinc-50 ring-1 ring-transparent hover:ring-zinc-200 transition-colors">
          <i data-lucide="briefcase" class="w-4.5 h-4.5 text-zinc-700"></i>
          <span class="sidebar-label truncate">Applied Internships</span>
        </a>
        <a href="#" class="group flex items-center gap-3 px-3 py-2 mx-2 rounded-md text-sm text-zinc-700 hover:text-zinc-900 hover:bg-zinc-50 ring-1 ring-transparent hover:ring-zinc-200 transition-colors">
          <i data-lucide="bookmark" class="w-4.5 h-4.5 text-zinc-700"></i>
          <span class="sidebar-label truncate">Saved Internships</span>
        </a>
        <a href="#" class="group flex items-center gap-3 px-3 py-2 mx-2 rounded-md text-sm text-zinc-700 hover:text-zinc-900 hover:bg-zinc-50 ring-1 ring-transparent hover:ring-zinc-200 transition-colors">
          <i data-lucide="bell" class="w-4.5 h-4.5 text-zinc-700"></i>
          <span class="sidebar-label truncate">Notifications</span>
        </a>
        <!-- New: Resume Filter nav link -->
        <a href="#resume-filter" class="group flex items-center gap-3 px-3 py-2 mx-2 rounded-md text-sm text-zinc-700 hover:text-zinc-900 hover:bg-zinc-50 ring-1 ring-transparent hover:ring-zinc-200 transition-colors">
          <i data-lucide="file-search" class="w-4.5 h-4.5 text-zinc-700"></i>
          <span class="sidebar-label truncate">Resume Filter</span>
        </a>
      </nav>
      <!-- New: Resume Filter card -->
      <div id="resume-filter" class="px-3 py-2 border-t border-zinc-200">
        <div class="rounded-md bg-zinc-50 ring-1 ring-zinc-200 p-3">
          <div class="flex items-center gap-2">
            <i data-lucide="file-search" class="w-4 h-4 text-zinc-700"></i>
            <p class="text-sm font-medium text-zinc-900">Filter by Resume</p>
          </div>
          <p class="mt-1 text-xs text-zinc-600">Upload your resume to tailor internship results.</p>
          <input id="resumeInput" type="file" accept=".pdf,.doc,.docx" class="hidden" />
          <div class="mt-2 flex items-center gap-2">
            <button id="resumeUploadBtn" class="inline-flex items-center gap-2 rounded-md px-3 py-1.5 text-xs text-zinc-700 bg-white ring-1 ring-zinc-200 hover:bg-zinc-100 hover:ring-zinc-300 transition-colors">
              <i data-lucide="upload" class="w-3.5 h-3.5"></i>
              Upload Resume
            </button>
            <button id="applyResumeFilterBtn" disabled class="inline-flex items-center gap-2 rounded-md px-3 py-1.5 text-xs text-white bg-zinc-900 disabled:opacity-50 disabled:cursor-not-allowed hover:bg-zinc-800 transition-colors ring-1 ring-zinc-900/10">
              <i data-lucide="filter" class="w-3.5 h-3.5"></i>
              Use for Filter
            </button>
          </div>
          <div class="mt-2 flex items-center justify-between">
            <p id="resumeFileName" class="text-[11px] text-zinc-600 truncate"></p>
            <span id="resumeStatus" class="text-[11px] text-emerald-700"></span>
          </div>
        </div>
      </div>
      <div class="px-3 py-2 border-t border-zinc-200">
        <div class="rounded-md bg-zinc-50 ring-1 ring-zinc-200 p-3">
          <p class="text-xs text-zinc-600">Tip: Collapse the sidebar to maximize workspace.</p>
        </div>
      </div>
    </aside>

    <!-- Main Content -->
    <main id="mainContent" class="transition-[padding] duration-200 md:pl-72">
      <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8 py-6">
        <!-- Title + Filters -->
        <div class="flex items-start justify-between gap-4">
          <div>
            <h1 class="text-2xl md:text-3xl tracking-tight font-semibold text-zinc-900">My Internship Workspace</h1>
            <p class="mt-1 text-sm text-zinc-600">AI-curated recommendations and insights tailored to your skills.</p>
          </div>
          <div class="hidden md:flex items-center gap-2">
            <button class="inline-flex items-center gap-2 rounded-md px-3 py-2 text-sm text-zinc-700 bg-white ring-1 ring-zinc-200 hover:bg-zinc-50 hover:ring-zinc-300 transition-colors">
              <i data-lucide="refresh-cw" class="w-4 h-4"></i>
              Refresh
            </button>
            <button class="inline-flex items-center gap-2 rounded-md px-3 py-2 text-sm text-white bg-zinc-900 hover:bg-zinc-800 transition-colors ring-1 ring-zinc-900/10">
              <i data-lucide="sparkles" class="w-4 h-4"></i>
              Re-run AI
            </button>
          </div>
        </div>

        <!-- Search + Filter Bar -->
        <section class="mt-4 rounded-xl bg-white ring-1 ring-zinc-200 p-4">
          <div class="flex flex-col md:flex-row md:items-center gap-3">
            <div class="relative flex-1">
              <input type="text" placeholder="Search by title, company, or keyword..." class="w-full rounded-md bg-white ring-1 ring-zinc-200 px-9 py-2.5 text-sm placeholder:text-zinc-400 focus:outline-none focus:ring-2 focus:ring-zinc-300" />
              <i data-lucide="search" class="w-4 h-4 text-zinc-500 absolute left-2.5 top-1/2 -translate-y-1/2"></i>
            </div>
            <div class="grid grid-cols-2 md:grid-cols-4 gap-2 flex-1">
              <!-- Custom select: Skills -->
              <div class="relative">
                <select class="w-full appearance-none rounded-md bg-white ring-1 ring-zinc-200 px-3 py-2.5 pr-9 text-sm text-zinc-700 focus:outline-none focus:ring-2 focus:ring-zinc-300">
                  <option>Skills: Product, SQL, Analytics</option>
                  <option>Product Management</option>
                  <option>SQL</option>
                  <option>UX Research</option>
                  <option>Data Analysis</option>
                </select>
                <i data-lucide="chevron-down" class="pointer-events-none w-4 h-4 text-zinc-500 absolute right-2.5 top-1/2 -translate-y-1/2"></i>
              </div>
              <!-- Location -->
              <div class="relative">
                <select class="w-full appearance-none rounded-md bg-white ring-1 ring-zinc-200 px-3 py-2.5 pr-9 text-sm text-zinc-700 focus:outline-none focus:ring-2 focus:ring-zinc-300">
                  <option>Location: Remote</option>
                  <option>Remote</option>
                  <option>New York</option>
                  <option>London</option>
                  <option>Berlin</option>
                </select>
                <i data-lucide="chevron-down" class="pointer-events-none w-4 h-4 text-zinc-500 absolute right-2.5 top-1/2 -translate-y-1/2"></i>
              </div>
              <!-- Duration -->
              <div class="relative">
                <select class="w-full appearance-none rounded-md bg-white ring-1 ring-zinc-200 px-3 py-2.5 pr-9 text-sm text-zinc-700 focus:outline-none focus:ring-2 focus:ring-zinc-300">
                  <option>Duration: 3–6 months</option>
                  <option>0–2 months</option>
                  <option>3–6 months</option>
                  <option>6+ months</option>
                </select>
                <i data-lucide="chevron-down" class="pointer-events-none w-4 h-4 text-zinc-500 absolute right-2.5 top-1/2 -translate-y-1/2"></i>
              </div>
              <!-- Domain -->
              <div class="relative">
                <select class="w-full appearance-none rounded-md bg-white ring-1 ring-zinc-200 px-3 py-2.5 pr-9 text-sm text-zinc-700 focus:outline-none focus:ring-2 focus:ring-zinc-300">
                  <option>Domain: Product</option>
                  <option>Product</option>
                  <option>Data</option>
                  <option>Design</option>
                  <option>Marketing</option>
                </select>
                <i data-lucide="chevron-down" class="pointer-events-none w-4 h-4 text-zinc-500 absolute right-2.5 top-1/2 -translate-y-1/2"></i>
              </div>
            </div>
            <div class="flex items-center gap-2">
              <button class="inline-flex items-center gap-2 rounded-md px-3 py-2 text-sm text-zinc-700 bg-white ring-1 ring-zinc-200 hover:bg-zinc-50 hover:ring-zinc-300 transition-colors">
                <i data-lucide="sliders-horizontal" class="w-4 h-4"></i>
                Filters
              </button>
              <button class="inline-flex items-center gap-2 rounded-md px-3 py-2 text-sm text-white bg-zinc-900 hover:bg-zinc-800 transition-colors ring-1 ring-zinc-900/10">
                <i data-lucide="search-check" class="w-4 h-4"></i>
                Apply
              </button>
            </div>
          </div>
        </section>

        <!-- Widgets Grid -->
        <section class="mt-6 grid grid-cols-12 gap-6">
          <!-- Recommended Internships -->
          <div class="col-span-12 lg:col-span-7 rounded-xl bg-white ring-1 ring-zinc-200 p-4">
            <div class="flex items-center justify-between">
              <div class="flex items-center gap-2">
                <i data-lucide="sparkles" class="w-5 h-5 text-zinc-600"></i>
                <h2 class="text-lg tracking-tight font-semibold">Recommended Internships</h2>
              </div>
              <button class="text-xs rounded-md px-2 py-1 ring-1 ring-zinc-200 hover:bg-zinc-50">See all</button>
            </div>
            <div class="mt-3 divide-y divide-zinc-100">
              <!-- Item -->
              <div class="py-3 flex items-start justify-between gap-3">
                <div>
                  <div class="flex items-center gap-2">
                    <p class="text-sm font-medium text-zinc-900">Product Analyst Intern</p>
                    <span class="inline-flex items-center gap-1 text-[11px] text-emerald-700 bg-emerald-50 ring-1 ring-emerald-200 px-2 py-0.5 rounded-full">
                      <i data-lucide="badge-check" class="w-3.5 h-3.5"></i> Best Match
                    </span>
                  </div>
                  <p class="text-xs text-zinc-600 mt-0.5">InsightWorks • Remote • Stipend $1,200/mo • 3 months</p>
                  <div class="mt-2 flex items-center gap-2">
                    <div class="h-2 w-36 bg-zinc-100 rounded-full overflow-hidden">
                      <div class="h-full w-[92%] bg-emerald-500"></div>
                    </div>
                    <span class="text-xs text-zinc-700">92% match</span>
                  </div>
                </div>
                <div class="flex items-center gap-2">
                  <button class="rounded-md px-3 py-1.5 text-sm text-white bg-zinc-900 hover:bg-zinc-800 transition-colors">Apply</button>
                  <button class="rounded-md px-2.5 py-1.5 ring-1 ring-zinc-200 hover:bg-zinc-50" aria-label="Save">
                    <i data-lucide="bookmark-plus" class="w-4 h-4 text-zinc-700"></i>
                  </button>
                </div>
              </div>
              <!-- Item -->
              <div class="py-3 flex items-start justify-between gap-3">
                <div>
                  <div class="flex items-center gap-2">
                    <p class="text-sm font-medium text-zinc-900">Associate PM Intern</p>
                    <span class="inline-flex items-center gap-1 text-[11px] text-sky-700 bg-sky-50 ring-1 ring-sky-200 px-2 py-0.5 rounded-full">
                      <i data-lucide="flame" class="w-3.5 h-3.5"></i> Trending
                    </span>
                  </div>
                  <p class="text-xs text-zinc-600 mt-0.5">NovaTech • London • Stipend £900/mo • 6 months</p>
                  <div class="mt-2 flex items-center gap-2">
                    <div class="h-2 w-36 bg-zinc-100 rounded-full overflow-hidden">
                      <div class="h-full w-[86%] bg-emerald-500"></div>
                    </div>
                    <span class="text-xs text-zinc-700">86% match</span>
                  </div>
                </div>
                <div class="flex items-center gap-2">
                  <button class="rounded-md px-3 py-1.5 text-sm text-white bg-zinc-900 hover:bg-zinc-800 transition-colors">Apply</button>
                  <button class="rounded-md px-2.5 py-1.5 ring-1 ring-zinc-200 hover:bg-zinc-50" aria-label="Save">
                    <i data-lucide="bookmark-plus" class="w-4 h-4 text-zinc-700"></i>
                  </button>
                </div>
              </div>
              <!-- Item -->
              <div class="py-3 flex items-start justify-between gap-3">
                <div>
                  <div class="flex items-center gap-2">
                    <p class="text-sm font-medium text-zinc-900">Growth PM Intern</p>
                    <span class="inline-flex items-center gap-1 text-[11px] text-amber-700 bg-amber-50 ring-1 ring-amber-200 px-2 py-0.5 rounded-full">
                      <i data-lucide="trending-up" class="w-3.5 h-3.5"></i> High Demand
                    </span>
                  </div>
                  <p class="text-xs text-zinc-600 mt-0.5">BrightPath • Berlin • Stipend €1,000/mo • 4 months</p>
                  <div class="mt-2 flex items-center gap-2">
                    <div class="h-2 w-36 bg-zinc-100 rounded-full overflow-hidden">
                      <div class="h-full w-[78%] bg-emerald-500"></div>
                    </div>
                    <span class="text-xs text-zinc-700">78% match</span>
                  </div>
                </div>
                <div class="flex items-center gap-2">
                  <button class="rounded-md px-3 py-1.5 text-sm text-white bg-zinc-900 hover:bg-zinc-800 transition-colors">Apply</button>
                  <button class="rounded-md px-2.5 py-1.5 ring-1 ring-zinc-200 hover:bg-zinc-50" aria-label="Save">
                    <i data-lucide="bookmark-plus" class="w-4 h-4 text-zinc-700"></i>
                  </button>
                </div>
              </div>
            </div>
          </div>

          <!-- Active Applications -->
          <div class="col-span-12 lg:col-span-5 rounded-xl bg-white ring-1 ring-zinc-200 p-4">
            <div class="flex items-center justify-between">
              <div class="flex items-center gap-2">
                <i data-lucide="briefcase" class="w-5 h-5 text-zinc-600"></i>
                <h2 class="text-lg tracking-tight font-semibold">Active Applications</h2>
              </div>
              <button class="text-xs rounded-md px-2 py-1 ring-1 ring-zinc-200 hover:bg-zinc-50">Manage</button>
            </div>
            <div class="mt-3 space-y-2">
              <div class="flex items-center justify-between rounded-lg ring-1 ring-zinc-200 p-3">
                <div>
                  <p class="text-sm font-medium">Product Analyst Intern • InsightWorks</p>
                  <p class="text-xs text-zinc-600">Applied 2 days ago</p>
                </div>
                <span class="text-[11px] text-sky-800 bg-sky-50 ring-1 ring-sky-200 px-2 py-0.5 rounded-full">Applied</span>
              </div>
              <div class="flex items-center justify-between rounded-lg ring-1 ring-zinc-200 p-3">
                <div>
                  <p class="text-sm font-medium">Associate PM Intern • NovaTech</p>
                  <p class="text-xs text-zinc-600">Updated 1 day ago</p>
                </div>
                <span class="text-[11px] text-amber-800 bg-amber-50 ring-1 ring-amber-200 px-2 py-0.5 rounded-full">Shortlisted</span>
              </div>
              <div class="flex items-center justify-between rounded-lg ring-1 ring-zinc-200 p-3">
                <div>
                  <p class="text-sm font-medium">Growth PM Intern • BrightPath</p>
                  <p class="text-xs text-zinc-600">Updated 3 days ago</p>
                </div>
                <span class="text-[11px] text-emerald-800 bg-emerald-50 ring-1 ring-emerald-200 px-2 py-0.5 rounded-full">Selected</span>
              </div>
              <div class="flex items-center justify-between rounded-lg ring-1 ring-zinc-200 p-3">
                <div>
                  <p class="text-sm font-medium">UX Research Intern • PixelLabs</p>
                  <p class="text-xs text-zinc-600">Updated 1 week ago</p>
                </div>
                <span class="text-[11px] text-red-800 bg-red-50 ring-1 ring-red-200 px-2 py-0.5 rounded-full">Rejected</span>
              </div>
            </div>
          </div>

          <!-- Skill Match Analysis -->
          <div class="col-span-12 md:col-span-6 rounded-xl bg-white ring-1 ring-zinc-200 p-4">
            <div class="flex items-center justify-between">
              <div class="flex items-center gap-2">
                <i data-lucide="radar" class="w-5 h-5 text-zinc-600"></i>
                <h2 class="text-lg tracking-tight font-semibold">Skill Match Analysis</h2>
              </div>
              <button class="text-xs rounded-md px-2 py-1 ring-1 ring-zinc-200 hover:bg-zinc-50">View details</button>
            </div>
            <div class="mt-3 grid grid-cols-1 sm:grid-cols-2 gap-4">
              <div class="rounded-lg ring-1 ring-zinc-200 p-3">
                <p class="text-sm text-zinc-700">Overall Match</p>
                <!-- Chart: place canvas inside a wrapper div to avoid growth bug -->
                <div class="mt-2">
                  <div class="h-40">
                    <canvas id="matchChart"></canvas>
                  </div>
                </div>
              </div>
              <div class="rounded-lg ring-1 ring-zinc-200 p-3">
                <p class="text-sm text-zinc-700">Top Skills</p>
                <div class="mt-3 space-y-3">
                  <div>
                    <div class="flex items-center justify-between text-xs">
                      <span class="text-zinc-600">Product Sense</span><span class="text-zinc-700">88%</span>
                    </div>
                    <div class="mt-1 h-2 bg-zinc-100 rounded-full overflow-hidden"><div class="h-full w-[88%] bg-emerald-500"></div></div>
                  </div>
                  <div>
                    <div class="flex items-center justify-between text-xs">
                      <span class="text-zinc-600">SQL</span><span class="text-zinc-700">76%</span>
                    </div>
                    <div class="mt-1 h-2 bg-zinc-100 rounded-full overflow-hidden"><div class="h-full w-[76%] bg-emerald-500"></div></div>
                  </div>
                  <div>
                    <div class="flex items-center justify-between text-xs">
                      <span class="text-zinc-600">Data Analysis</span><span class="text-zinc-700">81%</span>
                    </div>
                    <div class="mt-1 h-2 bg-zinc-100 rounded-full overflow-hidden"><div class="h-full w-[81%] bg-emerald-500"></div></div>
                  </div>
                  <div>
                    <div class="flex items-center justify-between text-xs">
                      <span class="text-zinc-600">UX Research</span><span class="text-zinc-700">64%</span>
                    </div>
                    <div class="mt-1 h-2 bg-zinc-100 rounded-full overflow-hidden"><div class="h-full w-[64%] bg-emerald-500"></div></div>
                  </div>
                </div>
              </div>
            </div>
          </div>

          <!-- Upcoming Deadlines -->
          <div class="col-span-12 md:col-span-6 rounded-xl bg-white ring-1 ring-zinc-200 p-4">
            <div class="flex items-center justify-between">
              <div class="flex items-center gap-2">
                <i data-lucide="calendar-days" class="w-5 h-5 text-zinc-600"></i>
                <h2 class="text-lg tracking-tight font-semibold">Upcoming Deadlines</h2>
              </div>
              <button class="text-xs rounded-md px-2 py-1 ring-1 ring-zinc-200 hover:bg-zinc-50">Next 7 days</button>
            </div>
            <div class="mt-3">
              <!-- Simple 7-day strip -->
              <div class="grid grid-cols-7 gap-2">
                <!-- Day cards -->
                <div class="rounded-lg ring-1 ring-zinc-200 p-2 text-center">
                  <p class="text-[11px] text-zinc-500">Mon</p>
                  <p class="text-sm font-medium">12</p>
                  <span class="mt-1 inline-block text-[10px] text-zinc-700 bg-zinc-100 ring-1 ring-zinc-200 px-1.5 py-0.5 rounded">0</span>
                </div>
                <div class="rounded-lg ring-1 ring-zinc-200 p-2 text-center">
                  <p class="text-[11px] text-zinc-500">Tue</p>
                  <p class="text-sm font-medium">13</p>
                  <span class="mt-1 inline-block text-[10px] text-amber-800 bg-amber-50 ring-1 ring-amber-200 px-1.5 py-0.5 rounded">1</span>
                </div>
                <div class="rounded-lg ring-1 ring-zinc-200 p-2 text-center">
                  <p class="text-[11px] text-zinc-500">Wed</p>
                  <p class="text-sm font-medium">14</p>
                  <span class="mt-1 inline-block text-[10px] text-emerald-800 bg-emerald-50 ring-1 ring-emerald-200 px-1.5 py-0.5 rounded">2</span>
                </div>
                <div class="rounded-lg ring-1 ring-zinc-200 p-2 text-center">
                  <p class="text-[11px] text-zinc-500">Thu</p>
                  <p class="text-sm font-medium">15</p>
                  <span class="mt-1 inline-block text-[10px] text-amber-800 bg-amber-50 ring-1 ring-amber-200 px-1.5 py-0.5 rounded">1</span>
                </div>
                <div class="rounded-lg ring-1 ring-zinc-200 p-2 text-center">
                  <p class="text-[11px] text-zinc-500">Fri</p>
                  <p class="text-sm font-medium">16</p>
                  <span class="mt-1 inline-block text-[10px] text-red-800 bg-red-50 ring-1 ring-red-200 px-1.5 py-0.5 rounded">3</span>
                </div>
                <div class="rounded-lg ring-1 ring-zinc-200 p-2 text-center">
                  <p class="text-[11px] text-zinc-500">Sat</p>
                  <p class="text-sm font-medium">17</p>
                  <span class="mt-1 inline-block text-[10px] text-zinc-700 bg-zinc-100 ring-1 ring-zinc-200 px-1.5 py-0.5 rounded">0</span>
                </div>
                <div class="rounded-lg ring-1 ring-zinc-200 p-2 text-center">
                  <p class="text-[11px] text-zinc-500">Sun</p>
                  <p class="text-sm font-medium">18</p>
                  <span class="mt-1 inline-block text-[10px] text-emerald-800 bg-emerald-50 ring-1 ring-emerald-200 px-1.5 py-0.5 rounded">2</span>
                </div>
              </div>
              <div class="mt-3 space-y-2">
                <div class="flex items-center justify-between rounded-lg ring-1 ring-zinc-200 p-3">
                  <div class="flex items-center gap-2">
                    <i data-lucide="clock" class="w-4 h-4 text-amber-600"></i>
                    <p class="text-sm">Deadline: NovaTech — Associate PM Intern</p>
                  </div>
                  <span class="text-[11px] text-amber-800 bg-amber-50 ring-1 ring-amber-200 px-2 py-0.5 rounded-full">In 2 days</span>
                </div>
                <div class="flex items-center justify-between rounded-lg ring-1 ring-zinc-200 p-3">
                  <div class="flex items-center gap-2">
                    <i data-lucide="clock" class="w-4 h-4 text-red-600"></i>
                    <p class="text-sm">Deadline: BrightPath — Growth PM Intern</p>
                  </div>
                  <span class="text-[11px] text-red-800 bg-red-50 ring-1 ring-red-200 px-2 py-0.5 rounded-full">Tomorrow</span>
                </div>
              </div>
            </div>
          </div>

          <!-- Top Opportunities -->
          <div class="col-span-12 rounded-xl bg-white ring-1 ring-zinc-200 p-4">
            <div class="flex items-center justify-between">
              <div class="flex items-center gap-2">
                <i data-lucide="trophy" class="w-5 h-5 text-zinc-600"></i>
                <h2 class="text-lg tracking-tight font-semibold">Top Opportunities</h2>
              </div>
              <button class="text-xs rounded-md px-2 py-1 ring-1 ring-zinc-200 hover:bg-zinc-50">Refresh rankings</button>
            </div>
            <div class="mt-3 grid grid-cols-1 md:grid-cols-3 gap-3">
              <div class="rounded-lg ring-1 ring-zinc-200 p-3">
                <div class="flex items-center justify-between">
                  <p class="text-sm font-medium">Product Analyst Intern</p>
                  <span class="inline-flex items-center gap-1 text-[11px] text-emerald-700 bg-emerald-50 ring-1 ring-emerald-200 px-2 py-0.5 rounded-full">
                    <i data-lucide="badge-check" class="w-3.5 h-3.5"></i> Best Match
                  </span>
                </div>
                <p class="text-xs text-zinc-600 mt-0.5">InsightWorks • Remote • $1,200/mo</p>
              </div>
              <div class="rounded-lg ring-1 ring-zinc-200 p-3">
                <div class="flex items-center justify-between">
                  <p class="text-sm font-medium">Associate PM Intern</p>
                  <span class="inline-flex items-center gap-1 text-[11px] text-sky-700 bg-sky-50 ring-1 ring-sky-200 px-2 py-0.5 rounded-full">
                    <i data-lucide="flame" class="w-3.5 h-3.5"></i> Trending
                  </span>
                </div>
                <p class="text-xs text-zinc-600 mt-0.5">NovaTech • London • £900/mo</p>
              </div>
              <div class="rounded-lg ring-1 ring-zinc-200 p-3">
                <div class="flex items-center justify-between">
                  <p class="text-sm font-medium">Growth PM Intern</p>
                  <span class="inline-flex items-center gap-1 text-[11px] text-amber-700 bg-amber-50 ring-1 ring-amber-200 px-2 py-0.5 rounded-full">
                    <i data-lucide="trending-up" class="w-3.5 h-3.5"></i> High Demand
                  </span>
                </div>
                <p class="text-xs text-zinc-600 mt-0.5">BrightPath • Berlin • €1,000/mo</p>
              </div>
            </div>
          </div>
        </section>

        <!-- Internship Table -->
        <section class="mt-6 rounded-xl bg-white ring-1 ring-zinc-200 overflow-hidden">
          <div class="px-4 py-3 border-b border-zinc-200 flex items-center justify-between">
            <div class="flex items-center gap-2">
              <i data-lucide="table-2" class="w-5 h-5 text-zinc-600"></i>
              <h2 class="text-lg tracking-tight font-semibold">Internship Listings</h2>
            </div>
            <div class="flex items-center gap-2">
              <button class="inline-flex items-center gap-1.5 rounded-md px-3 py-1.5 text-xs text-zinc-700 bg-white ring-1 ring-zinc-200 hover:bg-zinc-50 hover:ring-zinc-300">
                <i data-lucide="download" class="w-3.5 h-3.5"></i> Export
              </button>
              <button class="inline-flex items-center gap-1.5 rounded-md px-3 py-1.5 text-xs text-white bg-zinc-900 hover:bg-zinc-800 ring-1 ring-zinc-900/10">
                <i data-lucide="plus" class="w-3.5 h-3.5"></i> Add
              </button>
            </div>
          </div>

          <div class="overflow-x-auto">
            <table class="min-w-full text-sm">
              <thead class="bg-zinc-50 border-b border-zinc-200">
                <tr class="text-left text-zinc-600">
                  <th class="px-4 py-2 font-medium">Internship</th>
                  <th class="px-4 py-2 font-medium">Company</th>
                  <th class="px-4 py-2 font-medium">Location</th>
                  <th class="px-4 py-2 font-medium">Stipend</th>
                  <th class="px-4 py-2 font-medium">Duration</th>
                  <th class="px-4 py-2 font-medium">Skill Match</th>
                  <th class="px-4 py-2 font-medium text-right">Actions</th>
                </tr>
              </thead>
              <tbody class="divide-y divide-zinc-100">
                <tr class="hover:bg-zinc-50">
                  <td class="px-4 py-3 text-zinc-900">Product Analyst Intern</td>
                  <td class="px-4 py-3 text-zinc-700">InsightWorks</td>
                  <td class="px-4 py-3 text-zinc-700">Remote</td>
                  <td class="px-4 py-3 text-zinc-700">$1,200/mo</td>
                  <td class="px-4 py-3 text-zinc-700">3 months</td>
                  <td class="px-4 py-3">
                    <div class="flex items-center gap-2">
                      <div class="h-2 w-24 bg-zinc-100 rounded-full overflow-hidden"><div class="h-full w-[92%] bg-emerald-500"></div></div>
                      <span class="text-xs text-zinc-700">92%</span>
                    </div>
                  </td>
                  <td class="px-4 py-3">
                    <div class="flex items-center gap-2 justify-end">
                      <button class="rounded-md px-3 py-1.5 text-xs text-white bg-zinc-900 hover:bg-zinc-800 transition-colors">Apply</button>
                      <button class="rounded-md px-2.5 py-1.5 ring-1 ring-zinc-200 hover:bg-zinc-50" aria-label="Save">
                        <i data-lucide="bookmark" class="w-4 h-4 text-zinc-700"></i>
                      </button>
                    </div>
                  </td>
                </tr>
                <tr class="hover:bg-zinc-50">
                  <td class="px-4 py-3 text-zinc-900">Associate PM Intern</td>
                  <td class="px-4 py-3 text-zinc-700">NovaTech</td>
                  <td class="px-4 py-3 text-zinc-700">London</td>
                  <td class="px-4 py-3 text-zinc-700">£900/mo</td>
                  <td class="px-4 py-3 text-zinc-700">6 months</td>
                  <td class="px-4 py-3">
                    <div class="flex items-center gap-2">
                      <div class="h-2 w-24 bg-zinc-100 rounded-full overflow-hidden"><div class="h-full w-[86%] bg-emerald-500"></div></div>
                      <span class="text-xs text-zinc-700">86%</span>
                    </div>
                  </td>
                  <td class="px-4 py-3">
                    <div class="flex items-center gap-2 justify-end">
                      <button class="rounded-md px-3 py-1.5 text-xs text-white bg-zinc-900 hover:bg-zinc-800 transition-colors">Apply</button>
                      <button class="rounded-md px-2.5 py-1.5 ring-1 ring-zinc-200 hover:bg-zinc-50" aria-label="Save">
                        <i data-lucide="bookmark" class="w-4 h-4 text-zinc-700"></i>
                      </button>
                    </div>
                  </td>
                </tr>
                <tr class="hover:bg-zinc-50">
                  <td class="px-4 py-3 text-zinc-900">Growth PM Intern</td>
                  <td class="px-4 py-3 text-zinc-700">BrightPath</td>
                  <td class="px-4 py-3 text-zinc-700">Berlin</td>
                  <td class="px-4 py-3 text-zinc-700">€1,000/mo</td>
                  <td class="px-4 py-3 text-zinc-700">4 months</td>
                  <td class="px-4 py-3">
                    <div class="flex items-center gap-2">
                      <div class="h-2 w-24 bg-zinc-100 rounded-full overflow-hidden"><div class="h-full w-[78%] bg-emerald-500"></div></div>
                      <span class="text-xs text-zinc-700">78%</span>
                    </div>
                  </td>
                  <td class="px-4 py-3">
                    <div class="flex items-center gap-2 justify-end">
                      <button class="rounded-md px-3 py-1.5 text-xs text-white bg-zinc-900 hover:bg-zinc-800 transition-colors">Apply</button>
                      <button class="rounded-md px-2.5 py-1.5 ring-1 ring-zinc-200 hover:bg-zinc-50" aria-label="Save">
                        <i data-lucide="bookmark" class="w-4 h-4 text-zinc-700"></i>
                      </button>
                    </div>
                  </td>
                </tr>
              </tbody>
            </table>
          </div>

          <!-- Mobile Cards (accessible duplication for small screens) -->
          <div class="md:hidden divide-y divide-zinc-100">
            <div class="p-4">
              <p class="text-sm font-medium">Product Analyst Intern</p>
              <p class="text-xs text-zinc-600">InsightWorks • Remote • $1,200/mo • 3 months</p>
              <div class="mt-2 flex items-center justify-between">
                <div class="flex items-center gap-2">
                  <div class="h-2 w-24 bg-zinc-100 rounded-full overflow-hidden"><div class="h-full w-[92%] bg-emerald-500"></div></div>
                  <span class="text-xs text-zinc-700">92%</span>
                </div>
                <div class="flex items-center gap-2">
                  <button class="rounded-md px-3 py-1.5 text-xs text-white bg-zinc-900 hover:bg-zinc-800">Apply</button>
                  <button class="rounded-md px-2.5 py-1.5 ring-1 ring-zinc-200 hover:bg-zinc-50" aria-label="Save">
                    <i data-lucide="bookmark" class="w-4 h-4 text-zinc-700"></i>
                  </button>
                </div>
              </div>
            </div>
            <div class="p-4">
              <p class="text-sm font-medium">Associate PM Intern</p>
              <p class="text-xs text-zinc-600">NovaTech • London • £900/mo • 6 months</p>
              <div class="mt-2 flex items-center justify-between">
                <div class="flex items-center gap-2">
                  <div class="h-2 w-24 bg-zinc-100 rounded-full overflow-hidden"><div class="h-full w-[86%] bg-emerald-500"></div></div>
                  <span class="text-xs text-zinc-700">86%</span>
                </div>
                <div class="flex items-center gap-2">
                  <button class="rounded-md px-3 py-1.5 text-xs text-white bg-zinc-900 hover:bg-zinc-800">Apply</button>
                  <button class="rounded-md px-2.5 py-1.5 ring-1 ring-zinc-200 hover:bg-zinc-50" aria-label="Save">
                    <i data-lucide="bookmark" class="w-4 h-4 text-zinc-700"></i>
                  </button>
                </div>
              </div>
            </div>
            <div class="p-4">
              <p class="text-sm font-medium">Growth PM Intern</p>
              <p class="text-xs text-zinc-600">BrightPath • Berlin • €1,000/mo • 4 months</p>
              <div class="mt-2 flex items-center justify-between">
                <div class="flex items-center gap-2">
                  <div class="h-2 w-24 bg-zinc-100 rounded-full overflow-hidden"><div class="h-full w-[78%] bg-emerald-500"></div></div>
                  <span class="text-xs text-zinc-700">78%</span>
                </div>
                <div class="flex items-center gap-2">
                  <button class="rounded-md px-3 py-1.5 text-xs text-white bg-zinc-900 hover:bg-zinc-800">Apply</button>
                  <button class="rounded-md px-2.5 py-1.5 ring-1 ring-zinc-200 hover:bg-zinc-50" aria-label="Save">
                    <i data-lucide="bookmark" class="w-4 h-4 text-zinc-700"></i>
                  </button>
                </div>
              </div>
            </div>
          </div>
        </section>

        <!-- Footer -->
        <footer class="py-8">
          <div class="text-center text-xs text-zinc-500">
            © 2025 PathFinder. Intelligent recommendations powered by your profile skills and preferences.
          </div>
        </footer>
      </div>
    </main>

    <script>
      // Initialize icons
      window.addEventListener('DOMContentLoaded', () => {
        lucide.createIcons({ attrs: { strokeWidth: 1.5 } });
      });

      // Sidebar toggle logic
      const sidebar = document.getElementById('sidebar');
      const main = document.getElementById('mainContent');
      const collapseBtn = document.getElementById('collapseBtn');
      const mobileSidebarToggle = document.getElementById('mobileSidebarToggle');
      const sidebarLabels = () => Array.from(sidebar.querySelectorAll('.sidebar-label'));

      let isCollapsed = false;

      function applySidebarState() {
        if (window.innerWidth >= 768) {
          // Desktop
          if (isCollapsed) {
            sidebar.classList.remove('w-72');
            sidebar.classList.add('w-20');
            main.classList.remove('md:pl-72');
            main.classList.add('md:pl-24');
            sidebarLabels().forEach(el => el.classList.add('hidden'));
          } else {
            sidebar.classList.remove('w-20');
            sidebar.classList.add('w-72');
            main.classList.remove('md:pl-24');
            main.classList.add('md:pl-72');
            sidebarLabels().forEach(el => el.classList.remove('hidden'));
          }
          sidebar.classList.remove('-translate-x-full');
        } else {
          // Mobile
          sidebar.classList.add('w-72');
          main.classList.remove('md:pl-24', 'md:pl-72');
        }
      }

      collapseBtn.addEventListener('click', () => {
        isCollapsed = !isCollapsed;
        const icon = collapseBtn.querySelector('svg');
        icon.setAttribute('data-lucide', isCollapsed ? 'panel-left-open' : 'panel-left-close');
        lucide.createIcons({ attrs: { strokeWidth: 1.5 } });
        applySidebarState();
      });

      mobileSidebarToggle.addEventListener('click', () => {
        const hidden = sidebar.classList.contains('-translate-x-full');
        if (hidden) {
          sidebar.classList.remove('-translate-x-full');
        } else {
          sidebar.classList.add('-translate-x-full');
        }
      });

      window.addEventListener('resize', applySidebarState);
      applySidebarState();

      // Profile dropdown
      const profileBtn = document.getElementById('profileBtn');
      const profileMenu = document.getElementById('profileMenu');
      profileBtn.addEventListener('click', (e) => {
        e.stopPropagation();
        profileMenu.classList.toggle('hidden');
      });
      document.addEventListener('click', (e) => {
        if (!profileMenu.contains(e.target) && !profileBtn.contains(e.target)) {
          profileMenu.classList.add('hidden');
        }
      });

      // Chart.js - Overall Match doughnut
      const ctx = document.getElementById('matchChart');
      if (ctx) {
        new Chart(ctx, {
          type: 'doughnut',
          data: {
            labels: ['Match', 'Gap'],
            datasets: [{
              data: [82, 18],
              backgroundColor: ['#10b981', '#e5e7eb'],
              borderWidth: 0
            }]
          },
          options: {
            responsive: true,
            maintainAspectRatio: false,
            cutout: '70%',
            plugins: {
              legend: { display: false },
              tooltip: { enabled: true }
            }
          }
        });
      }

      // Resume Filter interactions
      const resumeInput = document.getElementById('resumeInput');
      const resumeUploadBtn = document.getElementById('resumeUploadBtn');
      const applyResumeFilterBtn = document.getElementById('applyResumeFilterBtn');
      const resumeFileName = document.getElementById('resumeFileName');
      const resumeStatus = document.getElementById('resumeStatus');

      if (resumeUploadBtn && resumeInput) {
        resumeUploadBtn.addEventListener('click', () => resumeInput.click());
        resumeInput.addEventListener('change', () => {
          const file = resumeInput.files && resumeInput.files[0];
          if (file) {
            resumeFileName.textContent = file.name;
            applyResumeFilterBtn.disabled = false;
            resumeStatus.textContent = '';
          } else {
            resumeFileName.textContent = '';
            applyResumeFilterBtn.disabled = true;
          }
        });
      }

      if (applyResumeFilterBtn) {
        applyResumeFilterBtn.addEventListener('click', () => {
          // Placeholder for filtering logic
          resumeStatus.textContent = 'Resume filter applied';
          setTimeout(() => { resumeStatus.textContent = ''; }, 2500);
        });
      }
    </script>
  </body>
</html>
