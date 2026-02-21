# Portfolio Website - AWS S3 + CloudFront

## Project Overview
A professional portfolio website hosted on AWS S3 with CloudFront CDN distribution, demonstrating cloud storage, content delivery, and security best practices at the Cloud Practitioner level.

## Problem Solved
Need a fast, scalable, and cost-effective way to host a personal portfolio website without managing servers or infrastructure.

## Architecture

### AWS Services Used
- **Amazon S3:** Static website hosting and file storage
- **CloudFront:** Global Content Delivery Network (CDN)
- **Bucket Policy:** Security and access control

### How It Works

```
Website Visitor
    ↓
CloudFront Edge Location (nearest to visitor)
    ↓
CloudFront Cache
    ↓
S3 Bucket (if not cached)
```

**Flow:**
1. Visitor requests portfolio via CloudFront domain
2. CloudFront serves from nearest edge location (fast!)
3. If cached, serves immediately
4. If not cached, fetches from S3 bucket
5. Response is cached for future requests

## Design Decisions

### Why S3 for Storage?
- Designed for static content (HTML, CSS, images)
- Highly available and durable
- Extremely cheap
- Built-in website hosting capability
- No servers to manage

### Why CloudFront CDN?
- **Global reach:** Edge locations in 400+ cities worldwide
- **Performance:** Users get content from nearest location
- **Security:** Built-in DDoS protection
- **Caching:** Reduces load on origin (S3)
- **Cost:** Data transfer from S3 to CloudFront is free
- **HTTPS:** Automatic SSL/TLS certificates

### S3 Bucket Policy
Bucket policy allows public read access to portfolio.html while maintaining security:
- Only allows GET requests (read-only)
- Blocks PUT, DELETE, and other dangerous operations
- Prevents accidental or malicious modifications

## Technologies
- **AWS Services:** S3, CloudFront
- **Frontend:** HTML5, CSS3
- **Hosting:** Serverless (no servers, no infrastructure to manage)

## Performance Features
- **Global CDN:** Content cached at 400+ edge locations
- **Automatic compression:** CloudFront compresses files
- **HTTP/2 support:** Faster protocol for web delivery
- **IPv6:** Modern protocol support
- **HTTPS by default:** Secure connections

## Security Features
- **S3 bucket policy:** Least-privilege access
- **Public read-only:** Only allows viewing, not modifying
- **HTTPS enforced:** All traffic encrypted
- **DDoS protection:** CloudFront includes AWS Shield Standard
- **No servers to patch:** Fully managed service

## Cost Analysis

### Monthly Cost Breakdown
- **S3 Storage:** ~$0.02-0.05 (minimal)
- **CloudFront data transfer:** $0 (free tier: 1GB/month)
- **Requests:** $0 (within free tier)
- **Total:** $0-0.10/month

### Why This is Cost-Effective
- Free tier: 1GB data transfer + 1M requests/month
- No compute costs (no EC2, no servers)
- No database costs
- Storage costs negligible (~1-10MB for portfolio)
- Scales automatically (no capacity planning)

## How to Recreate This Project

### Prerequisites
- AWS Account (free tier eligible)
- HTML/CSS portfolio file
- AWS Console access

### Step-by-Step Setup

#### 1. Create S3 Bucket
- S3 Dashboard → Create Bucket
- Bucket name: `[your-name]-portfolio` (globally unique)
- Region: us-east-1
- Uncheck "Block public access"
- Create

#### 2. Upload Portfolio File
- S3 bucket → Upload
- Select your portfolio.html file
- Upload

#### 3. Enable Static Website Hosting
- S3 bucket → Properties
- Static website hosting → Edit → Enable
- Index document: `aws-port.html` (or your filename)
- Error document: `aws-port.html`
- Save

#### 4. Create Bucket Policy
- S3 bucket → Permissions → Bucket policy
- Paste policy allowing public read access
- Replace bucket name with your actual bucket name

```json
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Sid": "PublicReadGetObject",
            "Effect": "Allow",
            "Principal": "*",
            "Action": "s3:GetObject",
            "Resource": "arn:aws:s3:::YOUR-BUCKET-NAME/*"
        }
    ]
}
```

#### 5. Create CloudFront Distribution
- CloudFront Dashboard → Create Distribution
- Origin domain: `your-bucket.s3-website-us-east-1.amazonaws.com`
- Distribution type: Single website or app
- Viewer protocol: Redirect HTTP to HTTPS
- Create distribution

#### 6. Wait & Test
- Wait 5-10 minutes for CloudFront deployment
- Copy CloudFront domain name
- Open in browser: `https://your-cloudfront-domain.cloudfront.net`
- Verify portfolio loads and looks correct

#### 7. (Optional) Custom Domain
- Point your domain's DNS to CloudFront
- CloudFront will provision SSL certificate
- Visit your custom domain

## Key Learnings

### Cloud Storage
- S3 is optimized for static content (HTML, CSS, images, PDFs)
- Not designed for database or dynamic content
- Extremely durable (99.999999999% durability)

### Content Delivery Networks (CDNs)
- Distribute content globally from edge locations
- Reduce latency for end users
- Improve website performance
- Provide DDoS protection

### Caching Strategies
- Edge locations cache content
- Reduces requests to origin
- Improves performance
- Reduces origin load

### Infrastructure as a Service (IaaS)
- S3 + CloudFront = fully managed infrastructure
- No servers to patch, monitor, or maintain
- Automatic scaling
- Pay only for what you use

### Security Best Practices
- Least-privilege access (bucket policy)
- Read-only public access
- HTTPS enforcement
- No direct access to origin

## Comparison: S3 + CloudFront vs. Traditional Hosting

| Feature | S3 + CloudFront | Traditional Server |
|---------|-----------------|-------------------|
| Cost | $0-1/month | $5-20/month |
| Scaling | Automatic | Manual |
| Maintenance | None | Patching, updates |
| Uptime | 99.99%+ | Depends |
| Global reach | Built-in CDN | Single location |
| Security | Managed by AWS | Your responsibility |
| Setup time | 10 minutes | Hours |

## Project Files
- `aws-port.html` - Portfolio website HTML
- `README.md` - This file
- `/screenshots` - Screenshots of AWS setup and live website

## Screenshots
- [S3 Bucket with portfolio file]
- [Static website hosting enabled]
- [CloudFront distribution]
- [Live portfolio website]

## Tear Down Instructions
To avoid AWS charges (though this project costs ~$0):

1. **CloudFront:** Distributions → Select → Disable → Delete (takes ~15 minutes)
2. **S3 Bucket:** Buckets → Select → Empty bucket → Delete bucket

**Expected cost after cleanup:** $0.00

## What Makes This CP-Level Knowledge
✅ Understanding of S3 for object storage  
✅ Knowledge of CloudFront and CDN concepts  
✅ Basic bucket policies and security  
✅ Static website hosting  
✅ Global content distribution  
✅ Cost optimization (serverless)  
✅ No-infrastructure-to-manage approach  

## Next Steps / Improvements
- Add custom domain with Route 53
- Implement SSL/TLS certificate
- Set up error page for 404s
- Add CloudWatch monitoring
- Implement cache invalidation for updates
- Add versioning to portfolio (v1, v2, etc.)
- Set up automated deployments with GitHub Actions

## Advantages Over Project 1
- **Different AWS services:** S3 + CloudFront vs. VPC + EC2 + RDS
- **Different paradigm:** Serverless vs. traditional servers
- **Different use case:** Static content vs. dynamic application
- **Shows versatility:** Can work with multiple AWS approaches
- **Simpler architecture:** Fewer components, easier to understand

---

**Portfolio hosted on AWS with zero infrastructure to manage!**
