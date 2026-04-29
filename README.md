# OfficeTable

OfficeTable is an AI-powered group meal orchestration system for workplaces that automates the entire process of ordering food for teams. Instead of manual coordination across chats and fragmented orders, it collects employee preferences, intelligently selects optimal restaurants, builds a unified order, and manages delivery tracking in one flow.

It transforms a chaotic, multi-step human process into a seamless, agent-driven workflow that saves time, reduces errors, and improves team meal experiences.

---

## Tech stack & architecture overview

### Frontend
- React (Vite or Next.js)
- TailwindCSS
- Admin dashboard for office managers
- Employee preference onboarding interface

### Backend
- Node.js (Express or Hono)
- PostgreSQL (user preferences, order history, team data)
- Redis (caching + session + short-lived orchestration states)

### AI / Agent Layer
- LLM (local or API-based) for:
  - constraint aggregation (dietary, budget, preferences)
  - restaurant selection reasoning
  - menu optimization across group

### MCP Integration (Core Flow)

OfficeTable uses Swiggy MCP as the execution layer:

1. **Preference Aggregation**
   - Collect dietary restrictions, cuisine preferences, budget per employee

2. **Restaurant Discovery (Food MCP)**
   - Query restaurants using composite constraints:
     - cuisine overlap
     - dietary compatibility
     - rating / delivery time

3. **Menu Resolution**
   - Map each user’s preferences to available menu items
   - Ensure maximum coverage from a single restaurant (optimization step)

4. **Cart Orchestration**
   - Build a unified cart with item mapping per user
   - Handle quantities, substitutions, and constraints

5. **Order Execution**
   - Place order via MCP using a central company account

6. **Tracking & Status Aggregation**
   - Poll order status
   - Aggregate delivery updates into a single admin dashboard

### Integrations
- Slack / WhatsApp (notifications for admins)
- Optional calendar integration (scheduled recurring orders)

---

## High-level Architecture

Client (Admin + Employees)
        ↓
Backend API (Node.js)
        ↓
Agent Layer (LLM + Orchestration Logic)
        ↓
Swiggy MCP (Food APIs)
        ↓
Order Execution + Tracking