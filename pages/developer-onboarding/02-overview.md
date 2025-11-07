## 📋 Tutorial Overview

This tutorial will teach you how to build features in the Rucio WebUI using Clean Architecture principles. You'll learn to:

1. **Create Secondary Output Port & Gateway** (with tests)
2. **Create a Feature** (UseCase + Controller + Presenter)
3. **Call Feature from a Page** (API Route + React Component)
4. **Design the Page** (UI Components)

**Example:** We'll build a `list-subscriptions` feature that fetches subscriptions from the Rucio server.

---
## Follow Along

1. **Clone the Tutorial Repo**:  
   ```bash
   gh repo clone rucio/webui
   cd webui
   ```
2. **Switch to Tutorial branch**:  
   ```bash
   git checkout webui-tutorial
   ```
3. **Set up environment variables**:  
   ```bash
   cp .env.development.local.template .env.development.local
   # update the rucio server URLs: RUCIO_HOST, RUCIO_AUTH_HOST
   ```
4. **Install dependencies and start the development server**:  
   ```bash
   npm install
   npm run dev
   ```
