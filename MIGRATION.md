# Migration from Vercel to Netlify

## Summary
This project has been migrated from Vercel to Netlify as the deployment platform.

## Changes Made

### 1. Configuration Files
- **Removed**: `vercel.json`
- **Added**: `netlify.toml` with equivalent routing and function configuration

### 2. Package Scripts
Updated `package.json` scripts:
- `npm run deploy` - now uses `netlify deploy --prod`
- `npm run dev` - now uses `netlify dev`

### 3. Documentation
Updated `README.md`:
- Production URL changed from `https://strategic-intel.vercel.app` to `https://strategic-intel.netlify.app`
- All API usage examples updated with new URL

### 4. Code Comments
Updated deployment platform references in:
- `api/index.js` - "Standalone Version for Netlify"
- `api/real-simple.js` - "Simplified version for Netlify deployment"

### 5. Git Ignore
Updated `.gitignore`:
- Changed `.vercel` to `.netlify`

## Netlify Configuration

The `netlify.toml` file configures:

### Functions
- Uses `api/` directory for serverless functions
- Node.js bundler: esbuild

### Redirects/Routes
All previous Vercel routes are preserved:
- `/evolved` → `evolved-strategic-osint` function
- `/real` → `real-breach-osint` function  
- `/generation3`, `/generation6`, `/generation9` → `index` function with query parameters

## Deployment Steps

### Prerequisites
1. Install Netlify CLI: `npm install -g netlify-cli`
2. Ensure all environment variables are configured in Netlify dashboard

### Deploy
1. Connect repository to Netlify
2. Netlify will automatically detect `netlify.toml`
3. Set environment variables in Netlify dashboard (see `.env.example`)
4. Deploy using: `npm run deploy`

### Development
Run locally with: `npm run dev`

## Environment Variables
Same environment variables are required as before:
- `HIBP_API_KEY`
- `DEHASHED_USERNAME`
- `DEHASHED_API_KEY`
- `LEAKOSINT_API_KEY`
- `SHODAN_API_KEY`
- `VT_API_KEY`
- `GITHUB_TOKEN`
- `CENSYS_API_KEY`
- `SPYSE_API_KEY`

Configure these in the Netlify dashboard under Site settings → Environment variables.

## API Compatibility
All API endpoints remain the same:
- `/real` - Real OSINT Analysis
- `/evolved` - Evolved Strategic OSINT
- `/generation3`, `/generation6`, `/generation9` - Generation-specific endpoints
- All API handlers use standard request/response objects

## Notes
- Netlify Functions are compatible with Vercel's serverless function format
- The `handler(req, res)` pattern works on both platforms
- No code changes were required in the API handlers themselves
- Only configuration and documentation were updated
