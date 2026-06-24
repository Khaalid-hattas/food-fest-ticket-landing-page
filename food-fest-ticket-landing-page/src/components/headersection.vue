<template>
  <header class="hero-header">
    <div class="hero-overlay">
      <span class="date-tag">🗓️ October 24-26, 2026 • Green Point Park</span>
      <h1>Cape Town Food Fest</h1>
      <p class="subtitle">
        Join South Africa's finest culinary minds, local street food icons, and indie musicians 
        for an unforgettable weekend. Explore ticket options below and save your favorites.
      </p>
    </div>
  </header>
</template>

<style scoped>
.hero-header {
  background: linear-gradient(135deg, #2d3436 0%, #000000 100%);
  color: white;
  text-align: center;
  padding: 5rem 1.5rem;
  border-radius: 24px;
  margin-bottom: 3rem;
}

.date-tag {
  color: var(--secondary);
  font-weight: 600;
  text-transform: uppercase;
  letter-spacing: 1px;
  font-size: 0.9rem;
  display: inline-block;
  margin-bottom: 1rem;
}

h1 {
  font-size: 3rem;
  font-weight: 800;
  margin-bottom: 1rem;
  letter-spacing: -1px;
}

.subtitle {
  max-width: 650px;
  margin: 0 auto;
  color: #b2bec3;
  font-size: 1.1rem;
}

@media(max-width: 480px) {
  h1 { font-size: 2.2rem; }
  .hero-header { padding: 3rem 1rem; }
}
</style>