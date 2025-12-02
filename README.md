# AGM Store Builder

> Simple, fast, no-stress mini website and e-commerce builder for Nigerian entrepreneurs

![License](https://img.shields.io/badge/license-MIT-blue.svg)
![Node](https://img.shields.io/badge/node-%3E%3D18.0.0-brightgreen.svg)
![Next.js](https://img.shields.io/badge/next.js-14.0-black.svg)

## 🎯 Overview

AGM Store Builder enables Nigerian SMEs, social sellers, and entrepreneurs to create professional online stores in minutes—without coding, without Paystack KYC stress, and with instant payouts to their bank accounts.

**Key Features:**
- 🚀 Create store in under 5 minutes
- 💰 Instant payouts (no waiting period)
- 🏪 Auto-generated subdomain (username.agmshop.com)
- 📱 Mobile-first design
- 💳 No payment gateway onboarding required
- 🎨 Customizable templates

---

## 📋 Table of Contents

- [Tech Stack](#tech-stack)
- [Architecture](#architecture)
- [Getting Started](#getting-started)
- [Environment Variables](#environment-variables)
- [Database Schema](#database-schema)
- [Payment Integration](#payment-integration)
- [Subdomain Routing](#subdomain-routing)
- [API Documentation](#api-documentation)
- [Deployment](#deployment)
- [Contributing](#contributing)

---

## 🛠 Tech Stack

### Frontend
- **Framework:** Next.js 14 (App Router)
- **Styling:** Tailwind CSS
- **State Management:** Zustand / React Context
- **Forms:** React Hook Form + Zod
- **UI Components:** shadcn/ui
- **Icons:** Lucide React

### Backend
- **Runtime:** Node.js 18+
- **Framework:** Express.js / NestJS
- **Database:** PostgreSQL 15
- **ORM:** Prisma
- **Cache:** Redis
- **Queue:** BullMQ
- **File Storage:** AWS S3 / Cloudinary

### Payment
- **Primary:** Monnify Virtual Accounts
- **Backup:** Nomba
- **Verification:** Paystack Verify API

### Infrastructure
- **Frontend Hosting:** Vercel
- **Backend Hosting:** Railway / Render
- **DNS:** Cloudflare
- **Monitoring:** Sentry
- **Analytics:** PostHog / Mixpanel

---

## 🏗 Architecture

### System Overview

```mermaid
graph TB
    %% Users Layer
    subgraph USERS["👥 USERS"]
        Sellers["🛍️ Sellers<br/>(Store Owners)"]
        Buyers["🛒 Buyers<br/>(Customers)"]
    end

    %% DNS Layer
    subgraph DNS["🌐 CLOUDFLARE DNS"]
        Wildcard["*.agmshop.com<br/>Wildcard Routing"]
        MainDomain["agmshop.com<br/>Main Site"]
    end

    %% Frontend Layer
    subgraph FRONTEND["⚛️ NEXT.JS FRONTEND<br/>(Vercel)"]
        SSR["Server-Side Rendering<br/>• Store Pages (SEO)<br/>• Product Listings<br/>• Dynamic Routes"]
        ClientSide["Client-Side SPA<br/>• Dashboard<br/>• Admin Panel<br/>• Real-time Updates"]
        SubdomainRouter["Subdomain Router<br/>username.agmshop.com"]
    end

    %% Backend Layer
    subgraph BACKEND["🔧 EXPRESS BACKEND<br/>(Railway/Render)"]
        direction TB
        
        subgraph Services["Microservices Architecture"]
            AuthService["🔐 Auth Service<br/>• Login/Signup<br/>• JWT/OTP<br/>• Sessions"]
            StoreService["🏪 Store Service<br/>• CRUD Operations<br/>• Subdomain Setup<br/>• Customization"]
            ProductService["📦 Product Service<br/>• Inventory<br/>• Variations<br/>• Images"]
            OrderService["📋 Order Service<br/>• Cart → Checkout<br/>• Status Tracking<br/>• Fulfillment"]
            PaymentService["💳 Payment Service<br/>• Virtual Accounts<br/>• Webhooks<br/>• Payouts"]
            AnalyticsService["📊 Analytics Service<br/>• Revenue Stats<br/>• Customer Insights<br/>• Reports"]
        end
    end

    %% Database Layer
    subgraph DATABASE["💾 DATA LAYER"]
        direction LR
        PostgreSQL["🐘 POSTGRESQL<br/>• Users<br/>• Stores<br/>• Products<br/>• Orders<br/>• Transactions<br/>• Bank Accounts"]
        Redis["⚡ REDIS<br/>• Sessions<br/>• Rate Limiting<br/>• Job Queue<br/>• Cache"]
    end

    %% External Services Layer
    subgraph EXTERNAL["🔌 EXTERNAL SERVICES"]
        direction TB
        Monnify["💰 Monnify<br/>Virtual Accounts<br/>Payment Processing"]
        Paystack["🏦 Paystack<br/>Bank Verification<br/>Account Lookup"]
        AWS["☁️ AWS S3<br/>Image Storage<br/>File Uploads"]
        Termii["📱 Termii SMS<br/>OTP Delivery<br/>Notifications"]
        Resend["📧 Resend Email<br/>Transactional Emails<br/>Receipts"]
    end

    %% Background Jobs Layer
    subgraph JOBS["⚙️ BACKGROUND JOBS<br/>(BullMQ)"]
        PayoutQueue["💸 Payout Queue<br/>Instant Transfers"]
        NotificationQueue["🔔 Notification Queue<br/>SMS/Email Alerts"]
        AnalyticsQueue["📈 Analytics Queue<br/>Data Processing"]
    end

    %% Main Flow Connections
    Sellers --> DNS
    Buyers --> DNS
    DNS --> FRONTEND
    FRONTEND --> BACKEND
    BACKEND --> DATABASE
    BACKEND --> EXTERNAL
    BACKEND --> JOBS
    
    %% Detailed Connections
    SubdomainRouter -.->|Dynamic Routing| StoreService
    SSR -.->|Fetch Data| ProductService
    ClientSide -.->|API Calls| Services
    
    Services --> PostgreSQL
    Services --> Redis
    
    PaymentService <-->|API Calls| Monnify
    PaymentService <-->|Verification| Paystack
    ProductService -->|Upload| AWS
    AuthService -->|Send OTP| Termii
    OrderService -->|Receipts| Resend
    
    PaymentService -->|Queue Jobs| PayoutQueue
    OrderService -->|Queue Jobs| NotificationQueue
    AnalyticsService -->|Queue Jobs| AnalyticsQueue

    %% Styling
    classDef userClass fill:#e1f5ff,stroke:#0288d1,stroke-width:2px,color:#000
    classDef dnsClass fill:#fff3e0,stroke:#f57c00,stroke-width:2px,color:#000
    classDef frontendClass fill:#e8f5e9,stroke:#388e3c,stroke-width:2px,color:#000
    classDef backendClass fill:#f3e5f5,stroke:#7b1fa2,stroke-width:2px,color:#000
    classDef dataClass fill:#fce4ec,stroke:#c2185b,stroke-width:2px,color:#000
    classDef externalClass fill:#fff9c4,stroke:#f9a825,stroke-width:2px,color:#000
    classDef jobClass fill:#e0f2f1,stroke:#00796b,stroke-width:2px,color:#000

    class USERS,Sellers,Buyers userClass
    class DNS,Wildcard,MainDomain dnsClass
    class FRONTEND,SSR,ClientSide,SubdomainRouter frontendClass
    class BACKEND,Services,AuthService,StoreService,ProductService,OrderService,PaymentService,AnalyticsService backendClass
    class DATABASE,PostgreSQL,Redis dataClass
    class EXTERNAL,Monnify,Paystack,AWS,Termii,Resend externalClass
    class JOBS,PayoutQueue,NotificationQueue,AnalyticsQueue jobClass
```

### Complete E-Commerce Flow

```mermaid
sequenceDiagram
    participant Customer
    participant Store as Store Frontend<br/>(username.agmshop.com)
    participant API as Backend API
    participant DB as PostgreSQL
    participant Monnify
    participant Bank as Seller Bank Account

    Note over Customer,Bank: FULL E-COMMERCE FLOW

    rect rgb(230, 245, 255)
        Note right of Customer: 1. BROWSING PHASE
        Customer->>Store: Visit store page
        Store->>API: Fetch store + products
        API->>DB: Query store data
        DB-->>API: Return data
        API-->>Store: Store & products
        Store-->>Customer: Display store
    end

    rect rgb(255, 243, 224)
        Note right of Customer: 2. CHECKOUT PHASE
        Customer->>Store: Add to cart & checkout
        Store->>API: Create order
        API->>DB: Save order (status: pending)
        DB-->>API: Order created
        API->>Monnify: Get virtual account
        Monnify-->>API: Virtual account details
        API-->>Store: Payment instructions
        Store-->>Customer: Show bank details
    end

    rect rgb(232, 245, 233)
        Note right of Customer: 3. PAYMENT PHASE
        Customer->>Bank: Make bank transfer
        Bank->>Monnify: Credit virtual account
        Monnify->>API: Webhook notification
        API->>Monnify: Verify payment
        Monnify-->>API: Payment confirmed
    end

    rect rgb(255, 235, 238)
        Note right of Customer: 4. SETTLEMENT PHASE
        API->>DB: Update order (paid)
        API->>API: Calculate AGM fee (1-2%)
        API->>Monnify: Initiate payout
        Monnify->>Bank: Transfer to seller
        Bank-->>Monnify: Transfer successful
        Monnify-->>API: Payout confirmed
    end

    rect rgb(243, 229, 245)
        Note right of Customer: 5. NOTIFICATION PHASE
        API->>Customer: Send SMS (order confirmed)
        API->>Store: Send email/SMS (payment received)
        API->>DB: Update transaction status
    end
```

### Database Schema

```mermaid
erDiagram
    USERS ||--o{ STORES : owns
    USERS ||--o{ BANK_ACCOUNTS : has
    STORES ||--o{ PRODUCTS : contains
    STORES ||--o{ ORDERS : receives
    STORES ||--|| VIRTUAL_ACCOUNTS : has
    ORDERS ||--o{ TRANSACTIONS : generates
    ORDERS }o--o{ PRODUCTS : includes
    TRANSACTIONS }o--|| BANK_ACCOUNTS : pays_to

    USERS {
        uuid id PK
        string email "unique"
        string phone "unique"
        string password_hash
        string full_name
        boolean email_verified
        boolean phone_verified
        timestamp created_at
    }

    STORES {
        uuid id PK
        uuid user_id FK
        string username "unique"
        string display_name
        text description
        string logo_url
        string template_id
        json custom_colors
        boolean is_active
        timestamp created_at
    }

    PRODUCTS {
        uuid id PK
        uuid store_id FK
        string name
        text description
        decimal price
        json images
        json variations
        integer stock_quantity
        boolean is_active
    }

    ORDERS {
        uuid id PK
        uuid store_id FK
        string order_number "unique"
        string customer_name
        string customer_phone
        json items
        decimal subtotal
        decimal agm_fee
        decimal total_amount
        string status
        string payment_status
        string payment_reference "unique"
    }

    TRANSACTIONS {
        uuid id PK
        uuid order_id FK
        decimal amount
        decimal agm_fee
        decimal net_amount
        string type
        string status
        string payout_reference
    }

    BANK_ACCOUNTS {
        uuid id PK
        uuid user_id FK
        string account_number
        string account_name
        string bank_name
        boolean is_verified
        boolean is_default
    }

    VIRTUAL_ACCOUNTS {
        uuid id PK
        uuid store_id FK "unique"
        string account_number
        string account_name
        string bank_name
        string provider
        string provider_reference
        boolean is_active
    }
```

---

## 🚀 Getting Started

### Prerequisites

```bash
node >= 18.0.0
npm >= 9.0.0
postgresql >= 15.0
redis >= 7.0
```

### Installation

#### 1. Clone the repository
```bash
git clone https://github.com/thetruesammyjay/agm-store-builder.git
cd agm-store-builder
```

#### 2. Install dependencies

**Frontend:**
```bash
cd frontend
npm install
```

**Backend:**
```bash
cd backend
npm install
```

#### 3. Set up environment variables

Copy `.env.example` to `.env` in both directories and fill in your values.

```bash
cp frontend/.env.example frontend/.env
cp backend/.env.example backend/.env
```

#### 4. Set up database

```bash
cd backend
npx prisma migrate dev
npx prisma db seed
```

#### 5. Start development servers

**Backend:**
```bash
cd backend
npm run dev
# Runs on http://localhost:4000
```

**Frontend:**
```bash
cd frontend
npm run dev
# Runs on http://localhost:3000
```

---

## 🔐 Environment Variables

### Frontend (.env)

```env
# App
NEXT_PUBLIC_APP_URL=http://localhost:3000
NEXT_PUBLIC_API_URL=http://localhost:4000/api

# Analytics (Optional)
NEXT_PUBLIC_POSTHOG_KEY=your_posthog_key
NEXT_PUBLIC_SENTRY_DSN=your_sentry_dsn
```

### Backend (.env)

```env
# Server
NODE_ENV=development
PORT=4000
API_URL=http://localhost:4000

# Database
DATABASE_URL=postgresql://user:password@localhost:5432/agm_store_builder

# Redis
REDIS_URL=redis://localhost:6379

# JWT
JWT_SECRET=your_super_secret_jwt_key_change_this
JWT_EXPIRES_IN=7d

# Monnify
MONNIFY_API_KEY=your_monnify_api_key
MONNIFY_SECRET_KEY=your_monnify_secret_key
MONNIFY_CONTRACT_CODE=your_contract_code
MONNIFY_BASE_URL=https://sandbox.monnify.com

# Paystack (for bank verification)
PAYSTACK_SECRET_KEY=your_paystack_secret_key

# AWS S3 / Cloudinary
AWS_ACCESS_KEY_ID=your_aws_key
AWS_SECRET_ACCESS_KEY=your_aws_secret
AWS_REGION=us-east-1
AWS_BUCKET_NAME=agm-store-uploads

# Email (Resend / SendGrid)
RESEND_API_KEY=your_resend_key
EMAIL_FROM=noreply@agmshop.com

# SMS (Termii / SMS.to)
TERMII_API_KEY=your_termii_key
TERMII_SENDER_ID=AGM_STORE

# Rate Limiting
RATE_LIMIT_WINDOW_MS=900000
RATE_LIMIT_MAX_REQUESTS=100

# Domain
BASE_DOMAIN=agmshop.com
WILDCARD_DOMAIN=*.agmshop.com
```

---

## 💾 Database Schema

### Core Tables

```sql
-- Users (Sellers)
users
  - id (uuid, PK)
  - email (unique)
  - phone (unique)
  - password_hash
  - full_name
  - email_verified
  - phone_verified
  - created_at
  - updated_at

-- Stores
stores
  - id (uuid, PK)
  - user_id (FK → users)
  - username (unique) -- for subdomain
  - display_name
  - description
  - logo_url
  - template_id
  - custom_colors (json)
  - custom_fonts (json)
  - is_active
  - created_at
  - updated_at

-- Products
products
  - id (uuid, PK)
  - store_id (FK → stores)
  - name
  - description
  - price
  - compare_at_price
  - images (json array)
  - variations (json) -- size, color, etc.
  - stock_quantity
  - is_active
  - created_at
  - updated_at

-- Orders
orders
  - id (uuid, PK)
  - store_id (FK → stores)
  - order_number (unique)
  - customer_name
  - customer_phone
  - customer_email
  - customer_address (json)
  - items (json array)
  - subtotal
  - agm_fee
  - total_amount
  - status (pending, confirmed, fulfilled, cancelled)
  - payment_status (pending, paid, failed, refunded)
  - payment_reference
  - created_at
  - updated_at

-- Transactions (Payouts)
transactions
  - id (uuid, PK)
  - store_id (FK → stores)
  - order_id (FK → orders)
  - amount
  - agm_fee
  - net_amount
  - type (payout, refund)
  - status (pending, completed, failed)
  - bank_account_id (FK → bank_accounts)
  - payout_reference
  - created_at
  - updated_at

-- Bank Accounts
bank_accounts
  - id (uuid, PK)
  - user_id (FK → users)
  - account_number
  - account_name
  - bank_name
  - bank_code
  - is_verified
  - is_default
  - created_at
  - updated_at

-- Virtual Accounts (Monnify)
virtual_accounts
  - id (uuid, PK)
  - store_id (FK → stores)
  - account_number
  - account_name
  - bank_name
  - provider (monnify, nomba)
  - provider_reference
  - is_active
  - created_at
  - updated_at
```

---

## 💳 Payment Integration

### Flow Overview

```
1. Customer initiates checkout
2. Backend creates order (status: pending)
3. Frontend displays Monnify virtual account details
4. Customer makes bank transfer
5. Monnify sends webhook to backend
6. Backend verifies payment with Monnify API
7. Order status → confirmed
8. Auto-split: AGM fee (1-2%) + Seller payout
9. Initiate instant payout to seller's bank
10. Send SMS/email confirmations
```

### Webhook Handler (Example)

```javascript
// backend/src/controllers/webhooks/monnify.webhook.js

async handlePaymentNotification(req, res) {
  const { transactionReference, paymentReference, amountPaid, paidOn } = req.body;
  
  // 1. Verify webhook signature
  const isValid = verifyMonnifyWebhook(req.body, req.headers);
  if (!isValid) return res.status(400).json({ error: 'Invalid signature' });
  
  // 2. Find order by payment reference
  const order = await Order.findOne({ payment_reference: paymentReference });
  if (!order) return res.status(404).json({ error: 'Order not found' });
  
  // 3. Update order status
  order.payment_status = 'paid';
  order.status = 'confirmed';
  await order.save();
  
  // 4. Calculate splits
  const agmFee = amountPaid * 0.01; // 1%
  const sellerAmount = amountPaid - agmFee;
  
  // 5. Create transaction record
  const transaction = await Transaction.create({
    order_id: order.id,
    store_id: order.store_id,
    amount: amountPaid,
    agm_fee: agmFee,
    net_amount: sellerAmount,
    status: 'pending'
  });
  
  // 6. Queue payout job
  await payoutQueue.add('instant-payout', {
    transaction_id: transaction.id,
    amount: sellerAmount,
    bank_account_id: order.store.default_bank_account_id
  });
  
  // 7. Send notifications
  await notificationQueue.add('order-confirmed', { order_id: order.id });
  
  res.status(200).json({ success: true });
}
```

---

## 🌐 Subdomain Routing

### DNS Configuration (Cloudflare)

```
Type: A
Name: @
Content: <your-server-ip>
Proxy: Yes

Type: CNAME
Name: *
Content: agmshop.com
Proxy: Yes
```

### Next.js Dynamic Routing

```javascript
// frontend/middleware.js
import { NextResponse } from 'next/server';

export function middleware(request) {
  const hostname = request.headers.get('host');
  const url = request.nextUrl;
  
  // Check if subdomain exists
  const subdomain = hostname.split('.')[0];
  
  if (subdomain && subdomain !== 'www' && subdomain !== 'agmshop') {
    // Rewrite to store page
    url.pathname = `/store/${subdomain}${url.pathname}`;
    return NextResponse.rewrite(url);
  }
  
  return NextResponse.next();
}
```

```javascript
// frontend/app/store/[username]/page.js
export async function generateMetadata({ params }) {
  const store = await fetchStore(params.username);
  
  return {
    title: `${store.display_name} - AGM Store`,
    description: store.description,
  };
}

export default async function StorePage({ params }) {
  const store = await fetchStore(params.username);
  const products = await fetchProducts(params.username);
  
  return (
    <StoreLayout store={store}>
      <ProductGrid products={products} />
    </StoreLayout>
  );
}
```

---

## 📡 API Documentation

### Base URL
```
Development: http://localhost:4000/api
Production: https://api.agmshop.com
```

### Authentication

All authenticated endpoints require JWT token in header:
```
Authorization: Bearer <token>
```

### Key Endpoints

#### Auth
```
POST   /auth/signup           - Create new user account
POST   /auth/login            - Login user
POST   /auth/verify-email     - Verify email with OTP
POST   /auth/verify-phone     - Verify phone with OTP
POST   /auth/forgot-password  - Request password reset
POST   /auth/reset-password   - Reset password with token
```

#### Stores
```
POST   /stores                - Create new store
GET    /stores/:username      - Get store by username (public)
PUT    /stores/:id            - Update store
DELETE /stores/:id            - Delete store
GET    /stores/check/:username - Check username availability
```

#### Products
```
POST   /stores/:id/products              - Create product
GET    /stores/:username/products        - List products (public)
GET    /stores/:username/products/:id    - Get product (public)
PUT    /products/:id                     - Update product
DELETE /products/:id                     - Delete product
POST   /products/:id/upload-image        - Upload product image
```

#### Orders
```
POST   /stores/:username/orders          - Create order (public)
GET    /orders/:id                       - Get order details
GET    /dashboard/orders                 - List user's orders
PATCH  /orders/:id/status                - Update order status
```

#### Payments
```
POST   /payments/verify-bank-account     - Verify bank account
POST   /payments/add-bank-account        - Add bank account
GET    /payments/bank-accounts           - List bank accounts
POST   /webhooks/monnify                 - Monnify webhook
```

#### Dashboard
```
GET    /dashboard/analytics              - Get store analytics
GET    /dashboard/recent-orders          - Recent orders
GET    /dashboard/customers              - Customer list
GET    /dashboard/revenue                - Revenue stats
```

---

## 🚢 Deployment

### Frontend (Vercel)

1. **Connect GitHub repo**
2. **Configure build settings:**
   - Framework: Next.js
   - Build Command: `npm run build`
   - Output Directory: `.next`

3. **Add environment variables** (from `.env.example`)

4. **Configure custom domain:**
   - Add `agmshop.com` and `*.agmshop.com`
   - Update Cloudflare DNS

### Backend (Railway / Render)

1. **Create new service** from GitHub
2. **Configure:**
   - Build Command: `npm run build`
   - Start Command: `npm start`

3. **Add PostgreSQL database**
4. **Add Redis instance**
5. **Set environment variables**
6. **Run migrations:**
   ```bash
   npx prisma migrate deploy
   ```

### Database Migrations

```bash
# Create new migration
npx prisma migrate dev --name migration_name

# Deploy to production
npx prisma migrate deploy

# Generate Prisma Client
npx prisma generate
```

---

## 🧪 Testing

### Unit Tests
```bash
npm run test
```

### Integration Tests
```bash
npm run test:integration
```

### E2E Tests
```bash
npm run test:e2e
```

---

## 📊 Monitoring

- **Error Tracking:** Sentry
- **Analytics:** PostHog / Mixpanel
- **Logs:** Better Stack / Logtail
- **Uptime:** UptimeRobot

---

## 🤝 Contributing

1. Fork the repository
2. Create feature branch (`git checkout -b feature/amazing-feature`)
3. Commit changes (`git commit -m 'Add amazing feature'`)
4. Push to branch (`git push origin feature/amazing-feature`)
5. Open Pull Request

---

## 📄 License

MIT License - see [LICENSE](LICENSE) file for details

---

## 🙋‍♂️ Support

- **Email:** sammyjayisthename@gmail.com
- **WhatsApp:** +234 XXX XXX XXXX
- **Documentation:** https://docs.agmshop.com

---

## 🗺 Roadmap

### Phase 1 (MVP) - Q1 2025
- [x] User authentication
- [x] Store creation
- [x] Product management
- [x] Order processing
- [x] Payment integration
- [ ] Launch beta

### Phase 2 (Growth) - Q2 2025
- [ ] Premium subscriptions
- [ ] Custom domains
- [ ] WhatsApp integration
- [ ] Email automation
- [ ] Analytics dashboard

### Phase 3 (Scale) - Q3 2025
- [ ] AI product descriptions
- [ ] AI chatbot support
- [ ] Delivery integrations
- [ ] Digital products
- [ ] Affiliate system

---

**Built with ❤️ for Nigerian entrepreneurs**
