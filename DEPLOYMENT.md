# Deployment Guide

## Quick Deploy to Render

### Option 1: Using Render Dashboard (Recommended)

1. **Create GitHub Repository**
   \`\`\`bash
   git init
   git add .
   git commit -m "Initial commit"
   git push origin main
   \`\`\`

2. **Connect to Render**
   - Visit https://render.com
   - Sign up or log in
   - Click "New +" → "Web Service"
   - Select your GitHub repository

3. **Configure Settings**
   - Name: `weebcentral-scraper-api`
   - Environment: `Node`
   - Build Command: `npm install`
   - Start Command: `npm start`
   - Plan: Free (or higher for production)

4. **Deploy**
   - Click "Create Web Service"
   - Wait for deployment to complete
   - Your API is live!

### Option 2: Manual Push

\`\`\`bash
# Install Render CLI (optional)
npm install -g render

# Push to Render
render deploy
\`\`\`

### Option 3: Docker (Advanced)

Create a `Dockerfile`:

\`\`\`dockerfile
FROM node:18-alpine

WORKDIR /app
COPY package*.json ./
RUN npm install --production
COPY src ./src

EXPOSE 3000
CMD ["npm", "start"]
\`\`\`

Then push to Render as a Docker service.

## Environment Variables

Set these in Render dashboard under "Environment":

\`\`\`
PORT=3000
NODE_ENV=production
\`\`\`

## Monitoring

- Check logs: Render dashboard → Logs tab
- Monitor uptime: Render dashboard → Events tab
- API health: `GET /health`

## Troubleshooting

**API not responding:**
1. Check Render logs for errors
2. Verify free tier spin-down limits
3. Test locally first with `npm run dev`

**Scraper not working:**
1. Website structure may have changed
2. Update CSS selectors in `src/scrapers/animeScrapers.js`
3. Verify User-Agent headers are working

**Rate limiting:**
- Add delays between requests if needed
- Consider caching responses
- Respect website's terms of service

## Performance Tips

1. **Add Caching**
   \`\`\`js
   import NodeCache from 'node-cache';
   const cache = new NodeCache({ stdTTL: 600 });
   \`\`\`

2. **Add Rate Limiting**
   \`\`\`js
   import rateLimit from 'express-rate-limit';
   const limiter = rateLimit({ windowMs: 15 * 60 * 1000, max: 100 });
   app.use('/api/', limiter);
   \`\`\`

3. **Database Integration**
   - Store scraped data to avoid repeated scraping
   - Use PostgreSQL on Render

## Maintenance

- Monitor website changes to CSS selectors
- Update dependencies: `npm update`
- Test regularly with `npm run dev`
- Keep logs for debugging

## Need Help?

- Render Docs: https://render.com/docs
- Express Docs: https://expressjs.com
- Cheerio Docs: https://cheerio.js.org
