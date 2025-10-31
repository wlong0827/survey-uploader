# Deployment Guide

## Deploying to Vercel

Vercel is the recommended platform for deploying Next.js applications. It provides seamless integration, automatic HTTPS, and edge runtime support.

### Prerequisites

1. A [Vercel account](https://vercel.com/signup) (free tier is sufficient)
2. Your app should build successfully (`npm run build`)
3. Your OpenAI API credentials ready

### Step 1: Prepare Your Repository

Make sure your code is pushed to a Git repository (GitHub, GitLab, or Bitbucket):

```bash
git add .
git commit -m "Ready for deployment"
git push origin main
```

### Step 2: Deploy via Vercel Dashboard

1. Go to [vercel.com](https://vercel.com) and sign in
2. Click **"Add New Project"**
3. Import your Git repository
4. Vercel will auto-detect it's a Next.js project

### Step 3: Configure Environment Variables

In the Vercel project settings, add these environment variables:

#### Required Variables:

- **`OPENAI_API_KEY`** - Your OpenAI API key (server-side only)
  - Get it from: https://platform.openai.com/api-keys
  - **Important**: Must be from the same org & project as your Agent Builder workflow

- **`NEXT_PUBLIC_CHATKIT_WORKFLOW_ID`** - Your ChatKit workflow ID (public, client-side)
  - Format: `wf_...`
  - Get it from: https://platform.openai.com/agent-builder (after clicking "Publish")

#### Optional Variables:

- **`CHATKIT_API_BASE`** - Custom ChatKit API base URL (defaults to `https://api.openai.com`)

### Step 4: Configure Project Settings

- **Framework Preset**: Next.js (auto-detected)
- **Root Directory**: `./` (if your app is in the root)
- **Build Command**: `npm run build` (default)
- **Output Directory**: `.next` (default)
- **Install Command**: `npm install` (default)

### Step 5: Deploy

1. Click **"Deploy"**
2. Wait for the build to complete
3. Once deployed, Vercel will provide you with a URL like: `your-app-name.vercel.app`

### Step 6: Configure Domain Allowlist

**IMPORTANT**: Before your ChatKit app will work, you must add your domain to OpenAI's allowlist:

1. Go to [OpenAI Domain Allowlist](https://platform.openai.com/settings/organization/security/domain-allowlist)
2. Add your Vercel domain (e.g., `your-app-name.vercel.app`)
3. If you're using a custom domain, add that as well

### Step 7: Test Your Deployment

1. Visit your deployed URL
2. Test the chat interface
3. Check browser console for any errors (in development mode, errors will be logged)

### Using a Custom Domain

1. In Vercel project settings, go to **"Domains"**
2. Add your custom domain
3. Follow Vercel's DNS configuration instructions
4. Add the custom domain to OpenAI's domain allowlist

### Troubleshooting

#### Build Fails
- Check that all dependencies are in `package.json`
- Verify Node.js version compatibility (Next.js 15 requires Node 18.17+)

#### ChatKit Not Loading
- Verify `NEXT_PUBLIC_CHATKIT_WORKFLOW_ID` is set correctly
- Check that domain is in OpenAI's allowlist
- Verify `OPENAI_API_KEY` is from the correct organization

#### Environment Variables Not Working
- Ensure `NEXT_PUBLIC_*` variables are set for client-side access
- Server-side variables (without `NEXT_PUBLIC_`) are only available in API routes
- Redeploy after adding new environment variables

### Alternative: Deploy via Vercel CLI

If you prefer command-line deployment:

```bash
# Install Vercel CLI
npm i -g vercel

# Login to Vercel
vercel login

# Deploy
vercel

# For production deployment
vercel --prod
```

When prompted:
- Link to existing project or create new
- Add environment variables interactively or via Vercel dashboard later

## Alternative Deployment Platforms

While Vercel is recommended, you can also deploy to:

- **Netlify**: Good Next.js support, similar workflow
- **Railway**: Simple deployment with environment variable management
- **Fly.io**: Good for custom configurations
- **AWS Amplify**: If already using AWS infrastructure

For any of these alternatives, you'll still need to:
1. Set the same environment variables
2. Add your domain to OpenAI's allowlist
3. Configure the platform for Next.js 15

