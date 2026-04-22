# Directory Structure and Code Workflow

## Project Structure

```
ec2-remediation-system/
├── custom_EC2RemediationHelper.js    # Main script include for AI search and Slack integration
├── ec2-remediation-system.xml        # ServiceNow update set for system deployment
├── screenshots/                      # Visual documentation of setup and workflows
│   ├── 000 custom app.png
│   ├── 001 ec2 instance table.png
│   ├── 002 remediation table.png
│   ├── 003 connection alias.png
│   ├── 004 http connection.png
│   ├── 005 auth credentials.png
│   ├── 006 ui action trigger remediation.png
│   ├── 007 script include remediation call.png
│   ├── 008 flow.png
│   ├── 009 flow trigger.png
│   ├── 010 flow a1 incident record.png
│   ├── 011 flow a2 ai search.png
│   ├── 012 flow a3 set flow variables.png
│   ├── 013 flow a3_1 variable config.png
│   ├── 014 flow a3_2 variable definition.png
│   ├── 015 flow a4 slack issue.png
│   ├── 016 flow a5-6 do and wait.png
│   ├── 016 flow a6 trigger remediation.png
│   ├── 017 flow a7 instance on trigger.png
│   ├── 018 flow a8 update incident.png
│   ├── 019 flow a9 slack resolution.png
│   ├── 020 flow a9_1 minutes division.png
│   ├── 021 flow a9_2 minutes rounding.png
│   ├── 022 ai search custom_article linking.png
│   ├── 023 ai search custom_search app choice.png
│   ├── 024 ai search custom output log.png
│   ├── 025 ai custom search default search app config.png
│   ├── 026 ai custom search default search app profile.png
│   ├── 027 ai custom search default search app sources.png
│   ├── 028 ai custom search default search app retrievals.png
│   ├── 029 knowledge base.png
│   ├── 030 knowledge article.png
│   ├── 031 final slack cycle.png
│   ├── 032 final ec2 instance.png
│   ├── 033 final remediation log.png
│   ├── 034 final incidents.png
│   └── 035 final slack logs.png
└── README.md                         # Project overview and documentation
```

## Code Components

### custom_EC2RemediationHelper.js

**Purpose**: This is the core script include that handles AI-powered search functionality and Slack message formatting for the EC2 remediation system.

**Key Functions**:

1. **Input Processing**:
   - Accepts search terms, logging preferences, and search app specifications
   - Validates and sanitizes input parameters

2. **AI Search Configuration**:
   - Dynamically looks up AI search context configurations
   - Falls back to default search apps if specific app not found
   - Retrieves AI Search and Retrieval Profile configurations

3. **Search Execution**:
   - Uses `AISASearchUtil` to perform intelligent knowledge base searches
   - Handles both string and object result formats
   - Parses search results to extract article information

4. **Data Processing**:
   - Extracts article titles, sys_ids, table names, and content
   - Cleans HTML tags from titles and text
   - Identifies knowledge base numbers and record types

5. **Slack Message Formatting**:
   - Creates rich Slack messages with emojis and formatting
   - Includes record links for easy access
   - Provides contextual information based on record type (KB, Incident, Catalog Item)

6. **Output Generation**:
   - Sets multiple output variables for Flow Designer consumption
   - Includes status, count, titles, articles array, and formatted messages
   - Provides raw results for debugging

**Error Handling**:
- Catches configuration errors (missing search configs)
- Handles script execution errors with detailed logging
- Provides user-friendly error messages for Slack notifications

### ec2-remediation-system.xml

**Purpose**: ServiceNow update set containing all system configurations, tables, flows, and knowledge articles.

**Contents**:
- Custom application scope: `x_snc_ec2_monito_0`
- Table definitions for EC2 instances and remediation logs
- Flow Designer workflows
- UI actions and script includes
- Knowledge base articles with remediation procedures
- Connection aliases and authentication profiles

## Workflow Overview

### 1. EC2 Monitoring and Issue Detection

- EC2 instances are monitored through AWS integrations
- Health metrics and performance data are collected
- Threshold breaches trigger incident creation in ServiceNow

### 2. Incident Creation and Initial Assessment

- Flow Designer creates incident records with detailed EC2 information
- Incident is categorized and prioritized based on issue severity
- Initial diagnostic information is gathered

### 3. AI-Powered Knowledge Search

- `custom_EC2RemediationHelper.js` is called with issue keywords
- AI search queries the knowledge base for relevant articles
- Results are parsed and formatted for human consumption

### 4. Team Notification via Slack

- Formatted Slack messages are sent to DevOps channels
- Messages include issue details, found articles, and action items
- Links to ServiceNow records for direct access

### 5. Remediation Decision and Execution

- Team reviews AI search results and knowledge articles
- Manual or automatic remediation actions are triggered
- UI action "Trigger EC2 Remediation" executes remediation scripts

### 6. Resolution and Documentation

- Incident status is updated as remediation progresses
- Resolution time is tracked and logged
- Success/failure notifications are sent via Slack
- Knowledge base is updated with new remediation procedures if needed

## Data Flow

```
EC2 Instance Issue
        ↓
AWS Monitoring Alert
        ↓
ServiceNow Incident Creation
        ↓
Flow Designer Trigger
        ↓
AI Search Execution (custom_EC2RemediationHelper.js)
        ↓
Knowledge Base Query
        ↓
Results Parsing and Formatting
        ↓
Slack Notification
        ↓
Manual/Automated Remediation
        ↓
Incident Resolution
        ↓
Logging and Reporting
```

## Key Integration Points

### ServiceNow Components

- **Tables**: Custom EC2 instance and remediation log tables
- **Flows**: Automated workflows in Flow Designer
- **Script Includes**: Custom JavaScript for AI search and processing
- **UI Actions**: Manual triggers for remediation
- **Knowledge Base**: Articles with remediation procedures

### External Integrations

- **AWS**: EC2 instance monitoring and API calls
- **Slack**: Real-time team notifications
- **AI Search**: Intelligent knowledge discovery

## Configuration Requirements

### AI Search Setup

1. Enable AI Search in ServiceNow instance
2. Configure search contexts for EC2-related content
3. Set up retrieval profiles with appropriate sources
4. Ensure knowledge base articles are indexed

### Flow Designer Configuration

1. Import and activate the remediation flow
2. Configure flow variables and data mappings
3. Set up triggers for incident creation
4. Test flow execution with sample data

### Slack Integration

1. Create Slack app with webhook permissions
2. Configure incoming webhooks for notifications
3. Set up channel mappings for different issue types
4. Test message formatting and delivery

## Monitoring and Maintenance

### System Health Checks

- Monitor Flow Designer execution logs
- Check AI search response times and accuracy
- Review Slack notification delivery
- Audit remediation success rates

### Performance Optimization

- Optimize AI search queries for faster results
- Cache frequently accessed knowledge articles
- Implement retry logic for failed API calls
- Monitor system resource usage

### Update Procedures

- Test updates in development environment first
- Backup configurations before major changes
- Update knowledge base articles as procedures evolve
- Version control all script and configuration changes
