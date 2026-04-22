# EC2 Remediation System

## Overview

The EC2 Remediation System is a comprehensive ServiceNow application designed to automate the monitoring, detection, and remediation of Amazon EC2 instances. This system integrates with AWS monitoring tools, leverages AI-powered search capabilities within ServiceNow, and provides real-time notifications through Slack to ensure rapid response to infrastructure issues.

## Features

- **Automated EC2 Monitoring**: Continuous monitoring of EC2 instances for health and performance issues
- **AI-Powered Knowledge Search**: Intelligent search through ServiceNow knowledge base using AI to find relevant remediation steps
- **Slack Integration**: Real-time notifications to DevOps teams via Slack with formatted messages and actionable links
- **Flow-Based Automation**: ServiceNow Flow Designer integration for automated incident management and remediation workflows
- **Customizable Remediation Actions**: Flexible system allowing for custom remediation scripts and actions based on issue type
- **Comprehensive Logging**: Detailed logging and audit trails for all remediation activities

## Architecture

The system consists of several key components:

1. **EC2 Instance Table**: Custom table for tracking EC2 instances and their status
2. **Remediation Table**: Records of remediation actions taken
3. **AI Search Integration**: Custom script includes for intelligent knowledge base searching
4. **Flow Designer Workflows**: Automated processes for incident creation, investigation, and resolution
5. **Slack Notification System**: Integration for team communication and alerts

## Prerequisites

- ServiceNow Personal Developer Instance (PDI) or Enterprise instance
- AWS account with EC2 instances
- Slack workspace with appropriate permissions
- ServiceNow AI Search configured and enabled
- Flow Designer access

## Installation

1. **Import Update Set**:
   - Download the `ec2-remediation-system.xml` file
   - Navigate to System Update Sets > Retrieved Update Sets
   - Click "Import Update Set from XML"
   - Upload and commit the update set

2. **Configure AWS Integration**:
   - Set up AWS credentials in ServiceNow
   - Configure connection aliases for AWS API calls
   - Set up HTTP connections for AWS services

3. **Configure Slack Integration**:
   - Create Slack app with appropriate permissions
   - Configure webhook URLs in ServiceNow
   - Set up notification channels

4. **AI Search Setup**:
   - Ensure AI Search is enabled in your ServiceNow instance
   - Configure search contexts for EC2-related knowledge
   - Set up retrieval profiles for relevant knowledge bases

## Usage

### Monitoring EC2 Instances

1. Import EC2 instances into the custom EC2 Instance table
2. Configure monitoring thresholds and alert conditions
3. The system will automatically detect issues and create incidents

### Incident Response Workflow

1. **Issue Detection**: System detects EC2 performance issues
2. **Incident Creation**: Automatic incident creation with detailed information
3. **AI Knowledge Search**: Searches knowledge base for remediation steps
4. **Slack Notification**: Notifies team with findings and next steps
5. **Remediation Trigger**: Manual or automatic triggering of remediation actions
6. **Resolution Tracking**: Updates incident status and logs resolution

### Manual Remediation

- Use the "Trigger EC2 Remediation" UI action on incident records
- Review AI search results for appropriate remediation steps
- Execute remediation scripts through the system

## Configuration

### Key Tables

- `x_snc_ec2_monito_0_ec2_instance`: EC2 Instance records
- `x_snc_ec2_monito_0_remediation_log`: Remediation action logs
- `incident`: Standard incident table with custom fields

### Custom Script Includes

- `custom_EC2RemediationHelper`: Handles AI search and Slack formatting

### Flow Designer Flows

- EC2 Remediation Flow: Main automation workflow
- Slack Notification Flow: Handles team communications

## Screenshots

The `screenshots/` directory contains detailed visual documentation of:

- Application setup and configuration
- Table structures and relationships
- Flow Designer workflows
- UI actions and integrations
- Final system in action

## Contributing

1. Fork the repository
2. Create a feature branch
3. Make your changes
4. Test thoroughly in a PDI instance
5. Submit a pull request with detailed description

## Support

For support and questions:

- Check the knowledge base articles included in the update set
- Review the screenshots for configuration guidance
- Create an issue in this repository

## License

This project is licensed under the MIT License - see the LICENSE file for details.

## Version History

- **v1.0.0**: Initial release with core EC2 monitoring and remediation capabilities</content>
