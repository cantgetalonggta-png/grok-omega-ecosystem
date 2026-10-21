# Vercel Deployment Blueprint — GROK-OMEGA / OpenMontage Control Center

## Status (2026-10-21T22:54:38Z)
- **Team** `echo-ec69` (`team_kgQcPVmumwtmK3MdAGlxKJtg`)
- **Blocker**: API 403 — no permission to create projects on this team
- **Mitigation live**: raw.githack + jsDelivr hosting of `standalone.html`

## Recommended production path
1. Owner re-authenticates Vercel with project-create rights on the team  
2. Create empty project `openmontage-control-center`  
3. Connect GitHub `cantgetalonggta-png/openmontage-control-center`  
4. Framework preset: **Other** (static)  
5. Root directory: `/`  
6. Build command: none / `echo static`  
7. Output: `.`  
8. Production branch: `main`

## vercel.json (already in repo)
```json
{
  "version": 2,
  "cleanUrls": true,
  "rewrites": [{ "source": "/(.*)", "destination": "/index.html" }],
  "headers": [
    {
      "source": "/(.*)",
      "headers": [
        { "key": "Cache-Control", "value": "public, max-age=0, must-revalidate" },
        { "key": "X-Content-Type-Options", "value": "nosniff" }
      ]
    }
  ]
}

```

## CLI (when token has rights)
```bash
vercel --scope echo-ec69 link
vercel --scope echo-ec69 deploy --prod
```

## Health after deploy
- Open `/` → toast "Control Center ready"
- Click **Test all modules** → console PASS
- Click **Health Check** → ALL PASS
