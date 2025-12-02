# AGM Store Builder - Complete File Structure

> **Detailed project organization for Railway backend + Vercel frontend deployment**

---

## 📋 Table of Contents

1. [Project Root Structure](#project-root-structure)
2. [Frontend (Next.js on Vercel)](#frontend-nextjs-on-vercel)
3. [Backend (Express on Railway)](#backend-express-on-railway)
4. [Shared Code](#shared-code)
5. [Configuration Files](#configuration-files)
6. [Documentation](#documentation)
7. [Scripts & Automation](#scripts--automation)
8. [Deployment Files](#deployment-files)
9. [File Descriptions](#file-descriptions)

---

## Project Root Structure

```
agm-store-builder/
│
├── 📁 frontend/                    # Next.js application (Vercel)
├── 📁 backend/                     # Express API server (Railway)
├── 📁 shared/                      # Shared types and constants
├── 📁 docs/                        # Project documentation
├── 📁 scripts/                     # Utility scripts
├── 📁 .github/                     # GitHub Actions & templates
│
├── 📄 README.md                    # Main project documentation
├── 📄 ARCHITECTURE.md              # System architecture
├── 📄 DEVELOPMENT_PROMPT.md        # AI assistant guide
├── 📄 .gitignore                   # Git ignore rules
├── 📄 LICENSE                      # MIT License
├── 📄 package.json                 # Root package (optional)
└── 📄 .env.example                 # Environment variables template
```

---

## Frontend (Next.js on Vercel)

### Complete Frontend Structure

```
frontend/
│
├── 📁 public/                           # Static assets
│   ├── favicon.ico                      # Site favicon
│   ├── logo.svg                         # AGM logo
│   ├── logo-white.svg                   # White version for dark bg
│   ├── og-image.png                     # Open Graph image (1200x630)
│   ├── apple-touch-icon.png             # iOS home screen icon
│   ├── manifest.json                    # PWA manifest
│   ├── robots.txt                       # SEO robots file
│   │
│   ├── 📁 images/                       # Static images
│   │   ├── hero-banner.jpg
│   │   ├── features-1.png
│   │   ├── features-2.png
│   │   ├── testimonial-bg.jpg
│   │   └── 404-illustration.svg
│   │
│   └── 📁 templates/                    # Template preview images
│       ├── products-template.png
│       ├── bookings-template.png
│       ├── portfolio-template.png
│       ├── products-mobile.png
│       ├── bookings-mobile.png
│       └── portfolio-mobile.png
│
├── 📁 src/
│   │
│   ├── 📁 app/                          # Next.js 14 App Router
│   │   │
│   │   ├── layout.tsx                   # Root layout with providers
│   │   ├── page.tsx                     # Landing page (/)
│   │   ├── globals.css                  # Global styles & Tailwind
│   │   ├── loading.tsx                  # Root loading state
│   │   ├── error.tsx                    # Root error boundary
│   │   ├── not-found.tsx                # 404 page
│   │   │
│   │   ├── 📁 (marketing)/              # Marketing pages group
│   │   │   ├── layout.tsx               # Marketing layout (navbar + footer)
│   │   │   ├── about/
│   │   │   │   └── page.tsx
│   │   │   ├── pricing/
│   │   │   │   └── page.tsx
│   │   │   ├── features/
│   │   │   │   └── page.tsx
│   │   │   ├── contact/
│   │   │   │   └── page.tsx
│   │   │   └── blog/
│   │   │       ├── page.tsx
│   │   │       └── [slug]/
│   │   │           └── page.tsx
│   │   │
│   │   ├── 📁 (auth)/                   # Authentication routes
│   │   │   ├── layout.tsx               # Auth layout (centered card)
│   │   │   │
│   │   │   ├── login/
│   │   │   │   ├── page.tsx             # Login form
│   │   │   │   └── loading.tsx
│   │   │   │
│   │   │   ├── signup/
│   │   │   │   ├── page.tsx             # Signup form
│   │   │   │   └── loading.tsx
│   │   │   │
│   │   │   ├── verify/
│   │   │   │   └── page.tsx             # OTP verification
│   │   │   │
│   │   │   ├── forgot-password/
│   │   │   │   └── page.tsx             # Request reset link
│   │   │   │
│   │   │   └── reset-password/
│   │   │       └── page.tsx             # Reset password form
│   │   │
│   │   ├── 📁 (dashboard)/              # Dashboard routes (protected)
│   │   │   ├── layout.tsx               # Dashboard layout (sidebar + header)
│   │   │   ├── loading.tsx              # Dashboard loading
│   │   │   ├── error.tsx                # Dashboard error boundary
│   │   │   │
│   │   │   ├── dashboard/               # Main dashboard
│   │   │   │   ├── page.tsx             # Analytics overview
│   │   │   │   ├── loading.tsx
│   │   │   │   └── error.tsx
│   │   │   │
│   │   │   ├── orders/                  # Orders management
│   │   │   │   ├── page.tsx             # Orders list
│   │   │   │   ├── loading.tsx
│   │   │   │   ├── error.tsx
│   │   │   │   └── [id]/
│   │   │   │       ├── page.tsx         # Order details
│   │   │   │       └── loading.tsx
│   │   │   │
│   │   │   ├── products/                # Products management
│   │   │   │   ├── page.tsx             # Products list
│   │   │   │   ├── loading.tsx
│   │   │   │   ├── error.tsx
│   │   │   │   ├── new/
│   │   │   │   │   ├── page.tsx         # Create product
│   │   │   │   │   └── loading.tsx
│   │   │   │   └── [id]/
│   │   │   │       ├── page.tsx         # Product details
│   │   │   │       ├── loading.tsx
│   │   │   │       └── edit/
│   │   │   │           └── page.tsx     # Edit product
│   │   │   │
│   │   │   ├── customers/               # Customers list
│   │   │   │   ├── page.tsx
│   │   │   │   ├── loading.tsx
│   │   │   │   └── [id]/
│   │   │   │       └── page.tsx         # Customer details
│   │   │   │
│   │   │   ├── analytics/               # Advanced analytics
│   │   │   │   ├── page.tsx
│   │   │   │   └── loading.tsx
│   │   │   │
│   │   │   ├── reviews/                 # Customer reviews
│   │   │   │   ├── page.tsx
│   │   │   │   └── [id]/
│   │   │   │       └── page.tsx
│   │   │   │
│   │   │   └── settings/                # Store settings
│   │   │       ├── page.tsx             # Settings overview
│   │   │       ├── loading.tsx
│   │   │       │
│   │   │       ├── store/               # Store customization
│   │   │       │   └── page.tsx
│   │   │       │
│   │   │       ├── payment/             # Payment settings
│   │   │       │   └── page.tsx
│   │   │       │
│   │   │       ├── domain/              # Custom domain (premium)
│   │   │       │   └── page.tsx
│   │   │       │
│   │   │       ├── notifications/       # Notification preferences
│   │   │       │   └── page.tsx
│   │   │       │
│   │   │       ├── team/                # Team members (future)
│   │   │       │   └── page.tsx
│   │   │       │
│   │   │       └── profile/             # User profile
│   │   │           └── page.tsx
│   │   │
│   │   ├── 📁 onboarding/               # Store setup wizard
│   │   │   ├── layout.tsx               # Wizard layout with steps
│   │   │   │
│   │   │   ├── step-1-name/
│   │   │   │   └── page.tsx             # Choose store name/username
│   │   │   │
│   │   │   ├── step-2-template/
│   │   │   │   └── page.tsx             # Select template
│   │   │   │
│   │   │   ├── step-3-customize/
│   │   │   │   └── page.tsx             # Brand customization
│   │   │   │
│   │   │   ├── step-4-products/
│   │   │   │   └── page.tsx             # Add first products
│   │   │   │
│   │   │   ├── step-5-payment/
│   │   │   │   └── page.tsx             # Bank account setup
│   │   │   │
│   │   │   └── complete/
│   │   │       └── page.tsx             # Success page
│   │   │
│   │   ├── 📁 store/                    # Dynamic store pages (subdomain)
│   │   │   └── [username]/
│   │   │       ├── page.tsx             # Store homepage (SSR)
│   │   │       ├── layout.tsx           # Store layout
│   │   │       ├── loading.tsx          # Store loading
│   │   │       ├── error.tsx            # Store error
│   │   │       ├── not-found.tsx        # Store 404
│   │   │       │
│   │   │       ├── products/            # Product pages
│   │   │       │   └── [id]/
│   │   │       │       ├── page.tsx     # Product detail (SSR)
│   │   │       │       └── loading.tsx
│   │   │       │
│   │   │       ├── checkout/            # Checkout flow
│   │   │       │   ├── page.tsx         # Checkout form
│   │   │       │   └── success/
│   │   │       │       └── page.tsx     # Payment instructions
│   │   │       │
│   │   │       ├── track/               # Order tracking
│   │   │       │   └── [orderNumber]/
│   │   │       │       └── page.tsx
│   │   │       │
│   │   │       ├── book/                # Booking page (for bookings template)
│   │   │       │   └── page.tsx
│   │   │       │
│   │   │       └── about/               # Store about page
│   │   │           └── page.tsx
│   │   │
│   │   ├── 📁 api/                      # API routes (optional, for webhooks)
│   │   │   ├── health/
│   │   │   │   └── route.ts             # Health check endpoint
│   │   │   │
│   │   │   ├── revalidate/
│   │   │   │   └── route.ts             # ISR revalidation
│   │   │   │
│   │   │   └── webhooks/
│   │   │       └── clerk/               # If using Clerk for auth
│   │   │           └── route.ts
│   │   │
│   │   └── middleware.ts                # CRITICAL: Subdomain routing logic
│   │
│   ├── 📁 components/                   # React components
│   │   │
│   │   ├── 📁 ui/                       # shadcn/ui base components
│   │   │   ├── button.tsx
│   │   │   ├── input.tsx
│   │   │   ├── textarea.tsx
│   │   │   ├── select.tsx
│   │   │   ├── card.tsx
│   │   │   ├── dialog.tsx
│   │   │   ├── dropdown-menu.tsx
│   │   │   ├── form.tsx
│   │   │   ├── label.tsx
│   │   │   ├── separator.tsx
│   │   │   ├── skeleton.tsx
│   │   │   ├── table.tsx
│   │   │   ├── tabs.tsx
│   │   │   ├── toast.tsx
│   │   │   ├── toaster.tsx
│   │   │   ├── alert.tsx
│   │   │   ├── alert-dialog.tsx
│   │   │   ├── badge.tsx
│   │   │   ├── calendar.tsx
│   │   │   ├── checkbox.tsx
│   │   │   ├── popover.tsx
│   │   │   ├── progress.tsx
│   │   │   ├── radio-group.tsx
│   │   │   ├── scroll-area.tsx
│   │   │   ├── sheet.tsx
│   │   │   ├── slider.tsx
│   │   │   ├── switch.tsx
│   │   │   └── tooltip.tsx
│   │   │
│   │   ├── 📁 auth/                     # Authentication components
│   │   │   ├── LoginForm.tsx            # Email/phone login
│   │   │   ├── SignupForm.tsx           # Registration form
│   │   │   ├── OTPInput.tsx             # 6-digit OTP input
│   │   │   ├── OTPVerification.tsx      # OTP verification flow
│   │   │   ├── ForgotPasswordForm.tsx
│   │   │   ├── ResetPasswordForm.tsx
│   │   │   ├── ProtectedRoute.tsx       # Route guard HOC
│   │   │   ├── AuthProvider.tsx         # Auth context provider
│   │   │   └── SocialLogin.tsx          # Google/Facebook login
│   │   │
│   │   ├── 📁 dashboard/                # Dashboard components
│   │   │   ├── Sidebar.tsx              # Main sidebar navigation
│   │   │   ├── Header.tsx               # Dashboard header
│   │   │   ├── MobileNav.tsx            # Mobile navigation
│   │   │   ├── Breadcrumbs.tsx          # Navigation breadcrumbs
│   │   │   ├── StatsCard.tsx            # Metric display card
│   │   │   ├── RevenueChart.tsx         # Revenue line chart
│   │   │   ├── OrdersChart.tsx          # Orders bar chart
│   │   │   ├── TopProducts.tsx          # Best selling products
│   │   │   ├── RecentOrders.tsx         # Recent orders list
│   │   │   ├── QuickActions.tsx         # Quick action buttons
│   │   │   ├── NotificationBell.tsx     # Notifications dropdown
│   │   │   ├── UserMenu.tsx             # User dropdown menu
│   │   │   └── SearchBar.tsx            # Global search
│   │   │
│   │   ├── 📁 products/                 # Product components
│   │   │   ├── ProductCard.tsx          # Product grid item
│   │   │   ├── ProductGrid.tsx          # Products grid layout
│   │   │   ├── ProductList.tsx          # Products list (table)
│   │   │   ├── ProductForm.tsx          # Create/edit product form
│   │   │   ├── ProductFormBasic.tsx     # Basic info step
│   │   │   ├── ProductFormPricing.tsx   # Pricing step
│   │   │   ├── ProductFormInventory.tsx # Inventory step
│   │   │   ├── ProductFormImages.tsx    # Images step
│   │   │   ├── ImageUpload.tsx          # Drag & drop image upload
│   │   │   ├── ImageGallery.tsx         # Product image gallery
│   │   │   ├── VariationManager.tsx     # Size/color variations
│   │   │   ├── VariationRow.tsx         # Single variation item
│   │   │   ├── InventoryTracker.tsx     # Stock level indicator
│   │   │   ├── ProductFilter.tsx        # Filter sidebar
│   │   │   ├── ProductSort.tsx          # Sort dropdown
│   │   │   ├── BulkActions.tsx          # Bulk edit/delete
│   │   │   └── ProductImport.tsx        # CSV import (future)
│   │   │
│   │   ├── 📁 orders/                   # Order components
│   │   │   ├── OrderCard.tsx            # Order summary card
│   │   │   ├── OrderList.tsx            # Orders table
│   │   │   ├── OrderDetails.tsx         # Full order view
│   │   │   ├── OrderStatusBadge.tsx     # Status indicator
│   │   │   ├── OrderTimeline.tsx        # Order history timeline
│   │   │   ├── OrderItems.tsx           # Order line items
│   │   │   ├── OrderCustomer.tsx        # Customer info card
│   │   │   ├── OrderActions.tsx         # Action buttons
│   │   │   ├── UpdateStatusDialog.tsx   # Change status modal
│   │   │   ├── RefundDialog.tsx         # Refund modal
│   │   │   ├── OrderFilter.tsx          # Filter by status/date
│   │   │   ├── OrderExport.tsx          # Export orders (CSV/PDF)
│   │   │   └── PrintInvoice.tsx         # Print invoice button
│   │   │
│   │   ├── 📁 store/                    # Storefront components
│   │   │   ├── StoreHeader.tsx          # Store header/nav
│   │   │   ├── StoreFooter.tsx          # Store footer
│   │   │   ├── StoreLayout.tsx          # Store wrapper layout
│   │   │   ├── StoreBanner.tsx          # Hero banner
│   │   │   ├── ProductListing.tsx       # Product grid on store
│   │   │   ├── ProductQuickView.tsx     # Quick view modal
│   │   │   ├── AddToCartButton.tsx      # Add to cart CTA
│   │   │   ├── Cart.tsx                 # Shopping cart sidebar
│   │   │   ├── CartItem.tsx             # Cart line item
│   │   │   ├── CartSummary.tsx          # Cart totals
│   │   │   ├── CheckoutForm.tsx         # Customer checkout form
│   │   │   ├── CheckoutSummary.tsx      # Order summary
│   │   │   ├── PaymentInstructions.tsx  # Bank transfer details
│   │   │   ├── OrderConfirmation.tsx    # Success page
│   │   │   ├── SearchProducts.tsx       # Store search
│   │   │   ├── CategoryFilter.tsx       # Category sidebar
│   │   │   └── StoreContact.tsx         # Contact section
│   │   │
│   │   ├── 📁 onboarding/               # Onboarding wizard components
│   │   │   ├── StepIndicator.tsx        # Progress bar
│   │   │   ├── WizardNav.tsx            # Next/back buttons
│   │   │   ├── UsernameInput.tsx        # Username availability check
│   │   │   ├── TemplateSelector.tsx     # Template cards
│   │   │   ├── TemplatePreview.tsx      # Template preview modal
│   │   │   ├── ColorPicker.tsx          # Brand color picker
│   │   │   ├── FontSelector.tsx         # Font dropdown
│   │   │   ├── LogoUpload.tsx           # Logo uploader
│   │   │   ├── QuickProductForm.tsx     # Simplified product add
│   │   │   ├── BankAccountForm.tsx      # Bank details form
│   │   │   ├── BankVerification.tsx     # Paystack verification
│   │   │   └── OnboardingSuccess.tsx    # Completion screen
│   │   │
│   │   ├── 📁 settings/                 # Settings components
│   │   │   ├── StoreSettingsForm.tsx    # Store name, description
│   │   │   ├── BrandingSettings.tsx     # Colors, fonts, logo
│   │   │   ├── DomainSettings.tsx       # Custom domain (premium)
│   │   │   ├── PaymentSettings.tsx      # Bank accounts
│   │   │   ├── NotificationSettings.tsx # Email/SMS preferences
│   │   │   ├── ProfileSettings.tsx      # User profile
│   │   │   ├── SecuritySettings.tsx     # Password, 2FA
│   │   │   ├── TeamSettings.tsx         # Team members (future)
│   │   │   ├── BillingSettings.tsx      # Subscription (Phase 2)
│   │   │   └── DangerZone.tsx           # Delete account
│   │   │
│   │   ├── 📁 analytics/                # Analytics components
│   │   │   ├── RevenueCard.tsx          # Total revenue
│   │   │   ├── OrdersCard.tsx           # Total orders
│   │   │   ├── CustomersCard.tsx        # Total customers
│   │   │   ├── ConversionCard.tsx       # Conversion rate
│   │   │   ├── SalesChart.tsx           # Sales over time
│   │   │   ├── TopProductsChart.tsx     # Best sellers
│   │   │   ├── TrafficSources.tsx       # Traffic breakdown
│   │   │   ├── CustomerGrowth.tsx       # Customer growth
│   │   │   ├── DateRangePicker.tsx      # Filter by date
│   │   │   └── ExportReport.tsx         # Export analytics
│   │   │
│   │   ├── 📁 marketing/                # Marketing page components
│   │   │   ├── Hero.tsx                 # Landing hero
│   │   │   ├── Features.tsx             # Features section
│   │   │   ├── HowItWorks.tsx           # Steps explanation
│   │   │   ├── Testimonials.tsx         # Customer reviews
│   │   │   ├── Pricing.tsx              # Pricing tiers
│   │   │   ├── FAQ.tsx                  # FAQ accordion
│   │   │   ├── CTA.tsx                  # Call to action
│   │   │   ├── Navbar.tsx               # Marketing navbar
│   │   │   └── Footer.tsx               # Marketing footer
│   │   │
│   │   └── 📁 shared/                   # Shared/common components
│   │       ├── Logo.tsx                 # AGM logo component
│   │       ├── LoadingSpinner.tsx       # Loading indicator
│   │       ├── LoadingSkeleton.tsx      # Content placeholder
│   │       ├── EmptyState.tsx           # Empty list placeholder
│   │       ├── ErrorBoundary.tsx        # Error boundary wrapper
│   │       ├── ErrorMessage.tsx         # Error display
│   │       ├── SuccessMessage.tsx       # Success toast
│   │       ├── ConfirmDialog.tsx        # Confirmation modal
│   │       ├── DataTable.tsx            # Reusable data table
│   │       ├── Pagination.tsx           # Pagination controls
│   │       ├── FileUploader.tsx         # Generic file uploader
│   │       ├── RichTextEditor.tsx       # WYSIWYG editor
│   │       ├── CopyButton.tsx           # Copy to clipboard
│   │       ├── BackButton.tsx           # Browser back button
│   │       ├── PageHeader.tsx           # Page title + actions
│   │       └── Container.tsx            # Max-width wrapper
│   │
│   ├── 📁 lib/                          # Utility functions
│   │   ├── api.ts                       # API client (axios wrapper)
│   │   ├── auth.ts                      # Auth utilities
│   │   ├── utils.ts                     # General utilities
│   │   ├── cn.ts                        # className utility (shadcn)
│   │   ├── constants.ts                 # App constants
│   │   ├── validators.ts                # Zod validation schemas
│   │   ├── format.ts                    # Date/currency formatters
│   │   ├── storage.ts                   # localStorage wrapper
│   │   ├── seo.ts                       # SEO utilities
│   │   └── analytics.ts                 # Analytics helpers
│   │
│   ├── 📁 hooks/                        # Custom React hooks
│   │   ├── useAuth.ts                   # Auth state & actions
│   │   ├── useUser.ts                   # User data hook
│   │   ├── useStore.ts                  # Store data hook
│   │   ├── useProducts.ts               # Products CRUD
│   │   ├── useOrders.ts                 # Orders management
│   │   ├── useCart.ts                   # Shopping cart
│   │   ├── useCheckout.ts               # Checkout flow
│   │   ├── useUpload.ts                 # File upload
│   │   ├── useDebounce.ts               # Debounce input
│   │   ├── useMediaQuery.ts             # Responsive breakpoints
│   │   ├── useLocalStorage.ts           # Persist to localStorage
│   │   ├── useInfiniteScroll.ts         # Infinite scroll
│   │   ├── useCopyToClipboard.ts        # Copy helper
│   │   └── useToast.ts                  # Toast notifications
│   │
│   ├── 📁 store/                        # Zustand state management
│   │   ├── index.ts                     # Store exports
│   │   ├── authStore.ts                 # Auth state
│   │   ├── cartStore.ts                 # Cart state
│   │   ├── uiStore.ts                   # UI state (sidebar, modals)
│   │   └── notificationStore.ts         # Notifications
│   │
│   ├── 📁 types/                        # TypeScript definitions
│   │   ├── index.ts                     # Type exports
│   │   ├── api.ts                       # API response types
│   │   ├── user.ts                      # User types
│   │   ├── store.ts                     # Store types
│   │   ├── product.ts                   # Product types
│   │   ├── order.ts                     # Order types
│   │   ├── payment.ts                   # Payment types
│   │   ├── analytics.ts                 # Analytics types
│   │   └── global.d.ts                  # Global type declarations
│   │
│   ├── 📁 styles/                       # Additional styles
│   │   ├── globals.css                  # Global styles
│   │   ├── variables.css                # CSS variables
│   │   └── animations.css               # Custom animations
│   │
│   └── middleware.ts                    # CRITICAL: Subdomain routing
│
├── 📁 tests/                            # Frontend tests
│   ├── 📁 components/
│   │   ├── auth/
│   │   ├── dashboard/
│   │   ├── products/
│   │   └── store/
│   │
│   ├── 📁 pages/
│   │   ├── dashboard.test.tsx
│   │   ├── onboarding.test.tsx
│   │   └── store.test.tsx
│   │
│   ├── 📁 utils/
│   │   ├── api.test.ts
│   │   └── format.test.ts
│   │
│   └── setup.ts                         # Test setup
│
├── 📄 package.json                      # Dependencies
├── 📄 package-lock.json
├── 📄 tsconfig.json                     # TypeScript config
├── 📄 next.config.js                    # Next.js config
├── 📄 tailwind.config.ts                # Tailwind config
├── 📄 postcss.config.js                 # PostCSS config
├── 📄 components.json                   # shadcn/ui config
├── 📄 .env.local                        # Local environment variables
├── 📄 .env.example                      # Environment template
├── 📄 .eslintrc.json                    # ESLint config
├── 📄 .prettierrc                       # Prettier config
├── 📄 .gitignore                        # Git ignore
├── 📄 vercel.json                       # Vercel config (IMPORTANT)
└── 📄 README.md                         # Frontend docs
```

---

## Backend (Express on Railway)

### Complete Backend Structure

```
backend/
│
├── 📁 prisma/                           # Prisma ORM
│   ├── schema.prisma                    # Database schema (CRITICAL)
│   ├── seed.ts                          # Database seeding
│   │
│   └── 📁 migrations/                   # Database migrations
│       ├── 20250101000000_init/
│       │   └── migration.sql
│       ├── 20250102000000_add_virtual_accounts/
│       │   └── migration.sql
│       └── 20250103000000_add_reviews/
│           └── migration.sql
│
├── 📁 src/
│   │
│   ├── index.ts                         # Entry point
│   ├── app.ts                           # Express app setup
│   ├── server.ts                        # Server startup
│   │
│   ├── 📁 config/                       # Configuration files
│   │   ├── database.ts                  # Prisma client singleton
│   │   ├── redis.ts                     # Redis client
│   │   ├── aws.ts                       # S3 config
│   │   ├── cloudinary.ts                # Cloudinary config (alternative)
│   │   ├── monnify.ts                   # Monnify API config
│   │   ├── paystack.ts                  # Paystack config
│   │   ├── termii.ts                    # Termii SMS config
│   │   ├── resend.ts                    # Resend email config
│   │   ├── jwt.ts                       # JWT config
│   │   ├── cors.ts                      # CORS settings
│   │   ├── rate-limit.ts                # Rate limiter config
│   │   └── constants.ts                 # App constants
│   │
│   ├── 📁 controllers/                  # HTTP request handlers
│   │   ├── auth.controller.ts           # Auth endpoints
│   │   ├── user.controller.ts           # User management
│   │   ├── store.controller.ts          # Store CRUD
│   │   ├── product.controller.ts        # Product CRUD
│   │   ├── order.controller.ts          # Order management
│   │   ├── payment.controller.ts        # Payment operations
│   │   ├── upload.controller.ts         # File uploads
│   │   ├── dashboard.controller.ts      # Analytics
│   │   ├── customer.controller.ts       # Customer data
│   │   ├── review.controller.ts         # Reviews
│   │   ├── webhook.controller.ts        # Webhook handlers
│   │   └── health.controller.ts         # Health check
│   │
│   ├── 📁 services/                     # Business logic layer
│   │   ├── auth.service.ts              # Auth logic
│   │   ├── user.service.ts              # User operations
│   │   ├── store.service.ts             # Store operations
│   │   ├── product.service.ts           # Product operations
│   │   ├── order.service.ts             # Order operations
│   │   ├── payment.service.ts           # Payment orchestration
│   │   ├── monnify.service.ts           # Monnify integration
│   │   ├── paystack.service.ts          # Paystack integration
│   │   ├── email.service.ts             # Email sending
│   │   ├── sms.service.ts               # SMS sending
│   │   ├── upload.service.ts            # File upload (S3/Cloudinary)
│   │   ├── analytics.service.ts         # Analytics calculations
│   │   ├── notification.service.ts      # Multi-channel notifications
│   │   ├── otp.service.ts               # OTP generation/verification
│   │   └── cache.service.ts             # Redis caching
│   │
│   ├── 📁 repositories/                 # Data access layer
│   │   ├── user.repository.ts           # User DB queries
│   │   ├── store.repository.ts          # Store DB queries
│   │   ├── product.repository.ts        # Product DB queries
│   │   ├── order.repository.ts          # Order DB queries
│   │   ├── transaction.repository.ts    # Transaction DB queries
│   │   ├── bank-account.repository.ts   # Bank account queries
│   │   ├── virtual-account.repository.ts # Virtual account queries
│   │   ├── customer.repository.ts       # Customer queries
│   │   └── review.repository.ts         # Review queries
│   │
│   ├── 📁 middleware/                   # Express middleware
│   │   ├── auth.middleware.ts           # JWT verification
│   │   ├── validate.middleware.ts       # Request validation
│   │   ├── error.middleware.ts          # Error handling
│   │   ├── rate-limit.middleware.ts     # Rate limiting
│   │   ├── cors.middleware.ts           # CORS setup
│   │   ├── logger.middleware.ts         # Request logging
│   │   ├── upload.middleware.ts         # Multer setup
│   │   ├── webhook-verify.middleware.ts # Webhook signature verification
│   │   └── owner.middleware.ts          # Resource ownership check
│   │
│   ├── 📁 routes/                       # API routes
│   │   ├── index.ts                     # Route aggregator
│   │   ├── auth.routes.ts               # /api/v1/auth/*
│   │   ├── user.routes.ts               # /api/v1/users/*
│   │   ├── store.routes.ts              # /api/v1/stores/*
│   │   ├── product.routes.ts            # /api/v1/products/*
│   │   ├── order.routes.ts              # /api/v1/orders/*
│   │   ├── payment.routes.ts            # /api/v1/payments/*
│   │   ├── upload.routes.ts             # /api/v1/upload/*
│   │   ├── dashboard.routes.ts          # /api/v1/dashboard/*
│   │   ├── customer.routes.ts           # /api/v1/customers/*
│   │   ├── review.routes.ts             # /api/v1/reviews/*
│   │   ├── webhook.routes.ts            # /api/v1/webhooks/*
│   │   └── health.routes.ts             # /api/v1/health
│   │
│   ├── 📁 validators/                   # Zod validation schemas
│   │   ├── auth.validator.ts            # Auth schemas
│   │   ├── user.validator.ts            # User schemas
│   │   ├── store.validator.ts           # Store schemas
│   │   ├── product.validator.ts         # Product schemas
│   │   ├── order.validator.ts           # Order schemas
│   │   ├── payment.validator.ts         # Payment schemas
│   │   ├── review.validator.ts          # Review schemas
│   │   └── common.validator.ts          # Shared schemas
│   │
│   ├── 📁 jobs/                         # Background jobs (BullMQ)
│   │   ├── index.ts                     # Job exports
│   │   ├── queues.ts                    # Queue definitions
│   │   ├── workers.ts                   # Worker setup
│   │   │
│   │   ├── 📁 processors/               # Job processors
│   │   │   ├── payout.processor.ts      # Process payouts
│   │   │   ├── notification.processor.ts # Send notifications
│   │   │   ├── analytics.processor.ts   # Update analytics
│   │   │   ├── email.processor.ts       # Send emails
│   │   │   └── sms.processor.ts         # Send SMS
│   │   │
│   │   └── 📁 schedulers/               # Scheduled jobs
│   │       ├── daily-summary.ts         # Daily sales summary
│   │       ├── abandoned-cart.ts        # Abandoned cart reminders
│   │       └── inventory-alerts.ts      # Low stock alerts
│   │
│   ├── 📁 types/                        # TypeScript types
│   │   ├── index.ts                     # Type exports
│   │   ├── express.d.ts                 # Express type extensions
│   │   ├── user.types.ts                # User types
│   │   ├── store.types.ts               # Store types
│   │   ├── product.types.ts             # Product types
│   │   ├── order.types.ts               # Order types
│   │   ├── payment.types.ts             # Payment types
│   │   ├── monnify.types.ts             # Monnify API types
│   │   ├── paystack.types.ts            # Paystack API types
│   │   └── job.types.ts                 # Job types
│   │
│   ├── 📁 utils/                        # Utility functions
│   │   ├── bcrypt.util.ts               # Password hashing
│   │   ├── jwt.util.ts                  # JWT operations
│   │   ├── otp.util.ts                  # OTP generation
│   │   ├── slug.util.ts                 # Slug generation
│   │   ├── date.util.ts                 # Date utilities
│   │   ├── currency.util.ts             # Currency formatting
│   │   ├── validator.util.ts            # Custom validators
│   │   ├── error.util.ts                # Error handling
│   │   ├── response.util.ts             # Response formatting
│   │   └── webhook.util.ts              # Webhook verification
│   │
│   ├── 📁 lib/                          # External integrations
│   │   ├── prisma.ts                    # Prisma client
│   │   ├── redis.ts                     # Redis client
│   │   ├── logger.ts                    # Winston logger
│   │   ├── sentry.ts                    # Sentry error tracking
│   │   └── metrics.ts                   # Performance metrics
│   │
│   ├── 📁 constants/                    # Application constants
│   │   ├── errors.ts                    # Error codes/messages
│   │   ├── messages.ts                  # Success messages
│   │   ├── status-codes.ts              # HTTP status codes
│   │   ├── reserved-usernames.ts        # Reserved usernames list
│   │   ├── templates.ts                 # Store template IDs
│   │   └── banks.ts                     # Nigerian bank list
│   │
│   └── 📁 templates/                    # Email/SMS templates
│       ├── 📁 email/
│       │   ├── welcome.html             # Welcome email
│       │   ├── otp.html                 # OTP email
│       │   ├── order-confirmation.html
│       │   ├── payment-received.html
│       │   └── payout-completed.html
│       │
│       └── 📁 sms/
│           ├── otp.ts                   # OTP SMS template
│           ├── order-confirmed.ts
│           └── payment-received.ts
│
├── 📁 tests/                            # Backend tests
│   ├── 📁 unit/
│   │   ├── 📁 services/
│   │   │   ├── auth.service.test.ts
│   │   │   ├── store.service.test.ts
│   │   │   ├── product.service.test.ts
│   │   │   ├── order.service.test.ts
│   │   │   └── payment.service.test.ts
│   │   │
│   │   ├── 📁 repositories/
│   │   │   ├── user.repository.test.ts
│   │   │   └── store.repository.test.ts
│   │   │
│   │   └── 📁 utils/
│   │       ├── jwt.util.test.ts
│   │       ├── otp.util.test.ts
│   │       └── currency.util.test.ts
│   │
│   ├── 📁 integration/
│   │   ├── auth.test.ts                 # Auth endpoints
│   │   ├── store.test.ts                # Store endpoints
│   │   ├── product.test.ts              # Product endpoints
│   │   ├── order.test.ts                # Order endpoints
│   │   ├── payment.test.ts              # Payment endpoints
│   │   └── webhook.test.ts              # Webhook endpoints
│   │
│   ├── 📁 e2e/
│   │   ├── full-checkout.test.ts        # Complete checkout flow
│   │   ├── store-creation.test.ts       # Store setup flow
│   │   └── payment-webhook.test.ts      # Payment flow
│   │
│   ├── setup.ts                         # Test setup
│   ├── teardown.ts                      # Test cleanup
│   └── helpers.ts                       # Test utilities
│
├── 📁 scripts/                          # Utility scripts
│   ├── seed.ts                          # Seed database
│   ├── reset-db.ts                      # Reset database
│   ├── generate-banks.ts                # Fetch Nigerian banks
│   └── migrate.ts                       # Run migrations
│
├── 📄 package.json                      # Dependencies
├── 📄 package-lock.json
├── 📄 tsconfig.json                     # TypeScript config
├── 📄 nodemon.json                      # Nodemon config
├── 📄 .env                              # Environment variables
├── 📄 .env.example                      # Environment template
├── 📄 .eslintrc.json                    # ESLint config
├── 📄 .prettierrc                       # Prettier config
├── 📄 .gitignore                        # Git ignore
├── 📄 Dockerfile                        # Docker config
├── 📄 railway.json                      # Railway config (IMPORTANT)
├── 📄 railway.toml                      # Railway deployment
└── 📄 README.md                         # Backend docs
```

---

## Shared Code

```
shared/
│
├── 📁 types/
│   ├── api.types.ts                     # Shared API types
│   ├── store.types.ts                   # Store types
│   ├── product.types.ts                 # Product types
│   └── order.types.ts                   # Order types
│
├── 📁 constants/
│   ├── app-constants.ts                 # App-wide constants
│   ├── status.ts                        # Order/payment statuses
│   └── templates.ts                     # Template definitions
│
├── 📁 validators/
│   └── shared.validators.ts             # Shared Zod schemas
│
└── 📄 package.json                      # Shared package
```

---

## Configuration Files

### Root Level Configuration

```
agm-store-builder/
│
├── 📄 .gitignore                        # Git ignore rules
├── 📄 .env.example                      # Environment template
├── 📄 package.json                      # Root package (monorepo setup)
├── 📄 turbo.json                        # Turborepo config (optional)
├── 📄 pnpm-workspace.yaml               # PNPM workspace (optional)
└── 📄 .nvmrc                            # Node version
```

### Frontend Configuration Files

```
frontend/
│
├── 📄 next.config.js                    # Next.js configuration
├── 📄 tsconfig.json                     # TypeScript configuration
├── 📄 tailwind.config.ts                # Tailwind CSS configuration
├── 📄 postcss.config.js                 # PostCSS configuration
├── 📄 components.json                   # shadcn/ui configuration
├── 📄 .eslintrc.json                    # ESLint rules
├── 📄 .prettierrc                       # Prettier formatting
├── 📄 vercel.json                       # Vercel deployment config
└── 📄 .env.local                        # Local environment variables
```

### Backend Configuration Files

```
backend/
│
├── 📄 tsconfig.json                     # TypeScript configuration
├── 📄 nodemon.json                      # Development server config
├── 📄 .eslintrc.json                    # ESLint rules
├── 📄 .prettierrc                       # Prettier formatting
├── 📄 railway.json                      # Railway deployment config
├── 📄 Dockerfile                        # Docker container (optional)
└── 📄 .env                              # Environment variables
```

---

## Documentation

```
docs/
│
├── 📄 README.md                         # Documentation index
├── 📄 ARCHITECTURE.md                   # System architecture
├── 📄 API.md                            # API documentation
├── 📄 DEPLOYMENT.md                     # Deployment guide
├── 📄 DEVELOPMENT.md                    # Development setup
├── 📄 PAYMENT_FLOW.md                   # Payment integration
├── 📄 DATABASE.md                       # Database schema docs
├── 📄 TESTING.md                        # Testing guide
├── 📄 SECURITY.md                       # Security best practices
├── 📄 TROUBLESHOOTING.md                # Common issues
│
├── 📁 api/                              # API documentation
│   ├── auth.md
│   ├── stores.md
│   ├── products.md
│   ├── orders.md
│   └── webhooks.md
│
└── 📁 guides/                           # User guides
    ├── onboarding.md
    ├── creating-products.md
    ├── managing-orders.md
    └── payment-setup.md
```

---

## Scripts & Automation

```
scripts/
│
├── setup.sh                             # Initial project setup
├── install-all.sh                       # Install all dependencies
├── dev.sh                               # Start all dev servers
├── build.sh                             # Build all projects
├── test.sh                              # Run all tests
├── deploy.sh                            # Deploy to production
├── seed-db.ts                           # Seed database with test data
├── migrate.sh                           # Run database migrations
├── backup-db.sh                         # Backup database
└── generate-types.ts                    # Generate TypeScript types
```

---

## Deployment Files

### Vercel Configuration (frontend/vercel.json)

```json
{
  "buildCommand": "npm run build",
  "outputDirectory": ".next",
  "framework": "nextjs",
  "rewrites": [
    {
      "source": "/api/:path*",
      "destination": "https://api.agmshop.com/api/:path*"
    }
  ],
  "headers": [
    {
      "source": "/(.*)",
      "headers": [
        {
          "key": "X-Content-Type-Options",
          "value": "nosniff"
        },
        {
          "key": "X-Frame-Options",
          "value": "DENY"
        },
        {
          "key": "X-XSS-Protection",
          "value": "1; mode=block"
        }
      ]
    }
  ],
  "env": {
    "NEXT_PUBLIC_API_URL": "@api_url",
    "NEXT_PUBLIC_APP_URL": "@app_url"
  }
}
```

### Railway Configuration (backend/railway.json)

```json
{
  "build": {
    "builder": "NIXPACKS",
    "buildCommand": "npm run build"
  },
  "deploy": {
    "startCommand": "npm start",
    "healthcheckPath": "/api/v1/health",
    "healthcheckTimeout": 100,
    "restartPolicyType": "ON_FAILURE",
    "restartPolicyMaxRetries": 3
  }
}
```

### Railway TOML (backend/railway.toml)

```toml
[build]
builder = "NIXPACKS"
buildCommand = "npm ci && npm run build"

[deploy]
startCommand = "npm start"
healthcheckPath = "/api/v1/health"
healthcheckTimeout = 100
restartPolicyType = "ON_FAILURE"
restartPolicyMaxRetries = 3

[[services]]
name = "backend"
port = 4000

[[services]]
name = "postgresql"
type = "database"

[[services]]
name = "redis"
type = "redis"
```

---

## File Descriptions

### Critical Files

#### `frontend/src/middleware.ts`
**Purpose:** Handles subdomain routing for dynamic stores  
**Importance:** ⭐⭐⭐⭐⭐ CRITICAL

```typescript
// Intercepts requests to username.agmshop.com
// Rewrites to /store/[username] for Next.js routing
// Enables dynamic store pages without manual DNS config
```

#### `frontend/next.config.js`
**Purpose:** Next.js configuration  
**Importance:** ⭐⭐⭐⭐⭐ CRITICAL

```javascript
// Configures:
// - Image optimization domains
// - API proxy to backend
// - Webpack customization
// - Environment variables
```

#### `frontend/vercel.json`
**Purpose:** Vercel deployment configuration  
**Importance:** ⭐⭐⭐⭐⭐ CRITICAL

```json
// Configures:
// - Build settings
// - Environment variables
// - API rewrites (proxy to Railway backend)
// - Security headers
// - Custom domains (*.agmshop.com)
```

#### `backend/prisma/schema.prisma`
**Purpose:** Database schema definition  
**Importance:** ⭐⭐⭐⭐⭐ CRITICAL

```prisma
// Defines:
// - All database models
// - Relationships between tables
// - Indexes for performance
// - Field types and constraints
```

#### `backend/railway.json`
**Purpose:** Railway deployment configuration  
**Importance:** ⭐⭐⭐⭐⭐ CRITICAL

```json
// Configures:
// - Build command
// - Start command
// - Health check endpoint
// - Restart policies
// - Environment variables
```

#### `backend/src/controllers/webhook.controller.ts`
**Purpose:** Handles Monnify payment webhooks  
**Importance:** ⭐⭐⭐⭐⭐ CRITICAL

```typescript
// Handles:
// - Payment confirmation webhooks
// - Signature verification
// - Order status updates
// - Payout initiation
```

---

### Important Configuration Files

#### `frontend/tailwind.config.ts`
```typescript
// Tailwind CSS configuration
// - Theme colors
// - Font families
// - Custom utilities
// - Plugin configurations
```

#### `backend/src/config/monnify.ts`
```typescript
// Monnify API configuration
// - API credentials
// - Base URL (sandbox/production)
// - Contract code
// - Timeout settings
```

#### `backend/src/middleware/auth.middleware.ts`
```typescript
// JWT authentication middleware
// - Token extraction from header
// - Token verification
// - User attachment to request
// - Role-based access control
```

---

## Development Workflow

### Starting Development

```bash
# Terminal 1: Backend
cd backend
npm install
npx prisma migrate dev
npm run dev
# Running on http://localhost:4000

# Terminal 2: Frontend
cd frontend
npm install
npm run dev
# Running on http://localhost:3000

# Terminal 3: Background Jobs (optional)
cd backend
npm run worker
```

### Building for Production

```bash
# Frontend (Vercel will run this)
cd frontend
npm run build

# Backend (Railway will run this)
cd backend
npm run build
npm start
```

---

## Deployment Notes

### Vercel Frontend (Free Tier)

**Current URL:** `your-project.vercel.app`  
**Custom Domain (Later):** `agmshop.com` + `*.agmshop.com`

**Free Tier Limits:**
- 100 GB bandwidth/month
- Unlimited deployments
- Automatic SSL
- Edge functions included

**To Remove .vercel.app:**
1. Add custom domain in Vercel dashboard
2. Update DNS records in Cloudflare
3. Vercel automatically provisions SSL

### Railway Backend

**Estimated Cost:** $5-20/month depending on usage

**Included:**
- PostgreSQL database
- Redis instance
- 512MB RAM (scalable)
- Automatic deployments from Git

**Environment Variables Needed:**
```
DATABASE_URL          # Auto-provisioned by Railway
REDIS_URL             # Auto-provisioned by Railway
JWT_SECRET
MONNIFY_API_KEY
MONNIFY_SECRET_KEY
PAYSTACK_SECRET_KEY
AWS_ACCESS_KEY_ID
AWS_SECRET_ACCESS_KEY
TERMII_API_KEY
RESEND_API_KEY
```

---

## Storage Strategy

### Images & Files

**Phase 1 (MVP):** AWS S3
- Product images
- Store logos
- User uploads

**Alternative:** Cloudinary
- Built-in image optimization
- Transformation API
- Generous free tier

### Recommended Structure:
```
s3://agm-store-uploads/
├── stores/
│   └── {storeId}/
│       ├── logo.png
│       └── banner.jpg
│
├── products/
│   └── {productId}/
│       ├── image-1.jpg
│       ├── image-2.jpg
│       └── image-3.jpg
│
└── temp/
    └── {userId}/
        └── upload-{timestamp}.jpg
```

---

## Database Management

### Migrations Workflow

```bash
# Create migration
npx prisma migrate dev --name add_reviews_table

# Apply to production
npx prisma migrate deploy

# Generate Prisma Client
npx prisma generate

# View database
npx prisma studio
```

### Backup Strategy

**Railway Automated Backups:**
- Daily backups (retained 7 days)
- Point-in-time recovery
- Manual backup trigger available

---

## Monitoring & Logging

### Recommended Tools

**Error Tracking:** Sentry
- Frontend errors
- Backend exceptions
- Performance monitoring

**Logging:** Better Stack (Logtail)
- Backend logs
- API request logs
- Job queue logs

**Uptime Monitoring:** UptimeRobot
- API endpoint checks
- Store availability
- Email alerts

**Analytics:** PostHog
- User behavior
- Feature usage
- Conversion tracking

---

## Security Checklist

### Environment Variables
- ✅ Never commit `.env` files
- ✅ Use `.env.example` as template
- ✅ Rotate secrets regularly
- ✅ Use different keys for dev/prod

### API Security
- ✅ Rate limiting on all endpoints
- ✅ JWT token expiration (7 days)
- ✅ HTTPS only in production
- ✅ CORS configured properly
- ✅ Input validation with Zod
- ✅ SQL injection protection (Prisma)

### Payment Security
- ✅ Webhook signature verification
- ✅ HTTPS for webhook URLs
- ✅ Idempotency checks
- ✅ Transaction logging

---

## Next Steps After Setup

1. **Initialize Git repositories**
2. **Set up Vercel project** (connect GitHub)
3. **Set up Railway project** (connect GitHub)
4. **Configure environment variables**
5. **Run database migrations**
6. **Deploy to staging**
7. **Test payment flow**
8. **Deploy to production**
9. **Configure custom domain**
10. **Set up monitoring**

---

**Total Files:** ~200+ files  
**Lines of Code (Estimated):** 15,000-20,000 LOC  
**Development Time:** 4-6 weeks for MVP  

**Repository:** https://github.com/thetruesammyjay/agm-store-builder

---

This structure is production-ready, scalable, and follows industry best practices. Every file has a clear purpose and location. 🚀
