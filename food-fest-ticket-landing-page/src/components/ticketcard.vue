<template>
  <div 
    class="ticket-card" 
    :class="{ 'featured': ticket.isFeatured, 'is-favourited': isFavourited }"
  >
    <div v-if="ticket.isFeatured" class="badge">Most Popular</div>

    <div class="card-header">
      <h3>{{ ticket.name }}</h3>
      <button 
        @click="$emit('toggle-favourite', ticket.id)" 
        class="fav-btn"
        :aria-label="isFavourited ? 'Remove from favourites' : 'Add to favourites'"
      >
        <span class="heart-icon">{{ isFavourited ? '❤️' : '🤍' }}</span>
      </button>
    </div>

    <div class="price-container">
      <span class="currency">R</span>
      <span class="price">{{ ticket.price }}</span>
      <span class="perks-text">/ per person</span>
    </div>

    <p class="description">{{ ticket.description }}</p>

    <ul class="benefits-list">
      <li v-for="(benefit, index) in ticket.benefits" :key="index">
        <span class="check-icon">✓</span> {{ benefit }}
      </li>
    </ul>

    <div class="card-actions">
      <slot name="action-button">
        <button class="btn-primary" @click="fallbackAction">Select Tier</button>
      </slot>
    </div>
  </div>
</template>

<script setup>
defineProps({
  ticket: {
    type: Object,
    required: true
  },
  isFavourited: {
    type: Boolean,
    default: false
  }
});

defineEmits(['toggle-favourite', 'select-tier']);

const fallbackAction = () => {
  alert("Ticketing system coming soon! Stand by for pre-sales.");
};
</script>

<style scoped>
.ticket-card {
  background: white;
  border-radius: 16px;
  padding: 2.5rem 2rem;
  box-shadow: 0 10px 30px rgba(0,0,0,0.05);
  position: relative;
  display: flex;
  flex-direction: column;
  transition: transform 0.3s ease, box-shadow 0.3s ease;
  border: 2px solid transparent;
}

.ticket-card:hover {
  transform: translateY(-5px);
  box-shadow: 0 15px 35px rgba(0,0,0,0.1);
}

.ticket-card.featured {
  border-color: var(--primary);
  transform: scale(1.03);
}

.ticket-card.featured:hover {
  transform: translateY(-5px) scale(1.03);
}

.badge {
  position: absolute;
  top: -15px;
  right: 25px;
  background: var(--primary);
  color: white;
  padding: 0.3rem 1rem;
  border-radius: 20px;
  font-size: 0.8rem;
  font-weight: bold;
  text-transform: uppercase;
  letter-spacing: 1px;
}

.card-header {
  display: flex;
  justify-content: space-between;
  align-items: center;
  margin-bottom: 1rem;
}

.card-header h3 {
  font-size: 1.6rem;
  color: var(--dark);
}

.fav-btn {
  background: none;
  border: none;
  font-size: 1.5rem;
  cursor: pointer;
  transition: transform 0.2s ease;
}

.fav-btn:hover {
  transform: scale(1.2);
}

.price-container {
  margin-bottom: 1.5rem;
}

.currency {
  font-size: 1.5rem;
  font-weight: bold;
  vertical-align: super;
  color: var(--primary);
}

.price {
  font-size: 3rem;
  font-weight: 800;
  color: var(--dark);
}

.description {
  color: var(--gray);
  margin-bottom: 2rem;
  min-height: 50px;
}

.benefits-list {
  list-style: none;
  margin-bottom: 2.5rem;
  flex-grow: 1;
}

.benefits-list li {
  margin-bottom: 0.8rem;
  display: flex;
  align-items: center;
  color: #4f5d75;
}

.check-icon {
  color: var(--success);
  margin-right: 10px;
  font-weight: bold;
}

.card-actions {
  margin-top: auto;
}

/* Styled Fallback/Default Slot Button */
:deep(.btn-primary) {
  width: 100%;
  background: var(--dark);
  color: white;
  border: none;
  padding: 1rem;
  border-radius: 8px;
  font-size: 1rem;
  font-weight: 600;
  cursor: pointer;
  transition: background 0.2s ease;
}

.featured :deep(.btn-primary) {
  background: var(--primary);
}

:deep(.btn-primary:hover) {
  opacity: 0.9;
}
</style>