# CurvyFitPT+ Email Templates - Implementation Guide

## Overview

This package includes three professional email templates designed for CurvyFitPT+:

1. **Welcome Email** - Sent when users sign up
2. **Weekly Inspiration** - Motivational content and challenges
3. **Fitness Tips & Tricks** - Educational content and pro tips

All templates feature:
- Dark red and black theme matching the app
- Mobile-responsive design
- Email-safe HTML/CSS (works in all major email clients)
- Social media links to Maggie's profiles
- Professional branding and layout

---

## Email Templates

### 1. Welcome Email (`email-welcome-template.html`)
**When to Send:** Immediately after user signs up

**Content Includes:**
- Warm welcome and thank you message
- Maggie's inspiring mantra
- Complete list of app features (6 main features)
- Next steps for getting started
- Call-to-action button to open the app
- Social media links

**Subject Line Suggestions:**
- "Welcome to CurvyFitPT+ - Your Journey Starts Now! 💪"
- "You're In! Let's Transform Together"
- "Welcome to the CurvyFitPT+ Family"

---

### 2. Weekly Inspiration Email (`email-inspiration-template.html`)
**When to Send:** Every Monday morning (7:00 AM user's timezone)

**Content Includes:**
- Motivational opening message
- Featured inspirational quote
- Weekly challenge with specific goals
- Mindset shift exercise
- Encouragement and support
- Call-to-action to track progress

**Subject Line Suggestions:**
- "Your Weekly Motivation: Keep Going 💪"
- "Monday Motivation: This Week's Challenge"
- "New Week, New Wins - Let's Do This!"

---

### 3. Fitness Tips & Tricks Email (`email-tips-template.html`)
**When to Send:** Every Thursday afternoon (2:00 PM user's timezone)

**Content Includes:**
- 5 actionable fitness tips
- Professional advice from Maggie's experience
- Pro tips for each recommendation
- Science-backed strategies
- Call-to-action to log workouts

**Subject Line Suggestions:**
- "5 Pro Tips to Level Up Your Fitness Game 🎯"
- "Trainer Secrets: What My Top Clients Do Differently"
- "Fitness Tips That Actually Work"

---

## How to Use These Templates

### Option 1: Email Service Providers (Recommended)

#### **Mailchimp**
1. Log into Mailchimp
2. Go to Campaigns → Create Campaign → Email
3. Choose "Paste in code" option
4. Copy the entire HTML from one of the template files
5. Paste it into the code editor
6. Customize merge tags (replace `{{FIRST_NAME}}` etc.)
7. Test send to yourself
8. Schedule or send immediately

**Merge Tags:**
- Replace static greetings with `*|FNAME|*` for first name
- Use `*|EMAIL|*` for email address

#### **SendGrid**
1. Log into SendGrid
2. Go to Marketing → Designs → Create Design
3. Select "Code Editor"
4. Paste the HTML template
5. Add personalization tags: `{{first_name}}`, `{{email}}`
6. Save as template
7. Use in campaigns or automated sequences

#### **ConvertKit**
1. Log into ConvertKit
2. Go to Broadcasts or Sequences
3. Create new email
4. Switch to HTML editor
5. Paste the template code
6. Use liquid tags for personalization: `{{ subscriber.first_name }}`
7. Save and schedule

#### **ActiveCampaign**
1. Log into ActiveCampaign
2. Go to Campaigns → Create Campaign
3. Choose "HTML Email"
4. Paste template code
5. Use personalization: `%FIRSTNAME%`, `%EMAIL%`
6. Test and send

---

### Option 2: Backend Integration (For Developers)

If you're building a custom backend for the app, here's how to integrate:

#### **Node.js with Nodemailer**

```javascript
const nodemailer = require('nodemailer');
const fs = require('fs');

// Configure your email service
const transporter = nodemailer.createTransport({
  service: 'gmail', // or 'sendgrid', 'mailgun', etc.
  auth: {
    user: 'your-email@gmail.com',
    pass: 'your-app-password'
  }
});

// Function to send welcome email
async function sendWelcomeEmail(userEmail, userName) {
  // Read the template file
  let htmlTemplate = fs.readFileSync('./email-welcome-template.html', 'utf8');
  
  // Replace placeholders (if you add them to the template)
  htmlTemplate = htmlTemplate.replace('{{USER_NAME}}', userName);
  
  const mailOptions = {
    from: 'CurvyFitPT+ <noreply@curvyfitpt.com>',
    to: userEmail,
    subject: 'Welcome to CurvyFitPT+ - Your Journey Starts Now! 💪',
    html: htmlTemplate
  };
  
  await transporter.sendMail(mailOptions);
  console.log(`Welcome email sent to ${userEmail}`);
}

// Usage
sendWelcomeEmail('user@example.com', 'Sarah');
```

#### **Python with Flask-Mail**

```python
from flask import Flask
from flask_mail import Mail, Message
import os

app = Flask(__name__)
app.config['MAIL_SERVER'] = 'smtp.gmail.com'
app.config['MAIL_PORT'] = 587
app.config['MAIL_USE_TLS'] = True
app.config['MAIL_USERNAME'] = 'your-email@gmail.com'
app.config['MAIL_PASSWORD'] = 'your-app-password'

mail = Mail(app)

def send_welcome_email(user_email, user_name):
    # Read template
    with open('email-welcome-template.html', 'r') as f:
        html_content = f.read()
    
    # Replace placeholders
    html_content = html_content.replace('{{USER_NAME}}', user_name)
    
    msg = Message(
        'Welcome to CurvyFitPT+ - Your Journey Starts Now! 💪',
        sender='CurvyFitPT+ <noreply@curvyfitpt.com>',
        recipients=[user_email],
        html=html_content
    )
    
    mail.send(msg)
    print(f'Welcome email sent to {user_email}')

# Usage
send_welcome_email('user@example.com', 'Sarah')
```

---

## Email Automation Workflows

### Suggested Email Sequence for New Users

**Day 0 (Signup):**
- Send: Welcome Email
- Purpose: Onboard user, explain features

**Day 3:**
- Send: Weekly Inspiration Email
- Purpose: Keep engagement high, provide motivation

**Day 7:**
- Send: Fitness Tips Email
- Purpose: Educate and provide value

**Day 10:**
- Send: Weekly Inspiration Email (different content)
- Purpose: Check-in, encourage consistency

**Day 14:**
- Send: Fitness Tips Email (different content)
- Purpose: Deepen knowledge

**Ongoing (After Day 14):**
- Monday: Weekly Inspiration (weekly)
- Thursday: Fitness Tips (weekly)

---

## Personalization Recommendations

### Add These Dynamic Fields:

1. **User's First Name** - Makes emails feel personal
2. **Days Since Signup** - Reference their journey
3. **Recent Activity** - "We saw you logged 3 workouts last week!"
4. **Calorie Streak** - "You've hit your target 5 days in a row!"
5. **Upcoming Milestones** - "You're 2 lbs away from your goal!"

### Example Personalized Opening:

```html
<p style="font-size: 16px; margin-bottom: 20px;">
    Hey {{FIRST_NAME}},
</p>

<p style="font-size: 16px; margin-bottom: 20px;">
    You've been crushing it for {{DAYS_ACTIVE}} days now—that's dedication! 
    I saw you logged {{WORKOUTS_THIS_WEEK}} workouts this week. Keep that momentum going!
</p>
```

---

## Best Practices

### Sending Times
- **Welcome Email:** Immediately after signup
- **Inspiration Emails:** Monday 7:00 AM (local time)
- **Tips Emails:** Thursday 2:00 PM (local time)

### Frequency
- **New Users:** 2-3 emails per week for first 2 weeks
- **Active Users:** 2 emails per week (Monday + Thursday)
- **Inactive Users (30+ days):** 1 re-engagement email per month

### A/B Testing
Test these elements:
- Subject lines (emoji vs. no emoji)
- Send times (morning vs. afternoon)
- CTA button text
- Email length (shorter vs. longer content)

### Compliance
- Always include unsubscribe link
- Honor unsubscribe requests within 24 hours
- Include physical mailing address (required by CAN-SPAM)
- Get explicit consent during signup

---

## Customization Guide

### Update Colors
Find and replace these hex codes in the templates:

- `#C41E3A` - Primary red
- `#8B0000` - Dark red
- `#FF4757` - Accent red
- `#0A0A0A` - Black background
- `#1A1A1A` - Dark gray
- `#2A2A2A` - Mid gray
- `#CCCCCC` - Text gray

### Update Social Links
Already configured in templates:
- YouTube: `https://www.youtube.com/@MaggieBermudez`
- Instagram: `https://www.instagram.com/maggie.a.bermudez/`
- TikTok: `https://www.tiktok.com/@maggie.a.bermudez`

### Update CTAs
Look for links with `href="#"` and replace with:
- App URL: Your app's web URL or deep link
- Social profiles: Already configured
- Unsubscribe: Link to your unsubscribe handler

---

## Testing Checklist

Before sending to your list, test:

✅ **Email Clients:**
- Gmail (desktop and mobile)
- Apple Mail (iOS)
- Outlook (desktop)
- Yahoo Mail
- Mobile preview

✅ **Functionality:**
- All links work
- Social media buttons link correctly
- Unsubscribe link works
- Images load (if using external images)
- Personalization tokens display correctly

✅ **Spam Testing:**
- Use tools like Mail-Tester.com
- Avoid spam trigger words in subject lines
- Ensure proper authentication (SPF, DKIM, DMARC)

---

## Metrics to Track

Monitor these KPIs:

1. **Open Rate** - Target: 25-35%
2. **Click-Through Rate** - Target: 3-8%
3. **Unsubscribe Rate** - Keep below 0.5%
4. **Bounce Rate** - Keep below 2%
5. **Conversion to App Open** - Custom tracking
6. **Engagement Time** - How long users read

---

## Future Template Ideas

Consider creating templates for:

- **Weekly Workout Spotlight** - Feature one workout with demo video
- **Meal Prep Sunday** - Weekly meal plan with shopping list
- **Success Story** - User transformation features
- **New Feature Announcement** - App updates
- **Special Challenges** - 30-day challenges, competitions
- **Holiday Specials** - Seasonal fitness tips
- **Re-engagement** - Win back inactive users

---

## Support & Questions

For questions about implementing these templates or customizing for your needs, consider:

1. Email service provider support documentation
2. Developer documentation for your email API
3. Testing tools like Litmus or Email on Acid
4. Email marketing communities and forums

---

**Version:** 1.0  
**Last Updated:** February 2026  
**Created by:** CurvyFitPT+ Team
