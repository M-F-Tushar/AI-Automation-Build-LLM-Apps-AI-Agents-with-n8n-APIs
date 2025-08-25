# n8n Automation Course - Complete Structure Guide

## Section Overview: Getting Started with n8n

This section covers the foundational knowledge needed to begin working with n8n, from installation to creating your first automated workflows.

---

## 1. Installation & Setup

### 1.1 Prerequisites
- **Node.js**: Required for local installation
- **Optional**: Docker (alternative installation method)
- **Optional**: NVM for Windows (node version management)

### 1.2 Local Installation Process

#### Step 1: Install Node.js
1. Go to [nodejs.org](https://nodejs.org)
2. Download the latest LTS version
3. Run the installer and follow setup instructions

#### Step 2: Install NVM for Windows (Optional but Recommended)
1. Search "NVM for Windows" or visit the GitHub repository
2. Download `nvm-setup.zip`
3. Extract and run the installer
4. This allows switching between Node.js versions if needed

#### Step 3: Install n8n
1. Open Node.js Command Prompt
2. Run: `npm install -g n8n`
3. Wait for installation to complete (2-3 minutes)

#### Step 4: Start n8n
1. In command prompt, type: `n8n`
2. Open browser and go to: `http://localhost:5678`
3. Create account with email, name, and password

### 1.3 Mac Installation
1. Download Node.js from official website
2. Open Terminal (Applications > Utilities)
3. Install n8n: `sudo npm install -g n8n`
4. Start n8n: `sudo n8n start`
5. Access at: `http://localhost:5678`

---

## 2. Managing Node Versions & Updates

### 2.1 Troubleshooting Installation Issues
**Common problems:**
- Wrong Node.js version
- Insufficient admin privileges

**Solutions:**
- Use NVM to manage Node versions
- Ensure admin rights on your machine

### 2.2 Using NVM (Node Version Manager)
```bash
nvm list                    # See installed versions
nvm install 20.16.0        # Install specific version
nvm use 20.16.0            # Switch to version
```

**Recommended stable version:** Node.js 20.16.0

### 2.3 Updating n8n
```bash
npm update -g n8n          # Update to latest version
```

**Update frequency:** Check for updates regularly as n8n is actively developed

---

## 3. Cloud Alternative - n8n.io

### 3.1 When to Use Cloud Version
- Don't want local installation
- Easier setup process
- Need hosting capabilities
- Working with team members

### 3.2 Getting Started
1. Visit [n8n.io](https://n8n.io)
2. Click "Get Started for free"
3. Sign up with email
4. **Free trial:** 2 weeks, no credit card required

### 3.3 Advantages of Cloud Version
- Automatic updates
- No local maintenance
- Built-in integrations work with one click
- Hosting included
- Better for webhooks and external triggers

---

## 4. Interface Overview

### 4.1 Main Navigation
- **Workflows**: Create and manage automations
- **Credentials**: Store API keys and authentication
- **Executions**: View workflow run history
- **Templates**: Browse marketplace for pre-built workflows

### 4.2 Workflow Canvas
- **Control + Drag**: Move around canvas
- **Control + Scroll**: Zoom in/out
- **Plus Button**: Add new nodes
- **Always start with trigger node**

### 4.3 Settings & Configuration
- **Timezone**: Critical for time-based workflows
- **User Management**: Account settings
- **API Access**: For programmatic control
- **Version Information**: Check for updates

---

## 5. First Automation - Form to Airtable

### 5.1 Workflow Overview
**Goal**: Create a hotel booking form that automatically saves submissions to Airtable

**Components needed:**
- Form trigger node
- Airtable node
- Proper credentials setup

### 5.2 Setting Up the Form Trigger

#### Step 1: Create Workflow
1. Click "Create Workflow"
2. Name it "Airtable" 
3. **Important**: Set timezone in settings
4. Save workflow

#### Step 2: Configure Form Trigger
1. Add "On form submission" trigger
2. **Form title**: "Room"
3. **Description**: "What room do you like?"

#### Step 3: Add Form Fields
**Field 1 - Name:**
- Label: "Your Name"
- Type: Text
- Placeholder: "type your Name"
- Required: Yes

**Field 2 - Room Selection:**
- Label: "What room do you like?"
- Type: Dropdown
- Options: "single room", "deluxe room", "suite"
- Required: Yes

### 5.3 Setting Up Airtable Integration

#### Step 1: Create Airtable Database
1. Go to [airtable.com](https://airtable.com)
2. Create account (free)
3. Create workspace: "Test Airtable"
4. Create table with fields: "Name" and "Room"

#### Step 2: Get API Token
1. Click profile → Developer Hub
2. Create "Personal Access Token"
3. Name: "N8N2" 
4. Permissions needed:
   - Read records
   - Write records
   - Read schema
5. Select workspace access
6. Copy token

#### Step 3: Configure n8n Airtable Node
1. Add Airtable node after form trigger
2. Operation: "Create"
3. Create new credentials with API token
4. Select base: "Test Airtable"
5. Select table: "Table 1"
6. Map form fields:
   - Name: `{{ $json['Your Name'] }}`
   - Room: `{{ $json['What room do you like?'] }}`

### 5.4 Testing the Workflow

#### Test Mode
1. Click "Test Workflow"
2. Fill out form with sample data
3. Check if data appears in Airtable

#### Production Mode
1. Set workflow to "Active"
2. Use production URL for real submissions
3. Share URL with users

---

## 6. Workflow Management

### 6.1 Importing/Exporting Workflows

#### Exporting
1. Click three dots on workflow
2. Select "Download"
3. Saves as JSON file

#### Importing
1. Create new workflow
2. Click three dots → "Import from file"
3. Select JSON file
4. All settings and connections preserved

### 6.2 Workflow Marketplace
- **Templates section**: Browse pre-built workflows
- **Free options**: Many templates available at no cost
- **Paid options**: Advanced workflows ($1-$49)
- **Selling workflows**: Create and sell your own

### 6.3 Best Practices
- Always test workflows before activating
- Save frequently during development
- Use descriptive names for workflows
- Document complex logic
- Export backups of important workflows

---

## 7. Data Handling & Processing

### 7.1 Scheduled Triggers
**Purpose**: Run workflows automatically at set intervals

#### Time Trigger Configuration
- **Interval options**: Minutes, hours, days, weeks
- **Example**: Every minute, every day at midnight
- **Use cases**: Data backups, report generation, monitoring

### 7.2 Data Conversion Example

#### Workflow: Airtable to Local File
**Components:**
1. **Schedule Trigger**: Every minute
2. **Airtable Node**: Search records
3. **Convert to File**: Transform data to text
4. **Write to Disk**: Save locally

#### Configuration Steps
1. Schedule trigger → Every 1 minute
2. Airtable → Search operation → Select base/table
3. Convert to File → Text format → Select data field
4. Write File → Specify local path

**Note**: This is for learning data flow concepts, not practical production use

### 7.3 Data Flow Concepts
- **Passing data between nodes**: Automatic data flow
- **Data transformation**: Converting formats (JSON, text, CSV)
- **Local file operations**: Reading/writing to disk (local only)
- **Multiple items handling**: Processing arrays of data

---

## 8. Google Sheets Integration

### 8.1 Why Google Sheets
- Popular data storage
- Real-time collaboration
- Easy data visualization
- Familiar interface

### 8.2 Local vs Cloud Setup

#### Cloud Version (Easy)
1. Add Google Sheets node
2. Click "Sign in with Google"
3. Authorize access
4. Ready to use

#### Local Version (Complex)
Requires Google Cloud Console setup:

### 8.3 Google Cloud Console Setup (Local Only)

#### Step 1: Create Project
1. Go to [console.cloud.google.com](https://console.cloud.google.com)
2. Create Google Cloud account
3. Create new project
4. Name: "N8N Course"

#### Step 2: Enable APIs
1. Go to APIs & Services → Library
2. Search "Google Sheets API"
3. Enable the API

#### Step 3: OAuth Consent Screen
1. Go to OAuth consent screen
2. Choose "External"
3. Fill in app name: "N8N Course"
4. Add your email address
5. Complete setup

#### Step 4: Create Credentials
1. Go to Credentials → Create credentials
2. Choose "OAuth client ID"
3. Type: Web application
4. Name: "Web client one"
5. **Important**: Add OAuth redirect URL from n8n
6. Copy client ID and client secret

#### Step 5: Configure n8n
1. In n8n Google Sheets node
2. Create new credentials
3. Paste client ID and secret
4. Add OAuth redirect URL
5. Add test user (your email)
6. Sign in with Google

### 8.4 Using Google Sheets Node
**Basic operations:**
- Create spreadsheet
- Read data from sheets
- Write data to sheets
- Update existing data

**Example workflow:**
1. Manual trigger
2. Google Sheets → Create spreadsheet
3. Test and verify creation

---

## 9. Key Learning Principles

### 9.1 Learning Philosophy
**"Learning is same circumstances but different behavior"**
- Practice builds competence
- Repetition creates muscle memory
- Each attempt improves understanding

### 9.2 Hands-On Approach
**Why build yourself vs. import:**
- Understanding vs. just using
- Problem-solving skills
- Customization ability
- Troubleshooting capability

### 9.3 Progressive Complexity
**Course structure:**
1. Basic installations and setup
2. Simple hard-coded automations
3. Data processing and transformation
4. API integrations
5. **Next**: AI and LLM integration

### 9.4 Collaborative Learning
**Benefits of community:**
- Shared knowledge
- Problem-solving support
- Win-win situations
- Value creation for others

---

## 10. Troubleshooting Common Issues

### 10.1 Installation Problems
**Symptoms**: n8n won't install or start
**Solutions**:
- Check Node.js version (use 20.16.0)
- Ensure admin privileges
- Clear npm cache: `npm cache clean --force`
- Use NVM to switch Node versions

### 10.2 Google Cloud Console Issues
**Common problems:**
- Missing API enablement
- Incorrect OAuth URLs
- Test user not added
- Credential mismatch

**Solutions:**
- Follow setup steps exactly
- Double-check all URLs
- Ensure test user is added
- Verify credential copying

### 10.3 Workflow Execution Issues
**Symptoms**: Workflows fail or don't trigger
**Checks:**
- Timezone settings correct
- Credentials properly configured
- Required fields filled
- Active status for production

---

## 11. Next Steps & Advanced Topics

### 11.1 Upcoming Sections
- **AI Integration**: Adding LLMs to workflows
- **Complex automations**: Multi-step processes
- **Webhook handling**: Real-time triggers
- **Error handling**: Robust workflow design
- **Production deployment**: Hosting and scaling

### 11.2 Skill Building Path
1. **Master basics**: Forms, triggers, simple integrations
2. **Data manipulation**: Processing, transforming, routing
3. **API integrations**: Third-party services
4. **AI enhancement**: Intelligent processing
5. **Advanced patterns**: Complex business logic

### 11.3 Monetization Opportunities
- **Template sales**: Create and sell workflows
- **Consulting services**: Help businesses automate
- **Custom solutions**: Build specific automations
- **Training/courses**: Teach others n8n skills

---

## Summary

This section establishes the foundation for n8n automation development. You've learned:

- **Installation methods**: Local and cloud options
- **Basic workflow creation**: Form to database automation
- **Data handling**: Processing and transformation concepts
- **Integration setup**: Google Sheets and Airtable connections
- **Workflow management**: Import/export and version control
- **Troubleshooting**: Common issues and solutions

The key is hands-on practice with progressively complex workflows, building from these basic concepts toward advanced AI-powered automations.
