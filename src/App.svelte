<script lang="ts">
  import { onMount } from 'svelte'

  const logos = ['Bally’s Colombo', 'Dialog', 'Commercial Bank', 'Virtually', 'Softlogic', 'LB Finance PLC']
  const features = [
    ['Automation', 'Orchestrate approvals, documents, and payments with visual workflows.'],
    ['AI Intelligence', 'Agents that classify, route, summarize, and recommend next actions.'],
    ['Data & Analytics', 'Live dashboards, health scores, and operational intelligence.'],
    ['Identity', 'Secure onboarding, KYC, user roles, and audit trails.'],
    ['Documents', 'Generate, sign, archive, and reconcile every business document.'],
    ['Payments', 'Collect, settle, reconcile, and report with enterprise-grade control.']
  ]
  const stats = [
    ['99.98%', 'platform uptime'],
    ['1.2M+', 'transactions processed'],
    ['42%', 'reduction in manual work'],
    ['8x', 'faster deployment']
  ]

  let mouseX = 0
  let mouseY = 0
  let mounted = false

  onMount(() => {
    mounted = true
    const onMove = (event: PointerEvent) => {
      mouseX = (event.clientX / window.innerWidth - 0.5) * 2
      mouseY = (event.clientY / window.innerHeight - 0.5) * 2
    }

    const revealObserver = new IntersectionObserver(
      entries => {
        entries.forEach(entry => {
          if (entry.isIntersecting) entry.target.classList.add('is-visible')
        })
      },
      { threshold: 0.18 }
    )

    document.querySelectorAll('.reveal').forEach(el => revealObserver.observe(el))
    window.addEventListener('pointermove', onMove, { passive: true })

    return () => {
      window.removeEventListener('pointermove', onMove)
      revealObserver.disconnect()
    }
  })
</script>

<svelte:head>
  <title>NEXORA — Modern Business Operating System</title>
  <meta name="description" content="A premium animated SaaS landing page for NEXORA." />
</svelte:head>

<main class:mounted>
  <section class="hero" aria-labelledby="hero-title">
    <nav class="nav" aria-label="Main navigation">
      <a class="brand" href="#top" aria-label="Nexora home">
        <span class="brand-orbit"><i></i></span>
        <span>NEXORA</span>
      </a>
      <div class="nav-links">
        <a href="#products">Products</a>
        <a href="#solutions">Solutions</a>
        <a href="#pricing">Pricing</a>
        <a href="#company">Company</a>
      </div>
      <a class="demo-btn" href="#demo">Book Demo <span>→</span></a>
    </nav>

    <div class="hero-grid" id="top">
      <div class="hero-copy reveal">
        <p class="eyebrow"><span></span> intelligent business infrastructure</p>
        <h1 id="hero-title">The Operating System for <em>Modern Business.</em></h1>
        <p class="lede">Connect payments, identity, documents, automation, and AI into one intelligent platform designed for fast-moving teams.</p>
        <div class="hero-actions">
          <a class="primary" href="#demo">Get Started <span>→</span></a>
          <a class="secondary" href="#video"><span class="play">▶</span> Watch Demo</a>
        </div>
      </div>

      <div
        class="hero-visual reveal"
        style={`--mx:${mouseX.toFixed(3)}; --my:${mouseY.toFixed(3)}`}
        aria-label="Animated NEXORA analytics dashboard"
      >
        <div class="glass-panel panel-a"></div>
        <div class="glass-panel panel-b"></div>
        {@render Dashboard(true, false)}
      </div>
    </div>

    <div class="trust reveal">
      <p>Trusted by businesses across Sri Lanka and beyond</p>
      <div class="logo-row" aria-label="Customer logos">
        {#each logos as logo}
          <span>{logo}</span>
        {/each}
      </div>
    </div>
  </section>

  <section class="split section-one reveal" id="products">
    <div class="section-index">01</div>
    <div class="mock-card light-card">
      <div class="card-toolbar"><span></span><span></span><span></span></div>
      <div class="invoice-head"><b>Invoice Flow</b><small>Today</small></div>
      <div class="invoice-total">LKR 2.4M</div>
      <div class="invoice-lines">
        <i style="--w:76%"></i><i style="--w:52%"></i><i style="--w:88%"></i><i style="--w:42%"></i>
      </div>
      <div class="approval-chip">Approved by AI Agent</div>
    </div>
    <article>
      <p class="kicker">Unified platform</p>
      <h2>One platform. Every workflow.</h2>
      <p>Bring your entire operating layer into one connected surface — from approvals and documents to payments, customer records, and compliance trails.</p>
      <a href="#platform">Explore Platform →</a>
    </article>
  </section>

  <section class="split reverse reveal" id="solutions">
    <article>
      <p class="section-index">02</p>
      <p class="kicker">Applied intelligence</p>
      <h2>AI that actually works.</h2>
      <p>NEXORA learns the rhythm of your business, understands patterns, routes work, flags risk, and completes repetitive tasks without adding complexity.</p>
      <a href="#ai">See AI in Action →</a>
    </article>
    <div class="workflow-card" aria-label="Animated AI workflow">
      <div class="workflow-title">AI Workflow</div>
      <svg viewBox="0 0 760 210" role="img" aria-label="Email received to payment sent workflow">
        <defs>
          <linearGradient id="flowGold" x1="0" x2="1">
            <stop offset="0" stop-color="#aa7b31" />
            <stop offset="1" stop-color="#f0c878" />
          </linearGradient>
        </defs>
        <path class="flow-path" d="M90 106 C 185 22, 246 188, 340 106 S 500 22, 590 106 S 680 176, 716 92" />
        {#each ['Email Received', 'AI Agent', 'Approval', 'Invoice Generated', 'Payment Sent'] as step, i}
          <g class="node" style={`--i:${i}`} transform={`translate(${80 + i * 150},106)`}>
            <circle r="33"></circle>
            <text y="70" text-anchor="middle">{step}</text>
          </g>
        {/each}
      </svg>
    </div>
  </section>

  <section class="split analytics-section reveal" id="pricing">
    <div class="mini-dashboard-wrap">{@render Dashboard(true, true)}</div>
    <article>
      <p class="section-index">03</p>
      <p class="kicker">Live command center</p>
      <h2>Real-time visibility.</h2>
      <p>See revenue, workflows, approvals, cash movement, and operational risk in one real-time analytics layer built for executives and operators.</p>
      <a href="#analytics">View Analytics →</a>
    </article>
  </section>

  <section class="features reveal" id="company">
    <p class="kicker">Scale without sprawl</p>
    <h2>Everything you need to scale</h2>
    <div class="feature-grid">
      {#each features as feature, i}
        <article class:highlight={i === 5}>
          <div class="feature-icon">{i + 1}</div>
          <h3>{feature[0]}</h3>
          <p>{feature[1]}</p>
        </article>
      {/each}
    </div>
  </section>

  <section class="stats reveal" aria-label="Nexora metrics">
    {#each stats as stat}
      <div>
        <strong>{stat[0]}</strong>
        <span>{stat[1]}</span>
      </div>
    {/each}
  </section>

  <section class="testimonial reveal">
    <article>
      <div class="quote-mark">“</div>
      <blockquote>This completely changed how we run our business.</blockquote>
      <p>CEO, Leading Financial Services Company</p>
    </article>
    <div class="office-art" aria-label="Abstract modern office image">
      <span></span><span></span><span></span><i></i>
    </div>
  </section>

  <section class="final-cta reveal" id="demo">
    <svg class="cta-lines" viewBox="0 0 900 360" aria-hidden="true">
      <path d="M-40 260 C 180 40, 310 410, 520 150 S 760 12, 940 190" />
      <path d="M-80 310 C 180 115, 360 420, 560 210 S 790 80, 980 245" />
    </svg>
    <p class="kicker">Build the future</p>
    <h2>Ready to build the future?</h2>
    <a class="gold-btn" href="mailto:hello@nexora.example">Start Today →</a>
  </section>
</main>

{#snippet Dashboard(dark: boolean = false, compact: boolean = false)}
  <div class:compact class="dashboard" class:dark>
    <div class="dash-top"><b>Overview</b><span>Live</span></div>
    <div class="dash-grid">
      <div class="metric-card"><small>Revenue</small><strong>$284.9k</strong><i>+18.2%</i></div>
      <div class="metric-card"><small>Success Rate</small><strong>98.7%</strong><i>+4.8%</i></div>
    </div>
    <div class="chart-panel">
      <svg viewBox="0 0 420 160">
        <path class="gridline" d="M0 122H420M0 82H420M0 42H420" />
        <path class="chart-line shadow" d="M8 126 C55 96 82 118 128 76 S205 34 248 58 S325 115 410 26" />
        <path class="chart-line" d="M8 126 C55 96 82 118 128 76 S205 34 248 58 S325 115 410 26" />
      </svg>
    </div>
    <div class="activity">
      <div><span></span><p>Payment settled</p><b>$28k</b></div>
      <div><span></span><p>Invoice approved</p><b>AI</b></div>
      <div><span></span><p>Risk check passed</p><b>99%</b></div>
    </div>
    <div class="bars">{#each Array(10) as _, i}<i style={`--i:${i};--h:${35 + ((i * 17) % 58)}%`}></i>{/each}</div>
  </div>
{/snippet}
