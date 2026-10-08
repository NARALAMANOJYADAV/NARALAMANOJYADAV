"""Generates animated SVG assets for the GitHub profile README.
Edit the TEXT in the CONTENT section below, then run:  python generate_assets.py
"""
import random, html, os

OUT = os.path.join(os.path.dirname(os.path.abspath(__file__)), "assets")
os.makedirs(OUT, exist_ok=True)
SANS = "'Segoe UI',Ubuntu,'Helvetica Neue',Arial,sans-serif"
MONO = "'Fira Code','JetBrains Mono','Courier New',monospace"
CYAN, PURPLE, PINK, GREEN = "#00e5ff", "#8b5cf6", "#ff4d9d", "#3ddc97"
e = html.escape

def save(name, svg):
    with open(os.path.join(OUT, name), "w", encoding="utf-8") as f:
        f.write(svg)

# ===================== CONTENT (edit here) =====================
NAME = "NARALA MANOJ"
SUBTITLE = "B.TECH  ·  AI & DATA SCIENCE   |   FULL STACK DEVELOPER"
ROLES = ["Building full-stack web apps", "Exploring AI & Data Science", "Open to work - let's collaborate"]

TERMINAL = [  # (prompt command, output, output color)
    ("whoami", "narala_manoj", CYAN),
    ("cat role.txt", "Full Stack Developer | B.Tech AI & Data Science", "#c9d1d9"),
    ("echo $LOCATION", "Nellore, India", "#c9d1d9"),
    ("ls skills/", "python  java  typescript  django  sqlite  git", PURPLE),
    ("./status.sh", "open_to_work = true   [OK]", GREEN),
]

PROJECTS = [  # file, title, desc lines, tags, accent, badge
    ("card-counseling.svg", "Counseling System",
     ["Django app for student counseling with", "admin & approval-user roles. Deploy-ready."],
     ["Python", "Django", "SQLite", "Render"], CYAN, "52+ commits"),
    ("card-ai-traveller.svg", "AI Travel Planner",
     ["AI-powered trip planning tool built", "in Python. Early-stage and evolving."],
     ["Python", "AI"], PURPLE, "AI project"),
    ("card-club.svg", "Club",
     ["Club web application built with", "TypeScript."],
     ["TypeScript", "Web"], PINK, "Web app"),
    ("card-handi.svg", "Handi",
     ["TypeScript web application.", "Edit this line with your feature."],
     ["TypeScript", "Web"], GREEN, "Web app"),
    ("card-helmate.svg", "Helmate",
     ["HTML web project.", "Edit this line with your feature."],
     ["HTML", "CSS"], "#ffb020", "Web project"),
    ("card-restaurant.svg", "Advanced Restaurant",
     ["Restaurant website built with HTML.", "Edit this line with your feature."],
     ["HTML", "CSS"], "#ff6b6b", "Website"),
]

CHIPS_1 = ["Python", "Java", "TypeScript", "JavaScript", "HTML5", "CSS3", "Django", "SQLite", "Data Science", "AI"]
CHIPS_2 = ["Git", "GitHub", "VS Code", "Render", "REST APIs", "Responsive UI", "Problem Solving", "Teamwork", "Full Stack"]
# ===============================================================

def header():
    W, H = 900, 300
    random.seed(7)
    orbs = []
    for _ in range(26):
        x, y, r = random.randint(10, W-10), random.randint(60, H-10), random.uniform(1.5, 6)
        col = random.choice([CYAN, PURPLE, PINK, "#ffffff"])
        d, b = random.uniform(6, 14), -random.uniform(0, 12)
        orbs.append(f'<circle cx="{x}" cy="{y}" r="{r:.1f}" fill="{col}" filter="url(#glow)">'
                    f'<animate attributeName="cy" values="{y};{y-90};{y}" dur="{d:.1f}s" begin="{b:.1f}s" repeatCount="indefinite"/>'
                    f'<animate attributeName="opacity" values="0.1;0.95;0.1" dur="{d:.1f}s" begin="{b:.1f}s" repeatCount="indefinite"/></circle>')
    blobs = (
        f'<circle r="130" fill="{PURPLE}" opacity="0.35" filter="url(#blur)"><animate attributeName="cx" values="120;420;120" dur="14s" repeatCount="indefinite"/><animate attributeName="cy" values="80;220;80" dur="11s" repeatCount="indefinite"/></circle>'
        f'<circle r="140" fill="{CYAN}" opacity="0.28" filter="url(#blur)"><animate attributeName="cx" values="780;480;780" dur="16s" repeatCount="indefinite"/><animate attributeName="cy" values="240;70;240" dur="13s" repeatCount="indefinite"/></circle>'
        f'<circle r="110" fill="{PINK}" opacity="0.22" filter="url(#blur)"><animate attributeName="cx" values="450;650;250;450" dur="18s" repeatCount="indefinite"/><animate attributeName="cy" values="150;260;60;150" dur="15s" repeatCount="indefinite"/></circle>')
    typed = []
    n = len(ROLES)
    cw = 12.0
    for i, t in enumerate(ROLES):
        w = len(t) * cw; x0 = 450 - w / 2
        a, b, c, d = i / n, i / n + 0.10, i / n + 0.26, (i + 1) / n - 0.001
        kt = f"0;{a:.3f};{b:.3f};{c:.3f};{d:.3f};1"
        typed.append(
            f'<clipPath id="c{i}"><rect x="{x0:.1f}" y="205" height="40" width="0"><animate attributeName="width" values="0;0;{w:.0f};{w:.0f};0;0" keyTimes="{kt}" dur="13s" repeatCount="indefinite"/></rect></clipPath>'
            f'<text x="{x0:.1f}" y="232" font-family="{MONO}" font-size="20" fill="#e6f1ff" clip-path="url(#c{i})">{e(t)}</text>'
            f'<rect y="210" width="3" height="26" fill="{CYAN}" x="{x0:.1f}">'
            f'<animate attributeName="x" values="{x0:.1f};{x0:.1f};{x0+w:.1f};{x0+w:.1f};{x0:.1f};{x0:.1f}" keyTimes="{kt}" dur="13s" repeatCount="indefinite"/>'
            f'<animate attributeName="opacity" values="0;0;1;1;0;0" keyTimes="{kt}" dur="13s" repeatCount="indefinite"/></rect>')
    return f'''<svg xmlns="http://www.w3.org/2000/svg" width="{W}" height="{H}" viewBox="0 0 {W} {H}" role="img" aria-label="Narala Manoj - AI and Data Science, Full Stack Developer">
<defs>
<clipPath id="round"><rect width="{W}" height="{H}" rx="22"/></clipPath>
<linearGradient id="bg" x1="0" y1="0" x2="1" y2="1"><stop offset="0" stop-color="#070b18"/><stop offset="0.5" stop-color="#0d1530"><animate attributeName="stop-color" values="#0d1530;#1a1040;#0b2036;#0d1530" dur="12s" repeatCount="indefinite"/></stop><stop offset="1" stop-color="#050812"/></linearGradient>
<pattern id="grid" width="40" height="40" patternUnits="userSpaceOnUse"><path d="M40 0H0V40" fill="none" stroke="#5b8cff" stroke-opacity="0.10" stroke-width="1"/><animateTransform attributeName="patternTransform" type="translate" from="0 0" to="40 40" dur="6s" repeatCount="indefinite"/></pattern>
<linearGradient id="tg" gradientUnits="userSpaceOnUse" x1="0" y1="0" x2="450" y2="0" spreadMethod="reflect"><stop offset="0" stop-color="{CYAN}"/><stop offset="0.5" stop-color="{PURPLE}"/><stop offset="1" stop-color="{PINK}"/><animateTransform attributeName="gradientTransform" type="translate" from="0 0" to="900 0" dur="6s" repeatCount="indefinite"/></linearGradient>
<linearGradient id="sweep" gradientUnits="userSpaceOnUse" x1="0" x2="300" y1="0" y2="0" spreadMethod="repeat"><stop offset="0" stop-color="{CYAN}" stop-opacity="0"/><stop offset="0.5" stop-color="{CYAN}"/><stop offset="1" stop-color="{PINK}" stop-opacity="0"/><animateTransform attributeName="gradientTransform" type="translate" from="-300 0" to="900 0" dur="3.5s" repeatCount="indefinite"/></linearGradient>
<filter id="glow" x="-300%" y="-300%" width="700%" height="700%"><feGaussianBlur stdDeviation="2.5" result="b"/><feMerge><feMergeNode in="b"/><feMergeNode in="SourceGraphic"/></feMerge></filter>
<filter id="blur" x="-50%" y="-50%" width="200%" height="200%"><feGaussianBlur stdDeviation="55"/></filter>
<filter id="tglow" x="-20%" y="-50%" width="140%" height="200%"><feGaussianBlur stdDeviation="6" result="b"/><feMerge><feMergeNode in="b"/><feMergeNode in="SourceGraphic"/></feMerge></filter>
</defs>
<g clip-path="url(#round)">
<rect width="{W}" height="{H}" fill="url(#bg)"/>
{blobs}
<rect width="{W}" height="{H}" fill="url(#grid)"/>
{''.join(orbs)}
<rect width="{W}" height="2" fill="#ffffff" opacity="0.06"><animate attributeName="y" values="0;{H};0" dur="7s" repeatCount="indefinite"/></rect>
<text x="450" y="132" text-anchor="middle" font-family="{SANS}" font-size="66" font-weight="800" letter-spacing="5" fill="url(#tg)" filter="url(#tglow)">{e(NAME)}<animate attributeName="opacity" values="0;1" dur="1.4s" fill="freeze"/></text>
<text x="450" y="172" text-anchor="middle" font-family="{SANS}" font-size="14" letter-spacing="3" fill="#9fb3d9">{e(SUBTITLE)}<animate attributeName="opacity" values="0;1" dur="2s" fill="freeze"/></text>
<line x1="330" y1="188" x2="570" y2="188" stroke="{CYAN}" stroke-opacity="0.4"/>
{''.join(typed)}
<rect y="{H-4}" width="{W}" height="4" fill="url(#sweep)"/>
</g>
<rect x="1" y="1" width="{W-2}" height="{H-2}" rx="21" fill="none" stroke="{CYAN}" stroke-opacity="0.25"/>
</svg>'''

def title(name, text, sub):
    W, H = 900, 70
    return f'''<svg xmlns="http://www.w3.org/2000/svg" width="{W}" height="{H}" viewBox="0 0 {W} {H}" role="img" aria-label="{e(text)}">
<defs><linearGradient id="g" x1="0" x2="1"><stop offset="0" stop-color="{CYAN}"/><stop offset="1" stop-color="{PINK}"/></linearGradient>
<linearGradient id="run" gradientUnits="userSpaceOnUse" x1="0" x2="260" spreadMethod="repeat"><stop offset="0" stop-color="{CYAN}" stop-opacity="0"/><stop offset="0.5" stop-color="#fff"/><stop offset="1" stop-color="{PINK}" stop-opacity="0"/><animateTransform attributeName="gradientTransform" type="translate" from="-260 0" to="900 0" dur="3s" repeatCount="indefinite"/></linearGradient></defs>
<rect x="0" y="14" width="6" height="38" rx="3" fill="url(#g)"><animate attributeName="height" values="38;24;38" dur="2s" repeatCount="indefinite"/></rect>
<text x="22" y="38" font-family="{SANS}" font-size="30" font-weight="800" letter-spacing="2" fill="#e6f1ff">{e(text)}</text>
<text x="22" y="58" font-family="{MONO}" font-size="12" fill="#6b7fa8">{e(sub)}</text>
<rect x="0" y="66" width="{W}" height="2" fill="#1b2744"/><rect x="0" y="66" width="{W}" height="2" fill="url(#run)"/>
</svg>'''

def terminal():
    W, H = 900, 300
    lines = []
    n = len(TERMINAL); total = 16
    cw = 9.6
    for i, (cmd, out, col) in enumerate(TERMINAL):
        y = 98 + i * 40
        s = (0.5 + i * 2.4) / total
        t1 = s + 0.5 / total
        w1 = (len(cmd) + 2) * cw
        s2 = t1 + 0.1 / total
        t2 = s2 + 0.9 / total
        w2 = len(out) * cw
        end = 0.93
        lines.append(
            f'<text x="34" y="{y}" font-family="{MONO}" font-size="16" fill="{GREEN}">$</text>'
            f'<clipPath id="a{i}"><rect x="56" y="{y-18}" height="26" width="0"><animate attributeName="width" values="0;0;{w1:.0f};{w1:.0f};0;0" keyTimes="0;{s:.3f};{t1:.3f};{end};{end+0.01};1" dur="{total}s" repeatCount="indefinite"/></rect></clipPath>'
            f'<text x="56" y="{y}" font-family="{MONO}" font-size="16" fill="#e6f1ff" clip-path="url(#a{i})">{e(cmd)}</text>'
            f'<clipPath id="b{i}"><rect x="260" y="{y-18}" height="26" width="0"><animate attributeName="width" values="0;0;{w2:.0f};{w2:.0f};0;0" keyTimes="0;{s2:.3f};{t2:.3f};{end};{end+0.01};1" dur="{total}s" repeatCount="indefinite"/></rect></clipPath>'
            f'<text x="260" y="{y}" font-family="{MONO}" font-size="16" fill="{col}" clip-path="url(#b{i})">{e(out)}</text>')
    return f'''<svg xmlns="http://www.w3.org/2000/svg" width="{W}" height="{H}" viewBox="0 0 {W} {H}" role="img" aria-label="Terminal intro about Narala Manoj">
<defs>
<linearGradient id="tb" x1="0" y1="0" x2="1" y2="1"><stop offset="0" stop-color="#0b1020"/><stop offset="1" stop-color="#0e1730"/></linearGradient>
<linearGradient id="bd" gradientUnits="userSpaceOnUse" x1="0" y1="0" x2="900" y2="0" spreadMethod="reflect"><stop offset="0" stop-color="{CYAN}"/><stop offset="0.5" stop-color="{PURPLE}"/><stop offset="1" stop-color="{PINK}"/><animateTransform attributeName="gradientTransform" type="translate" from="0 0" to="1800 0" dur="8s" repeatCount="indefinite"/></linearGradient>
<pattern id="scan" width="4" height="4" patternUnits="userSpaceOnUse"><rect width="4" height="1" fill="#fff" opacity="0.025"/></pattern>
</defs>
<rect x="1.5" y="1.5" width="{W-3}" height="{H-3}" rx="16" fill="url(#tb)" stroke="url(#bd)" stroke-width="2"/>
<rect x="1.5" y="1.5" width="{W-3}" height="40" rx="16" fill="#131c38"/><rect x="1.5" y="26" width="{W-3}" height="16" fill="#131c38"/>
<circle cx="28" cy="22" r="6" fill="#ff5f56"/><circle cx="50" cy="22" r="6" fill="#ffbd2e"/><circle cx="72" cy="22" r="6" fill="#27c93f"/>
<text x="450" y="27" text-anchor="middle" font-family="{MONO}" font-size="13" fill="#7f93bd">manoj@portfolio: ~</text>
{''.join(lines)}
<rect x="3" y="44" width="{W-6}" height="{H-48}" fill="url(#scan)"/>
<rect x="34" y="{98+n*40-22}" width="9" height="18" fill="{CYAN}"><animate attributeName="opacity" values="1;0;1" dur="1s" repeatCount="indefinite"/></rect>
</svg>'''

def chips():
    W, H = 900, 190
    def row(items, y, direction, dur):
        pills, x = [], 0
        widths = [len(t) * 8.6 + 36 for t in items]
        for t, w in zip(items, widths):
            c = [CYAN, PURPLE, PINK, GREEN][len(pills) % 4]
            pills.append(f'<g transform="translate({x:.0f},0)"><rect width="{w:.0f}" height="38" rx="19" fill="#0e1730" stroke="{c}" stroke-opacity="0.7"/><circle cx="18" cy="19" r="4" fill="{c}"><animate attributeName="opacity" values="1;0.3;1" dur="2s" begin="-{len(pills)*0.3:.1f}s" repeatCount="indefinite"/></circle><text x="30" y="24" font-family="{SANS}" font-size="14" font-weight="600" fill="#e6f1ff">{e(t)}</text></g>')
            x += w + 14
        total = x
        a, b = (0, -total) if direction == "l" else (-total, 0)
        grp = "".join(pills)
        return (f'<g transform="translate(0,{y})"><g><animateTransform attributeName="transform" type="translate" from="{a:.0f} 0" to="{b:.0f} 0" dur="{dur}s" repeatCount="indefinite"/>'
                f'{grp}<g transform="translate({total:.0f},0)">{grp}</g><g transform="translate({total*2:.0f},0)">{grp}</g></g></g>')
    return f'''<svg xmlns="http://www.w3.org/2000/svg" width="{W}" height="{H}" viewBox="0 0 {W} {H}" role="img" aria-label="Tech stack">
<defs><linearGradient id="fade" x1="0" x2="1"><stop offset="0" stop-color="#fff" stop-opacity="0"/><stop offset="0.08" stop-color="#fff"/><stop offset="0.92" stop-color="#fff"/><stop offset="1" stop-color="#fff" stop-opacity="0"/></linearGradient>
<mask id="m"><rect width="{W}" height="{H}" fill="url(#fade)"/></mask>
<linearGradient id="bgc" x1="0" y1="0" x2="1" y2="1"><stop offset="0" stop-color="#080d1c"/><stop offset="1" stop-color="#0c1430"/></linearGradient></defs>
<rect width="{W}" height="{H}" rx="18" fill="url(#bgc)"/>
<rect x="1" y="1" width="{W-2}" height="{H-2}" rx="17" fill="none" stroke="#1b2744"/>
<g mask="url(#m)">{row(CHIPS_1, 38, "l", 38)}{row(CHIPS_2, 108, "r", 42)}</g>
</svg>'''

def card(title_t, desc, tags, accent, badge):
    W, H = 440, 230
    random.seed(len(title_t))
    dots = "".join(
        f'<circle cx="{random.randint(20,420)}" cy="{random.randint(20,210)}" r="{random.uniform(1,2.5):.1f}" fill="{accent}" opacity="0.5"><animate attributeName="opacity" values="0.1;0.8;0.1" dur="{random.uniform(2,5):.1f}s" begin="-{random.uniform(0,4):.1f}s" repeatCount="indefinite"/></circle>'
        for _ in range(14))
    tg, x = [], 24
    for t in tags:
        w = len(t) * 8 + 24
        tg.append(f'<g transform="translate({x},166)"><rect width="{w}" height="26" rx="13" fill="{accent}" fill-opacity="0.12" stroke="{accent}" stroke-opacity="0.6"/><text x="{w/2}" y="18" text-anchor="middle" font-family="{MONO}" font-size="12" fill="{accent}">{e(t)}</text></g>')
        x += w + 8
    bw = len(badge) * 7.2 + 24
    d = "".join(f'<text x="24" y="{104+i*22}" font-family="{SANS}" font-size="14" fill="#a9b8d6">{e(l)}</text>' for i, l in enumerate(desc))
    return f'''<svg xmlns="http://www.w3.org/2000/svg" width="{W}" height="{H}" viewBox="0 0 {W} {H}" role="img" aria-label="{e(title_t)} project card">
<defs>
<linearGradient id="bg" x1="0" y1="0" x2="1" y2="1"><stop offset="0" stop-color="#0a1022"/><stop offset="1" stop-color="#0f1a38"/></linearGradient>
<radialGradient id="spot" cx="0" cy="0" r="220" gradientUnits="userSpaceOnUse"><stop offset="0" stop-color="{accent}" stop-opacity="0.28"/><stop offset="1" stop-color="{accent}" stop-opacity="0"/><animateTransform attributeName="gradientTransform" type="translate" values="0 0;440 0;440 230;0 230;0 0" dur="12s" repeatCount="indefinite"/></radialGradient>
<filter id="gl" x="-20%" y="-20%" width="140%" height="140%"><feGaussianBlur stdDeviation="3" result="b"/><feMerge><feMergeNode in="b"/><feMergeNode in="SourceGraphic"/></feMerge></filter>
<clipPath id="cl"><rect x="2" y="2" width="{W-4}" height="{H-4}" rx="18"/></clipPath>
</defs>
<rect x="2" y="2" width="{W-4}" height="{H-4}" rx="18" fill="url(#bg)"/>
<g clip-path="url(#cl)"><rect width="{W}" height="{H}" fill="url(#spot)"/>{dots}</g>
<rect x="2" y="2" width="{W-4}" height="{H-4}" rx="18" fill="none" stroke="{accent}" stroke-opacity="0.25"/>
<rect x="2" y="2" width="{W-4}" height="{H-4}" rx="18" fill="none" stroke="{accent}" stroke-width="2.5" pathLength="100" stroke-dasharray="14 86" stroke-linecap="round" filter="url(#gl)"><animate attributeName="stroke-dashoffset" from="100" to="0" dur="5s" repeatCount="indefinite"/></rect>
<circle cx="32" cy="38" r="5" fill="{accent}"><animate attributeName="r" values="4;7;4" dur="2s" repeatCount="indefinite"/><animate attributeName="opacity" values="1;0.4;1" dur="2s" repeatCount="indefinite"/></circle>
<text x="48" y="45" font-family="{SANS}" font-size="22" font-weight="800" fill="#f0f6ff">{e(title_t)}</text>
<g transform="translate({W-bw-20},24)"><rect width="{bw:.0f}" height="24" rx="12" fill="#ffffff" fill-opacity="0.06"/><text x="{bw/2:.0f}" y="16" text-anchor="middle" font-family="{MONO}" font-size="11" fill="#9fb3d9">{e(badge)}</text></g>
<line x1="24" y1="64" x2="{W-24}" y2="64" stroke="{accent}" stroke-opacity="0.25"/>
{d}
{''.join(tg)}
<text x="24" y="216" font-family="{MONO}" font-size="12" fill="{accent}">view repository -&gt;<animate attributeName="opacity" values="1;0.5;1" dur="2.5s" repeatCount="indefinite"/></text>
</svg>'''

def footer():
    W, H = 900, 200
    waves = ""
    for i, (col, op, amp, dur, y) in enumerate([(CYAN, 0.35, 28, 7, 120), (PURPLE, 0.40, 22, 10, 135), (PINK, 0.45, 16, 13, 150)]):
        seg = "t150,0 " * 11
        path = f"M0,{y} q75,-{amp} 150,0 {seg}V{H} H0 Z"
        waves += f'<path d="{path}" fill="{col}" fill-opacity="{op}"><animateTransform attributeName="transform" type="translate" from="{-300 if i%2==0 else 0} 0" to="{0 if i%2==0 else -300} 0" dur="{dur}s" repeatCount="indefinite"/></path>'
    return f'''<svg xmlns="http://www.w3.org/2000/svg" width="{W}" height="{H}" viewBox="0 0 {W} {H}" role="img" aria-label="Let's build something together">
<defs><clipPath id="r"><rect width="{W}" height="{H}" rx="22"/></clipPath>
<linearGradient id="bg" x1="0" y1="0" x2="0" y2="1"><stop offset="0" stop-color="#070b18"/><stop offset="1" stop-color="#101a3a"/></linearGradient>
<linearGradient id="tg" gradientUnits="userSpaceOnUse" x1="0" x2="450" spreadMethod="reflect"><stop offset="0" stop-color="{CYAN}"/><stop offset="0.5" stop-color="{PURPLE}"/><stop offset="1" stop-color="{PINK}"/><animateTransform attributeName="gradientTransform" type="translate" from="0 0" to="900 0" dur="6s" repeatCount="indefinite"/></linearGradient>
<filter id="g"><feGaussianBlur stdDeviation="5" result="b"/><feMerge><feMergeNode in="b"/><feMergeNode in="SourceGraphic"/></feMerge></filter></defs>
<g clip-path="url(#r)"><rect width="{W}" height="{H}" fill="url(#bg)"/>{waves}
<text x="450" y="70" text-anchor="middle" font-family="{SANS}" font-size="34" font-weight="800" letter-spacing="2" fill="url(#tg)" filter="url(#g)">LET'S BUILD SOMETHING TOGETHER<animate attributeName="opacity" values="1;0.75;1" dur="3s" repeatCount="indefinite"/></text>
<text x="450" y="98" text-anchor="middle" font-family="{MONO}" font-size="13" fill="#8da2cc">open to internships &amp; entry-level roles</text></g>
</svg>'''

save("header.svg", header())
save("title-about.svg", title("about", "ABOUT ME", "// who I am"))
save("title-stack.svg", title("stack", "TECH STACK", "// tools I work with"))
save("title-projects.svg", title("projects", "FEATURED PROJECTS", "// things I've built"))
save("title-insights.svg", title("insights", "GITHUB INSIGHTS", "// activity & languages"))
save("title-connect.svg", title("connect", "LET'S CONNECT", "// say h
