# Cloudflare Configuration Checklist — SMB Website

> Note: **Auto Minify was removed by Cloudflare on Aug 5, 2024.** Minify at build time (Vite/Laravel Mix handle this) and rely on Brotli instead.

## SSL/TLS
- [ ] Encryption mode → **Full (strict)**
- [ ] Always Use HTTPS → On
- [ ] Automatic HTTPS Rewrites → On
- [ ] TLS 1.3 → On
- [ ] HSTS → max-age ≥ 6 months *(only after HTTPS is confirmed working — bricks the domain if you regress)*

## DNS
- [ ] A/AAAA/CNAME records → Proxied (orange cloud)
- [ ] Zone status → Active

## Security / Bots
- [ ] Security Level → Medium
- [ ] Super Bot Fight Mode (Pro+) → Allow verified bots; don't broadly block "definitely automated"
- [ ] WAF custom rule (Pro+) → `(cf.client.bot)` → Skip remaining rules *(whitelists verified crawlers via CF's bot database)*

## robots.txt / Sitemap
- [ ] `robots.txt` at root with a `Sitemap:` line
- [ ] XML sitemap with `<loc>`, `<lastmod>` (ISO 8601); use a sitemap index if multiple
- [ ] Serve these from origin — ensure no cache/firewall rule blocks `/robots.txt` or `/sitemap.xml`

```
User-agent: *
Allow: /
Sitemap: https://yourdomain.com/sitemap.xml
```

## Caching
- [ ] Caching Level → Standard
- [ ] Browser Cache TTL → ≥ 4 hours
- [ ] Always Online → On
- [ ] Crawler Hints → On
- [ ] Tiered Cache → On *(free, reduces origin load)*

## Performance
- [ ] Brotli → On
- [ ] Early Hints → On
- [ ] HTTP/3 (QUIC) → On
- [ ] ~~Auto Minify~~ → removed; minify in build step
- [ ] Rocket Loader → Off unless static *(breaks JS-heavy sites)*
- [ ] APO → On only if WordPress

## SEO Hygiene
- [ ] Email Address Obfuscation → On
- [ ] Server-side Excludes → On
- [ ] Hotlink Protection → optional *(bandwidth only, no SEO impact)*

## Quick Reference

| Category | Setting | Recommendation |
|----------|---------|----------------|
| SSL/TLS | Encryption mode | Full (strict) |
| SSL/TLS | Always Use HTTPS | On |
| Security | Security Level | Medium |
| Security | Verified bots | Allow / don't block |
| DNS | Proxy status | Proxied (orange cloud) |
| Caching | Caching Level | Standard |
| Caching | Always Online | On |
| Caching | Crawler Hints | On |
| Speed | Brotli | On |
| Speed | Early Hints | On |
| Speed | HTTP/3 (QUIC) | On |
