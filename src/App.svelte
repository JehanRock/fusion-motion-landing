<script lang="ts">
  import { onMount } from 'svelte'

  let progress = 0
  let active = 0

  const sections = [
    { label: 'Signal', metric: '00.8s', copy: 'From brief to polished motion system without the agency drag.' },
    { label: 'Flow', metric: '14+', copy: 'Reusable animated sections, cards, reveals, and conversion patterns.' },
    { label: 'Launch', metric: '1 page', copy: 'A landing page built to feel alive before the product is even shipped.' }
  ]

  const features = [
    'Scroll-synced story rhythm',
    'Glass surfaces with depth',
    'Magnetic conversion blocks',
    'Responsive motion primitives'
  ]

  onMount(() => {
    const update = () => {
      const max = document.documentElement.scrollHeight - window.innerHeight
      progress = max > 0 ? Math.min(1, window.scrollY / max) : 0
      active = Math.min(2, Math.floor(progress * 3.2))
    }
    update()
    window.addEventListener('scroll', update, { passive: true })
    return () => window.removeEventListener('scroll', update)
  })
</script>

<svelte:head>
  <title>Velora Motion — premium Svelte landing page</title>
  <meta name="description" content="A clean, cinematic motion landing page built with Svelte." />
</svelte:head>

<div class="progress" style={`transform: scaleX(${progress})`}></div>

<main>
  <section class="hero section-panel">
    <nav class="nav" aria-label="Main navigation">
      <a class="brand" href="#top" aria-label="Velora home">
        <span class="brand-mark"></span>
        <span>Velora</span>
      </a>
      <div class="nav-links">
        <a href="#craft">Craft</a>
        <a href="#motion">Motion</a>
        <a href="#launch">Launch</a>
      </div>
      <a class="nav-cta" href="#launch">Start</a>
    </nav>

    <div class="hero-grid" id="top">
      <div class="hero-copy reveal">
        <p class="eyebrow"><span></span> Motion sites for products that need to feel expensive</p>
        <h1>Landing pages with cinematic rhythm and conversion-grade clarity.</h1>
        <p class="lede">A one-page Svelte experience with soft depth, scroll choreography, and dynamic sections that make a young brand feel inevitable.</p>
        <div class="actions">
          <a class="primary" href="#launch">Build the page</a>
          <a class="secondary" href="#motion">Watch the flow</a>
        </div>
      </div>

      <div class="orb-stage" aria-label="Animated product visual">
        <div class="halo halo-one"></div>
        <div class="halo halo-two"></div>
        <div class="device-card">
          <div class="device-top"><span></span><span></span><span></span></div>
          <div class="kinetic-word">motion</div>
          <div class="wave-bars">
            {#each Array(18) as _, i}
              <i style={`--i:${i}`}></i>
            {/each}
          </div>
          <div class="mini-stack">
            <b>+42%</b>
            <small>scroll depth</small>
          </div>
        </div>
      </div>
    </div>
  </section>

  <section class="ticker" aria-label="Capabilities">
    <div>
      <span>Scroll design</span><span>Interaction systems</span><span>Launch pages</span><span>Svelte motion</span><span>Premium UI</span>
    </div>
  </section>

  <section class="story section-panel" id="craft">
    <div class="section-heading reveal">
      <p class="eyebrow"><span></span> The craft layer</p>
      <h2>Every block earns its place.</h2>
    </div>
    <div class="cards">
      {#each sections as item, i}
        <article class:active={active === i} class="story-card reveal">
          <p>{item.label}</p>
          <h3>{item.metric}</h3>
          <span>{item.copy}</span>
        </article>
      {/each}
    </div>
  </section>

  <section class="motion section-panel" id="motion">
    <div class="motion-panel reveal">
      <div class="motion-copy">
        <p class="eyebrow"><span></span> Dynamic components</p>
        <h2>Animations that guide attention, not distract from it.</h2>
        <p>Soft reveals, parallax layers, floating glass, and responsive motion tokens give the page a high-end product feel while staying fast and readable.</p>
      </div>
      <div class="feature-grid">
        {#each features as feature, i}
          <div class="feature" style={`--d:${i * 90}ms`}>
            <span>{`0${i + 1}`}</span>
            <b>{feature}</b>
          </div>
        {/each}
      </div>
    </div>
  </section>

  <section class="launch section-panel" id="launch">
    <div class="launch-card reveal">
      <p class="eyebrow"><span></span> Ship the feeling</p>
      <h2>Make the first impression feel like a funded product.</h2>
      <p>Clean structure, seductive transitions, and a memorable visual system — ready to extend into a real brand site.</p>
      <a class="primary" href="mailto:hello@example.com">Start a motion build</a>
    </div>
  </section>
</main>
