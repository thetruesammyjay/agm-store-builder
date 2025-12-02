# AGM Store Builder - Frontend Development Guide

> Complete guide for building the Next.js 14 frontend with TailwindCSS, shadcn/ui, and mobile-first design

---

## 📋 Table of Contents

1. [Tech Stack](#tech-stack)
2. [Color Scheme](#color-scheme)
3. [Mobile-First Approach](#mobile-first-approach)
4. [Project Setup](#project-setup)
5. [Configuration Files](#configuration-files)
6. [Key Components to Build](#key-components-to-build)
7. [Routing Structure](#routing-structure)
8. [State Management](#state-management)
9. [Form Handling](#form-handling)
10. [API Integration](#api-integration)
11. [Deployment](#deployment)

---

## 🛠 Tech Stack

### Core Framework
- **Next.js 14** - App Router with Server Components
- **React 18** - UI library
- **TypeScript** - Type safety

### Styling & UI
- **TailwindCSS 3.4** - Utility-first CSS
- **shadcn/ui** - Pre-built accessible components
- **Lucide React** - Icon library
- **Tailwind Forms** - Form styling plugin
- **Tailwind Typography** - Content styling

### State & Forms
- **Zustand** - Lightweight state management
- **React Hook Form** - Form handling
- **Zod** - Schema validation

### Data Fetching
- **TanStack Query (React Query)** - Server state management
- **Axios** - HTTP client

### Development
- **ESLint** - Code linting
- **Prettier** - Code formatting
- **TypeScript ESLint** - TypeScript linting

---

## 🎨 Color Scheme

### Primary Colors

```typescript
// Blue (Primary)
primary: {
  50: '#eff6ff',   // Very light blue backgrounds
  100: '#dbeafe',  // Light blue accents
  200: '#bfdbfe',  // Soft blue
  300: '#93c5fd',  // Medium light blue
  400: '#60a5fa',  // Bright blue
  500: '#3b82f6',  // Primary blue (main brand color)
  600: '#2563eb',  // Darker blue (hover states)
  700: '#1d4ed8',  // Deep blue
  800: '#1e40af',  // Very dark blue
  900: '#1e3a8a',  // Darkest blue
}

// Yellow (Accent)
accent: {
  50: '#fefce8',   // Very light yellow
  100: '#fef9c3',  // Light yellow
  200: '#fef08a',  // Soft yellow
  300: '#fde047',  // Medium yellow
  400: '#facc15',  // Bright yellow
  500: '#eab308',  // Primary yellow (main accent)
  600: '#ca8a04',  // Darker yellow
  700: '#a16207',  // Deep yellow
  800: '#854d0e',  // Very dark yellow
  900: '#713f12',  // Darkest yellow
}

// Red (Alert/Error)
danger: {
  50: '#fef2f2',   // Very light red
  100: '#fee2e2',  // Light red
  200: '#fecaca',  // Soft red
  300: '#fca5a5',  // Medium red
  400: '#f87171',  // Bright red
  500: '#ef4444',  // Primary red (errors/alerts)
  600: '#dc2626',  // Darker red
  700: '#b91c1c',  // Deep red
  800: '#991b1b',  // Very dark red
  900: '#7f1d1d',  // Darkest red
}
```

### Usage Guidelines

**Primary Blue:**
- Main CTAs (Sign Up, Create Store, Add Product)
- Navigation active states
- Links
- Primary buttons
- Progress indicators

**Yellow Accent:**
- Secondary CTAs
- Highlights
- Success states
- Premium features badge
- Special offers

**Red:**
- Error messages
- Delete actions
- Critical alerts
- Low stock indicators
- Urgent notifications

**Neutral Colors:**
- Text: `gray-900` (dark), `gray-600` (medium), `gray-400` (light)
- Backgrounds: `white`, `gray-50`, `gray-100`
- Borders: `gray-200`, `gray-300`

---

## 📱 Mobile-First Approach

### Design Principles

1. **Touch-Friendly Targets**
   - Minimum 44x44px for buttons
   - Adequate spacing between interactive elements
   - Easy-to-tap navigation

2. **Progressive Enhancement**
   - Build for mobile first (320px+)
   - Enhance for tablet (768px+)
   - Optimize for desktop (1024px+)

3. **Performance**
   - Lazy load images
   - Code splitting
   - Optimistic UI updates
   - Skeleton loaders

4. **Navigation**
   - Bottom navigation for mobile
   - Hamburger menu that's easy to reach
   - Sticky headers when scrolling

### Responsive Breakpoints

```typescript
// Tailwind default breakpoints
sm: '640px',   // Small devices (landscape phones)
md: '768px',   // Medium devices (tablets)
lg: '1024px',  // Large devices (desktops)
xl: '1280px',  // Extra large devices
2xl: '1536px', // 2X large devices
```

### Mobile-First Component Pattern

```tsx
// Always start with mobile styles
<div className="
  // Mobile (default)
  flex flex-col space-y-4 p-4
  
  // Tablet (md)
  md:flex-row md:space-y-0 md:space-x-6 md:p-6
  
  // Desktop (lg)
  lg:p-8 lg:max-w-6xl lg:mx-auto
">
  {/* Content */}
</div>
```

---

## 🚀 Project Setup

### 1. Create Next.js Project

```bash
npx create-next-app@latest agm-store-builder-frontend --typescript --tailwind --app --use-npm

cd agm-store-builder-frontend
```

### 2. Install Dependencies

```bash
# Core dependencies
npm install zustand @tanstack/react-query axios react-hook-form @hookform/resolvers zod

# UI components
npm install class-variance-authority clsx tailwind-merge
npm install lucide-react

# Date handling
npm install date-fns

# Development dependencies
npm install -D @types/node @types/react @types/react-dom
```

### 3. Initialize shadcn/ui

```bash
npx shadcn-ui@latest init
```

When prompted:
- Style: **Default**
- Base color: **Slate**
- CSS variables: **Yes**

### 4. Add shadcn/ui Components

```bash
# Install commonly used components
npx shadcn-ui@latest add button
npx shadcn-ui@latest add input
npx shadcn-ui@latest add card
npx shadcn-ui@latest add dialog
npx shadcn-ui@latest add form
npx shadcn-ui@latest add select
npx shadcn-ui@latest add toast
npx shadcn-ui@latest add dropdown-menu
npx shadcn-ui@latest add tabs
npx shadcn-ui@latest add table
npx shadcn-ui@latest add badge
npx shadcn-ui@latest add alert
npx shadcn-ui@latest add skeleton
npx shadcn-ui@latest add separator
npx shadcn-ui@latest add sheet
```

---

## ⚙️ Configuration Files

### package.json

```json
{
  "name": "agm-store-builder-frontend",
  "version": "1.0.0",
  "private": true,
  "scripts": {
    "dev": "next dev",
    "build": "next build",
    "start": "next start",
    "lint": "next lint",
    "type-check": "tsc --noEmit"
  },
  "dependencies": {
    "next": "14.2.0",
    "react": "^18.3.0",
    "react-dom": "^18.3.0",
    "@tanstack/react-query": "^5.28.0",
    "axios": "^1.6.8",
    "zustand": "^4.5.2",
    "react-hook-form": "^7.51.0",
    "@hookform/resolvers": "^3.3.4",
    "zod": "^3.22.4",
    "class-variance-authority": "^0.7.0",
    "clsx": "^2.1.0",
    "tailwind-merge": "^2.2.2",
    "lucide-react": "^0.363.0",
    "date-fns": "^3.6.0",
    "sharp": "^0.33.3"
  },
  "devDependencies": {
    "typescript": "^5.4.0",
    "@types/node": "^20.11.30",
    "@types/react": "^18.2.70",
    "@types/react-dom": "^18.2.22",
    "autoprefixer": "^10.4.19",
    "postcss": "^8.4.38",
    "tailwindcss": "^3.4.1",
    "eslint": "^8.57.0",
    "eslint-config-next": "14.2.0",
    "@tailwindcss/forms": "^0.5.7",
    "@tailwindcss/typography": "^0.5.10"
  }
}
```

### vercel.json

```json
{
  "buildCommand": "npm run build",
  "outputDirectory": ".next",
  "framework": "nextjs",
  "regions": ["iad1"],
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
        },
        {
          "key": "Referrer-Policy",
          "value": "strict-origin-when-cross-origin"
        },
        {
          "key": "Permissions-Policy",
          "value": "camera=(), microphone=(), geolocation=()"
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

### src/middleware.ts

```typescript
import { NextResponse } from 'next/server';
import type { NextRequest } from 'next/server';

export function middleware(request: NextRequest) {
  const hostname = request.headers.get('host') || '';
  const url = request.nextUrl;
  
  // Get subdomain
  const subdomain = hostname.split('.')[0];
  
  // Skip for main domain and www
  if (subdomain === 'agmshop' || subdomain === 'www' || !subdomain) {
    return NextResponse.next();
  }
  
  // Skip for Vercel preview deployments
  if (hostname.includes('vercel.app')) {
    return NextResponse.next();
  }
  
  // Rewrite subdomain requests to /store/[username]
  if (url.pathname === '/' || url.pathname.startsWith('/store')) {
    const storeUrl = new URL(`/store/${subdomain}${url.pathname === '/' ? '' : url.pathname}`, request.url);
    storeUrl.search = url.search;
    
    return NextResponse.rewrite(storeUrl);
  }
  
  // Handle product pages
  if (url.pathname.startsWith('/products/')) {
    const productUrl = new URL(`/store/${subdomain}${url.pathname}`, request.url);
    return NextResponse.rewrite(productUrl);
  }
  
  return NextResponse.next();
}

export const config = {
  matcher: [
    /*
     * Match all request paths except for the ones starting with:
     * - api (API routes)
     * - _next/static (static files)
     * - _next/image (image optimization files)
     * - favicon.ico (favicon file)
     * - public (public files)
     */
    '/((?!api|_next/static|_next/image|favicon.ico|public).*)',
  ],
};
```

### tailwind.config.ts

```typescript
import type { Config } from 'tailwindcss';

const config: Config = {
  darkMode: ['class'],
  content: [
    './src/pages/**/*.{js,ts,jsx,tsx,mdx}',
    './src/components/**/*.{js,ts,jsx,tsx,mdx}',
    './src/app/**/*.{js,ts,jsx,tsx,mdx}',
  ],
  theme: {
    container: {
      center: true,
      padding: '2rem',
      screens: {
        '2xl': '1400px',
      },
    },
    extend: {
      colors: {
        border: 'hsl(var(--border))',
        input: 'hsl(var(--input))',
        ring: 'hsl(var(--ring))',
        background: 'hsl(var(--background))',
        foreground: 'hsl(var(--foreground))',
        primary: {
          DEFAULT: '#3b82f6', // Blue 500
          50: '#eff6ff',
          100: '#dbeafe',
          200: '#bfdbfe',
          300: '#93c5fd',
          400: '#60a5fa',
          500: '#3b82f6',
          600: '#2563eb',
          700: '#1d4ed8',
          800: '#1e40af',
          900: '#1e3a8a',
          foreground: '#ffffff',
        },
        accent: {
          DEFAULT: '#eab308', // Yellow 500
          50: '#fefce8',
          100: '#fef9c3',
          200: '#fef08a',
          300: '#fde047',
          400: '#facc15',
          500: '#eab308',
          600: '#ca8a04',
          700: '#a16207',
          800: '#854d0e',
          900: '#713f12',
          foreground: '#1e3a8a',
        },
        danger: {
          DEFAULT: '#ef4444', // Red 500
          50: '#fef2f2',
          100: '#fee2e2',
          200: '#fecaca',
          300: '#fca5a5',
          400: '#f87171',
          500: '#ef4444',
          600: '#dc2626',
          700: '#b91c1c',
          800: '#991b1b',
          900: '#7f1d1d',
          foreground: '#ffffff',
        },
        secondary: {
          DEFAULT: 'hsl(var(--secondary))',
          foreground: 'hsl(var(--secondary-foreground))',
        },
        destructive: {
          DEFAULT: '#ef4444',
          foreground: '#ffffff',
        },
        muted: {
          DEFAULT: 'hsl(var(--muted))',
          foreground: 'hsl(var(--muted-foreground))',
        },
        card: {
          DEFAULT: 'hsl(var(--card))',
          foreground: 'hsl(var(--card-foreground))',
        },
        popover: {
          DEFAULT: 'hsl(var(--popover))',
          foreground: 'hsl(var(--popover-foreground))',
        },
      },
      borderRadius: {
        lg: 'var(--radius)',
        md: 'calc(var(--radius) - 2px)',
        sm: 'calc(var(--radius) - 4px)',
      },
      fontFamily: {
        sans: ['var(--font-sans)', 'system-ui', 'sans-serif'],
      },
      keyframes: {
        'accordion-down': {
          from: { height: '0' },
          to: { height: 'var(--radix-accordion-content-height)' },
        },
        'accordion-up': {
          from: { height: 'var(--radix-accordion-content-height)' },
          to: { height: '0' },
        },
      },
      animation: {
        'accordion-down': 'accordion-down 0.2s ease-out',
        'accordion-up': 'accordion-up 0.2s ease-out',
      },
    },
  },
  plugins: [
    require('tailwindcss-animate'),
    require('@tailwindcss/forms'),
    require('@tailwindcss/typography'),
  ],
};

export default config;
```

### next.config.js

```javascript
/** @type {import('next').NextConfig} */
const nextConfig = {
  images: {
    remotePatterns: [
      {
        protocol: 'https',
        hostname: 'agm-store-uploads.s3.amazonaws.com',
      },
      {
        protocol: 'https',
        hostname: 'res.cloudinary.com',
      },
    ],
    formats: ['image/avif', 'image/webp'],
  },
  async rewrites() {
    return [
      {
        source: '/api/:path*',
        destination: process.env.NEXT_PUBLIC_API_URL + '/:path*',
      },
    ];
  },
  async headers() {
    return [
      {
        source: '/:path*',
        headers: [
          {
            key: 'X-DNS-Prefetch-Control',
            value: 'on',
          },
          {
            key: 'Strict-Transport-Security',
            value: 'max-age=63072000; includeSubDomains; preload',
          },
        ],
      },
    ];
  },
  // Enable React strict mode
  reactStrictMode: true,
  
  // Optimize production builds
  swcMinify: true,
  
  // Configure environment variables
  env: {
    NEXT_PUBLIC_APP_NAME: 'AGM Store Builder',
  },
};

module.exports = nextConfig;
```

### components.json

```json
{
  "$schema": "https://ui.shadcn.com/schema.json",
  "style": "default",
  "rsc": true,
  "tsx": true,
  "tailwind": {
    "config": "tailwind.config.ts",
    "css": "src/app/globals.css",
    "baseColor": "slate",
    "cssVariables": true,
    "prefix": ""
  },
  "aliases": {
    "components": "@/components",
    "utils": "@/lib/utils",
    "ui": "@/components/ui",
    "lib": "@/lib",
    "hooks": "@/hooks"
  }
}
```

### .env.example

```env
# Application
NEXT_PUBLIC_APP_NAME="AGM Store Builder"
NEXT_PUBLIC_APP_URL=http://localhost:3000
NEXT_PUBLIC_API_URL=http://localhost:4000/api

# Analytics (Optional)
NEXT_PUBLIC_POSTHOG_KEY=
NEXT_PUBLIC_POSTHOG_HOST=https://app.posthog.com

# Error Tracking (Optional)
NEXT_PUBLIC_SENTRY_DSN=

# Feature Flags
NEXT_PUBLIC_ENABLE_PREMIUM_FEATURES=false
```

### README.md (Frontend)

```markdown
# AGM Store Builder - Frontend

> Next.js 14 frontend for AGM Store Builder with mobile-first design

## Tech Stack

- **Framework:** Next.js 14 (App Router)
- **Styling:** TailwindCSS 3.4
- **UI Components:** shadcn/ui
- **Icons:** Lucide React
- **State Management:** Zustand
- **Forms:** React Hook Form + Zod
- **Data Fetching:** TanStack Query (React Query)

## Color Scheme

- **Primary:** Blue (#3b82f6)
- **Accent:** Yellow (#eab308)
- **Danger:** Red (#ef4444)

## Getting Started

### Prerequisites

- Node.js 18+
- npm or yarn

### Installation

1. Clone the repository
```bash
git clone https://github.com/thetruesammyjay/agm-store-builder.git
cd agm-store-builder/frontend
```

2. Install dependencies
```bash
npm install
```

3. Set up environment variables
```bash
cp .env.example .env.local
# Edit .env.local with your API URL
```

4. Run development server
```bash
npm run dev
```

Open [http://localhost:3000](http://localhost:3000)

### Build for Production

```bash
npm run build
npm start
```

## Project Structure

```
src/
├── app/                  # Next.js App Router pages
├── components/           # React components
│   ├── ui/              # shadcn/ui components
│   ├── auth/            # Authentication components
│   ├── dashboard/       # Dashboard components
│   ├── store/           # Store components
│   └── shared/          # Shared components
├── lib/                 # Utility functions
├── hooks/               # Custom React hooks
├── store/               # Zustand state management
├── types/               # TypeScript types
└── middleware.ts        # Next.js middleware (subdomain routing)
```

## Key Features

- 📱 Mobile-first responsive design
- 🎨 Blue, Yellow, Red color scheme
- 🔐 JWT authentication
- 🏪 Dynamic subdomain routing
- 📦 Product management
- 🛒 Shopping cart
- 💳 Payment integration
- 📊 Analytics dashboard

## Deployment

### Vercel (Recommended)

1. Push code to GitHub
2. Import project in Vercel
3. Configure environment variables
4. Deploy

### Manual Deployment

```bash
npm run build
npm start
```

## Contributing

1. Fork the repository
2. Create feature branch
3. Commit changes
4. Push to branch
5. Open Pull Request

## License

MIT License
```

---

## 🧩 Key Components to Build

### 1. Authentication Components

**LoginForm.tsx**
```tsx
'use client';

import { useForm } from 'react-hook-form';
import { zodResolver } from '@hookform/resolvers/zod';
import { z } from 'zod';
import { Button } from '@/components/ui/button';
import { Input } from '@/components/ui/input';
import { Form, FormControl, FormField, FormItem, FormLabel, FormMessage } from '@/components/ui/form';
import { Mail, Lock } from 'lucide-react';

const loginSchema = z.object({
  email: z.string().email('Invalid email address'),
  password: z.string().min(8, 'Password must be at least 8 characters'),
});

type LoginFormData = z.infer<typeof loginSchema>;

export function LoginForm() {
  const form = useForm<LoginFormData>({
    resolver: zodResolver(loginSchema),
    defaultValues: {
      email: '',
      password: '',
    },
  });

  const onSubmit = async (data: LoginFormData) => {
    // API call handled in API_ENDPOINTS.md
    console.log(data);
  };

  return (
    <Form {...form}>
      <form onSubmit={form.handleSubmit(onSubmit)} className="space-y-4">
        <FormField
          control={form.control}
          name="email"
          render={({ field }) => (
            <FormItem>
              <FormLabel>Email</FormLabel>
              <FormControl>
                <div className="relative">
                  <Mail className="absolute left-3 top-1/2 -translate-y-1/2 h-5 w-5 text-gray-400" />
                  <Input
                    type="email"
                    placeholder="you@example.com"
                    className="pl-10"
                    {...field}
                  />
                </div>
              </FormControl>
              <FormMessage />
            </FormItem>
          )}
        />

        <FormField
          control={form.control}
          name="password"
          render={({ field }) => (
            <FormItem>
              <FormLabel>Password</FormLabel>
              <FormControl>
                <div className="relative">
                  <Lock className="absolute left-3 top-1/2 -translate-y-1/2 h-5 w-5 text-gray-400" />
                  <Input
                    type="password"
                    placeholder="••••••••"
                    className="pl-10"
                    {...field}
                  />
                </div>
              </FormControl>
              <FormMessage />
            </FormItem>
          )}
        />

        <Button
          type="submit"
          className="w-full bg-primary-500 hover:bg-primary-600"
          disabled={form.formState.isSubmitting}
        >
          {form.formState.isSubmitting ? 'Logging in...' : 'Log In'}
        </Button>
      </form>
    </Form>
  );
}
```

### 2. Product Card (Mobile-Optimized)

**ProductCard.tsx**
```tsx
import Image from 'next/image';
import { Card, CardContent } from '@/components/ui/card';
import { Button } from '@/components/ui/button';
import { Badge } from '@/components/ui/badge';
import { ShoppingCart, Heart } from 'lucide-react';

interface Product {
  id: string;
  name: string;
  description: string;
  price: number;
  compareAtPrice?: number;
  images: string[];
  stockQuantity: number;
}

interface ProductCardProps {
  product: Product;
  onAddToCart: (product: Product) => void;
}

export function ProductCard({ product, onAddToCart }: ProductCardProps) {
  const discountPercentage = product.compareAtPrice
    ? Math.round(((product.compareAtPrice - product.price) / product.compareAtPrice) * 100)
    : 0;

  return (
    <Card className="overflow-hidden hover:shadow-lg transition-shadow">
      {/* Image */}
      <div className="relative aspect-square">
        <Image
          src={product.images[0] || '/placeholder.jpg'}
          alt={product.name}
          fill
          className="object-cover"
          sizes="(max-width: 768px) 50vw, (max-width: 1024px) 33vw, 25vw"
        />
        
        {/* Discount Badge */}
        {discountPercentage > 0 && (
          <Badge className="absolute top-2 right-2 bg-danger-500 text-white">
            -{discountPercentage}%
          </Badge>
        )}
        
        {/* Low Stock Warning */}
        {product.stockQuantity < 5 && product.stockQuantity > 0 && (
          <Badge className="absolute top-2 left-2 bg-accent-500 text-accent-900">
            Only {product.stockQuantity} left
          </Badge>
        )}
        
        {/* Wishlist Button */}
        <Button
          size="icon"
          variant="ghost"
          className="absolute top-2 right-2 bg-white/80 hover:bg-white"
        >
          <Heart className="h-5 w-5" />
        </Button>
      </div>

      <CardContent className="p-4">
        {/* Product Name */}
        <h3 className="font-semibold text-lg mb-2 line-clamp-2 min-h-[3.5rem]">
          {product.name}
        </h3>

        {/* Price */}
        <div className="flex items-center gap-2 mb-3">
          <span className="text-2xl font-bold text-primary-600">
            ₦{product.price.toLocaleString()}
          </span>
          {product.compareAtPrice && (
            <span className="text-sm text-gray-500 line-through">
              ₦{product.compareAtPrice.toLocaleString()}
            </span>
          )}
        </div>

        {/* Add to Cart Button */}
        <Button
          onClick={() => onAddToCart(product)}
          className="w-full bg-primary-500 hover:bg-primary-600"
          disabled={product.stockQuantity === 0}
        >
          <ShoppingCart className="h-4 w-4 mr-2" />
          {product.stockQuantity === 0 ? 'Out of Stock' : 'Add to Cart'}
        </Button>
      </CardContent>
    </Card>
  );
}
```

### 3. Mobile Navigation

**MobileNav.tsx**
```tsx
'use client';

import { useState } from 'react';
import Link from 'next/link';
import { Sheet, SheetContent, SheetTrigger } from '@/components/ui/sheet';
import { Button } from '@/components/ui/button';
import { Menu, Home, ShoppingBag, User, Settings } from 'lucide-react';

export function MobileNav() {
  const [open, setOpen] = useState(false);

  const navItems = [
    { href: '/', label: 'Home', icon: Home },
    { href: '/dashboard/products', label: 'Products', icon: ShoppingBag },
    { href: '/dashboard/settings', label: 'Settings', icon: Settings },
    { href: '/dashboard/settings-profile', label: 'Profile', icon: User },
  ];

  return (
    <Sheet open={open} onOpenChange={setOpen}>
      <SheetTrigger asChild>
        <Button variant="ghost" size="icon" className="md:hidden">
          <Menu className="h-6 w-6" />
        </Button>
      </SheetTrigger>
      
      <SheetContent side="left" className="w-[280px] sm:w-[320px]">
        <nav className="flex flex-col space-y-4 mt-8">
          {navItems.map((item) => (
            <Link
              key={item.href}
              href={item.href}
              onClick={() => setOpen(false)}
              className="flex items-center space-x-3 px-4 py-3 rounded-lg hover:bg-gray-100 transition-colors"
            >
              <item.icon className="h-5 w-5 text-gray-600" />
              <span className="font-medium">{item.label}</span>
            </Link>
          ))}
        </nav>
      </SheetContent>
    </Sheet>
  );
}
```

---

## 🗂 Routing Structure

```
app/
├── (marketing)/
│   ├── layout.tsx
│   ├── page.tsx              # Landing page
│   ├── about/page.tsx
│   ├── services/page.tsx
│   ├── pricing/page.tsx
│   └── contact/page.tsx
│
├── (auth)/
│   ├── layout.tsx
│   ├── login/page.tsx
│   ├── register/page.tsx
│   └── verify/page.tsx
│
├── (dashboard)/
│   ├── layout.tsx            # Dashboard layout with sidebar
│   ├── dashboard/page.tsx    # Analytics
│   ├── products/
│   │   ├── page.tsx
│   │   ├── new/page.tsx
│   │   └── [id]/edit/page.tsx
│   ├── orders/
│   │   ├── page.tsx
│   │   └── [id]/page.tsx
│   └── settings/
│       ├── page.tsx
│       ├── store/page.tsx
│       └── payment/page.tsx
│
├── onboarding/
│   ├── layout.tsx
│   ├── step-1-name/page.tsx
│   ├── step-2-template/page.tsx
│   ├── step-3-customize/page.tsx
│   ├── step-4-products/page.tsx
│   └── step-5-payment/page.tsx
│
└── store/[username]/
    ├── page.tsx              # Store homepage
    ├── products/[id]/page.tsx
    ├── checkout/page.tsx
    └── track/[orderNumber]/page.tsx
```

---

## 🗄 State Management

### Zustand Stores

**authStore.ts**
```typescript
import { create } from 'zustand';
import { persist } from 'zustand/middleware';

interface User {
  id: string;
  email: string;
  fullName: string;
}

interface AuthState {
  user: User | null;
  token: string | null;
  isAuthenticated: boolean;
  login: (user: User, token: string) => void;
  logout: () => void;
  updateUser: (user: Partial<User>) => void;
}

export const useAuthStore = create<AuthState>()(
  persist(
    (set) => ({
      user: null,
      token: null,
      isAuthenticated: false,
      login: (user, token) => set({ user, token, isAuthenticated: true }),
      logout: () => set({ user: null, token: null, isAuthenticated: false }),
      updateUser: (userData) =>
        set((state) => ({
          user: state.user ? { ...state.user, ...userData } : null,
        })),
    }),
    {
      name: 'auth-storage',
    }
  )
);
```

**cartStore.ts**
```typescript
import { create } from 'zustand';
import { persist } from 'zustand/middleware';

interface CartItem {
  id: string;
  name: string;
  price: number;
  quantity: number;
  image: string;
}

interface CartState {
  items: CartItem[];
  addItem: (item: CartItem) => void;
  removeItem: (id: string) => void;
  updateQuantity: (id: string, quantity: number) => void;
  clearCart: () => void;
  total: () => number;
}

export const useCartStore = create<CartState>()(
  persist(
    (set, get) => ({
      items: [],
      addItem: (item) =>
        set((state) => {
          const existingItem = state.items.find((i) => i.id === item.id);
          if (existingItem) {
            return {
              items: state.items.map((i) =>
                i.id === item.id ? { ...i, quantity: i.quantity + 1 } : i
              ),
            };
          }
          return { items: [...state.items, { ...item, quantity: 1 }] };
        }),
      removeItem: (id) =>
        set((state) => ({
          items: state.items.filter((i) => i.id !== id),
        })),
      updateQuantity: (id, quantity) =>
        set((state) => ({
          items: state.items.map((i) =>
            i.id === id ? { ...i, quantity } : i
          ),
        })),
      clearCart: () => set({ items: [] }),
      total: () =>
        get().items.reduce((sum, item) => sum + item.price * item.quantity, 0),
    }),
    {
      name: 'cart-storage',
    }
  )
);
```

---

## 📝 Form Handling

### Example: Product Form

```tsx
'use client';

import { useForm } from 'react-hook-form';
import { zodResolver } from '@hookform/resolvers/zod';
import { z } from 'zod';

const productSchema = z.object({
  name: z.string().min(3, 'Name must be at least 3 characters'),
  description: z.string().optional(),
  price: z.number().min(1, 'Price must be greater than 0'),
  compareAtPrice: z.number().optional(),
  stockQuantity: z.number().min(0, 'Stock cannot be negative'),
  images: z.array(z.string()).min(1, 'At least one image is required'),
});

type ProductFormData = z.infer<typeof productSchema>;

export function ProductForm() {
  const form = useForm<ProductFormData>({
    resolver: zodResolver(productSchema),
  });

  const onSubmit = async (data: ProductFormData) => {
    // API call
  };

  return (
    <Form {...form}>
      <form onSubmit={form.handleSubmit(onSubmit)}>
        {/* Form fields */}
      </form>
    </Form>
  );
}
```

---

## 🔌 API Integration

### API Client Setup

**lib/api.ts**
```typescript
import axios from 'axios';
import { useAuthStore } from '@/store/authStore';

const api = axios.create({
  baseURL: process.env.NEXT_PUBLIC_API_URL,
  headers: {
    'Content-Type': 'application/json',
  },
});

// Request interceptor
api.interceptors.request.use((config) => {
  const token = useAuthStore.getState().token;
  if (token) {
    config.headers.Authorization = `Bearer ${token}`;
  }
  return config;
});

// Response interceptor
api.interceptors.response.use(
  (response) => response,
  (error) => {
    if (error.response?.status === 401) {
      useAuthStore.getState().logout();
      window.location.href = '/login';
    }
    return Promise.reject(error);
  }
);

export default api;
```

### React Query Setup

**app/providers.tsx**
```tsx
'use client';

import { QueryClient, QueryClientProvider } from '@tanstack/react-query';
import { useState } from 'react';

export function Providers({ children }: { children: React.ReactNode }) {
  const [queryClient] = useState(
    () =>
      new QueryClient({
        defaultOptions: {
          queries: {
            staleTime: 60 * 1000, // 1 minute
            retry: 1,
          },
        },
      })
  );

  return (
    <QueryClientProvider client={queryClient}>
      {children}
    </QueryClientProvider>
  );
}
```

---

## 🚀 Deployment

### Vercel Deployment Steps

1. **Push to GitHub**
```bash
git add .
git commit -m "Initial commit"
git push origin main
```

2. **Import in Vercel**
   - Go to vercel.com
   - Click "New Project"
   - Import your GitHub repository
   - Configure settings:
     - Framework: Next.js
     - Root Directory: `./frontend` (if in monorepo)
     - Build Command: `npm run build`
     - Output Directory: `.next`

3. **Set Environment Variables**
   - `NEXT_PUBLIC_API_URL`: Your backend API URL
   - `NEXT_PUBLIC_APP_URL`: Your frontend URL

4. **Configure Custom Domain**
   - Add `agmshop.com` and `*.agmshop.com`
   - Update DNS records in Cloudflare:
     ```
     A     @              76.76.21.21
     CNAME *              cname.vercel-dns.com
     ```

5. **Deploy**
   - Click "Deploy"
   - Wait for build to complete
   - Your site is live!

---

## ✅ Development Checklist

### Setup Phase
- [ ] Create Next.js project
- [ ] Install all dependencies
- [ ] Configure Tailwind with custom colors
- [ ] Set up shadcn/ui
- [ ] Create `.env.local`
- [ ] Configure middleware for subdomain routing

### Component Development
- [ ] Build authentication forms
- [ ] Create product card (mobile-optimized)
- [ ] Build shopping cart
- [ ] Create dashboard layout
- [ ] Build onboarding wizard
- [ ] Create store layout

### State & Data
- [ ] Set up Zustand stores
- [ ] Configure React Query
- [ ] Implement API client
- [ ] Add error handling
- [ ] Add loading states

### Testing
- [ ] Test on mobile devices
- [ ] Test subdomain routing
- [ ] Test authentication flow
- [ ] Test checkout process
- [ ] Test responsive design

### Deployment
- [ ] Push to GitHub
- [ ] Deploy to Vercel
- [ ] Configure environment variables
- [ ] Set up custom domain
- [ ] Test production build

---

**Ready to build! See API_ENDPOINTS.md for backend integration details.**

**Repository:** https://github.com/thetruesammyjay/agm-store-builder.git
