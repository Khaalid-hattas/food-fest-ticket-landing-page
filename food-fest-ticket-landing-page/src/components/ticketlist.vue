<template>
  <div class="ticket-section">
    <div class="controls">
      <label for="sortTickets">Sort By Price: </label>
      <select id="sortTickets" v-model="sortBy">
        <option value="default">Default Arrangement</option>
        <option value="low-high">Low to High</option>
        <option value="high-low">High to Low</option>
      </select>
      
      <span class="fav-counter">Saved Tiers: {{ favourites.length }}</span>
    </div>

    <div class="tickets-grid">
      <TicketCard 
        v-for="ticket in sortedTickets" 
        :key="ticket.id" 
        :ticket="ticket"
        :isFavourited="favourites.includes(ticket.id)"
        @toggle-favourite="handleFavouriteToggle"
      >
        <template #action-button>
          <button class="btn-primary" @click="notifyMe(ticket.name)">
            {{ ticket.isFeatured ? 'Secure Priority Access' : 'Notify Me' }}
          </button>
        </template>
      </TicketCard>
    </div>
  </div>
</template>

<script setup>
import { ref, computed } from 'vue';
import TicketCard from './TicketCard.vue';

// Local Mock Data Source
const tickets = ref([
  {
    id: 1,
    name: 'Bronze Tier',
    price: 150,
    description: 'Perfect for casual foodies looking to explore the general marketplace vibe.',
    benefits: ['General Access entry pass', 'Access to 50+ street food vendors', 'Standard lawn seating for live music performance'],
    isFeatured: false
  },
  {
    id: 2,
    name: 'Gold Tier',
    price: 450,
    description: 'The definitive VIP luxury package for deep culinary appreciation.',
    benefits: ['Fast-track VIP express entry routing', 'Exclusive access to VIP Private Lounge & premium bars', 'Complimentary masterclass with guest chefs', '5 Free tasting coupons'],
    isFeatured: true
  },
  {
    id: 3,
    name: 'Silver Tier',
    price: 275,
    description: 'An elevated approach for enthusiasts wanting extra comfort and early access.',
    benefits: ['30-minute early entry access window', 'Access to priority shaded seating decks', '1 Complimentary craft beverage selection voucher'],
    isFeatured: false
  }
]);

// Interactive State arrays
const favourites = ref([]);
const sortBy = ref('default');

// Computed Property to dynamically sort data dynamically without losing index state
const sortedTickets = computed(() => {
  let list = [...tickets.value];
  if (sortBy.value === 'low-high') {
    return list.sort((a, b) => a.price - b.price);
  } else if (sortBy.value === 'high-low') {
    return list.sort((a, b) => b.price - a.price);
  }
  return list; 
});

// Logic Operations
const handleFavouriteToggle = (id) => {
  if (favourites.value.includes(id)) {
    favourites.value = favourites.value.filter(favId => favId !== id);
  } else {
    favourites.value.push(id);
  }
};

const notifyMe = (tierName) => {
  alert(`Awesome! You've been added to our notification queue for the ${tierName}. Stay tuned!`);
};
</script>

<style scoped>
.ticket-section {
  margin-top: 2rem;
}

.controls {
  display: flex;
  justify-content: space-between;
  align-items: center;
  margin-bottom: 2.5rem;
  background: white;
  padding: 1rem 1.5rem;
  border-radius: 12px;
  box-shadow: 0 4px 15px rgba(0,0,0,0.02);
}

.controls select {
  padding: 0.5rem 1rem;
  border-radius: 6px;
  border: 1px solid var(--gray);
  background: white;
  font-size: 0.9rem;
}

.fav-counter {
  font-weight: 600;
  background: rgba(255, 107, 107, 0.1);
  color: var(--primary);
  padding: 0.4rem 1rem;
  border-radius: 30px;
}

/* Flexbox/Grid breakpoint switching for fully responsive layouts */
.tickets-grid {
  display: grid;
  grid-template-columns: 1fr;
  gap: 2.5rem;
  align-items: stretch;
}

@media (min-width: 768px) {
  .tickets-grid {
    grid-template-columns: repeat(2, 1fr);
  }
}

@media (min-width: 1024px) {
  .tickets-grid {
    grid-template-columns: repeat(3, 1fr);
  }
}
</style>