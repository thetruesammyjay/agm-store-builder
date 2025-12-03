# Domain Routing

## URL

```bash
# Main site
https://shopwithagm.com → Normal homepage

# Store subdomain
https://teststore.shopwithagm.com → Store page for "teststore"
https://fashionstore.shopwithagm.com → Store page for "fashionstore"
```

## ⚙️ Vercel Configuration

Make sure your Vercel project has wildcard domain:

1. Go to Vercel Dashboard → Your Project → Settings → Domains
2. Add both:
   - `shopwithagm.com`
   - `*.shopwithagm.com` (wildcard for subdomains)

## 🔗 DNS Setup (Cloudflare)
```
A     @              76.76.21.21
CNAME *              cname.vercel-dns.com
CNAME www            cname.vercel-dns.com
```
