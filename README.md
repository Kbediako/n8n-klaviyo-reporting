# N8N Klaviyo Automated Reporting

This repository contains a fully functional n8n workflow that automatically generates and distributes reporting data from Klaviyo. The workflow periodically pulls campaign data and performance metrics, processes and aggregates results, and outputs a formatted HTML report via email.

## Features

- **Automated scheduling**: Configurable to run on your preferred schedule (default: weekly)
- **Comprehensive data collection**: Pulls campaign data and relevant metrics (opens, clicks) from Klaviyo's API
- **Data aggregation**: Processes raw API responses into useful summaries and campaign-specific metrics
- **Professional HTML reporting**: Generates a formatted HTML email with tables for campaign performance
- **Error handling**: Built-in error handling branches to ensure reliable operation

## Setup Instructions

### Prerequisites

1. An n8n instance (cloud or self-hosted)
2. Klaviyo account with API access
3. Email sending capability configured in n8n

### Installation

1. **Import the workflow**:
   - Download the `workflow.json` file from this repository
   - In your n8n instance, go to "Workflows" and click "Import from File"
   - Select the downloaded `workflow.json` file

2. **Configure Klaviyo API credentials**:
   - Create a new credential of type "Generic API"
   - Name it "Klaviyo API"
   - For Authentication, select "Query Auth"
   - Enter your Klaviyo Private API key as the value for "api_key"
   - Save the credential

3. **Configure metrics**:
   - In the "Fetch Metrics (Opens)" and "Fetch Metrics (Clicks)" nodes:
     - Update the query parameters to include your specific metric_id values for opens and clicks
     - You can find these metric IDs in your Klaviyo account or via the Metrics API

4. **Configure email reporting**:
   - In the "Send Email Report" node:
     - Update the "From Email" (reports@yourdomain.com)
     - Update the "To Email" (recipient@yourdomain.com)
     - Configure additional email settings as needed

5. **Configure schedule** (optional):
   - In the "Schedule Trigger" node, adjust the timing to your preferred reporting schedule

### Testing

1. Before activating the workflow, use the "Execute Workflow" button to test it manually
2. Check that the API calls succeed and that the resulting email contains the expected data
3. Examine the output of the "Process Data" node to see the raw report data

## Customization Options

### Adjusting the Report Content

To modify what data is included in the reports, you can edit the "Process Data" node's JavaScript code:

- Add additional metrics by creating new HTTP Request nodes and incorporating them in the processing logic
- Modify the HTML report layout by editing the `generateHtmlReport()` function
- Calculate additional statistics by extending the data aggregation portion of the code

### Alternative Output Options

Instead of email, you can output the report data to:

1. **Slack/Teams**: Add a Slack or Microsoft Teams node after the "Process Data" node
2. **Google Sheets**: Use a Google Sheets node to write data for archiving
3. **File storage**: Save reports as files using the appropriate nodes

## Troubleshooting

Common issues and solutions:

- **API Authorization Errors**: Verify your Klaviyo API key is correct and has the necessary permissions
- **Empty Reports**: Check that your date range includes active campaigns
- **Pagination Issues**: For large datasets, you may need to adjust the pagination settings in the HTTP Request nodes

## Advanced Usage

### Adding List and Segment Data

To include subscriber list or segment information:

1. Add a new HTTP Request node that calls the appropriate Klaviyo endpoint (e.g., `/api/v1/lists`)
2. Connect this node to the "Combine Results" node
3. Update the "Process Data" node to include the new information in your report

### Enhanced Error Handling

For more robust error handling:

1. Replace the simple "Error Handler" node with a more sophisticated error notification system
2. Add a "Send Email" node connected to the error paths to receive notifications when issues occur

## License

This project is licensed under the MIT License - see the LICENSE file for details.

## Contributing

Contributions are welcome! Please feel free to submit a Pull Request.

---

*Note: This workflow requires a valid Klaviyo account with API access and assumes you have already set up n8n with the necessary email sending capabilities.*