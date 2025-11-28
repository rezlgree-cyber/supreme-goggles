# WeebCentral Scraper API

A REST API for scraping anime data from WeebCentral.com, ready to deploy on Render.

## Features

- Scrape anime lists with pagination
- Get detailed anime information
- Fetch anime recommendations
- Search functionality
- CORS enabled
- Error handling and timeouts

## Local Development

1. Install dependencies:
\`\`\`bash
npm install
\`\`\`

2. Start the development server:
\`\`\`bash
npm run dev
\`\`\`

The API will be available at `http://localhost:3000`

## Deployment to Render

### Step 1: Push to GitHub
- Create a GitHub repository
- Push your code:
\`\`\`bash
git add .
git commit -m "Initial commit: WeebCentral Scraper API"
git push origin main
\`\`\`

### Step 2: Connect to Render
1. Go to https://render.com
2. Click "New +" and select "Web Service"
3. Connect your GitHub repository
4. Configure:
   - **Name:** weebcentral-scraper-api
   - **Runtime:** Node
   - **Build Command:** `npm install`
   - **Start Command:** `npm start`
   - **Instance Type:** Free or Starter

### Step 3: Deploy
- Click "Create Web Service"
- Render will automatically deploy your API
- Your API will be available at: `https://your-app-name.onrender.com`

## API Endpoints

### Health Check
\`\`\`
GET /health
\`\`\`
Returns server status.

### Get Anime List
\`\`\`
GET /api/anime?page=1&search=query
\`\`\`
Parameters:
- `page` (optional): Page number (default: 1)
- `search` (optional): Search query

### Get Anime Details
\`\`\`
GET /api/anime/:id
\`\`\`
Parameters:
- `id`: Anime ID

### Get Recommendations
\`\`\`
GET /api/recommendations
\`\`\`
Fetches recommended anime.

## Example Requests

\`\`\`bash
# Get first page of anime
curl https://your-app.onrender.com/api/anime

# Search for anime
curl https://your-app.onrender.com/api/anime?search=naruto

# Get specific anime details
curl https://your-app.onrender.com/api/anime/123

# Get recommendations
curl https://your-app.onrender.com/api/recommendations
\`\`\`

## Selector Customization

The scrapers use flexible CSS selectors that should work with most anime websites. If weebcentral.com's structure changes:

1. Edit `src/scrapers/animeScrapers.js`
2. Update the selectors to match the current HTML structure
3. Test with local development
4. Commit and push changes

## Error Handling

The API includes:
- Try-catch blocks for network errors
- Timeout protection (10 seconds)
- User-Agent spoofing to avoid blocking
- CORS support for cross-origin requests

## Notes

- Always respect the website's `robots.txt` and Terms of Service
- Add delays if scraping large amounts of data
- Consider implementing caching for repeated requests
- Monitor for website structure changes that might break selectors

## Free Tier Limitations (Render)

- 0.5 GB RAM
- 0.5 CPU
- Spins down after 15 minutes of inactivity
- Perfect for development and light usage

## License

MIT
