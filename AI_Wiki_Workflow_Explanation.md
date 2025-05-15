# AI Wiki Article Automation - Workflow Explanation
_Generated on 2025-05-15_

## Workflow Title
AI-Powered Wiki Article Automation

## 1. Webhook Node - Receive Article URL
Receives a POST request with JSON containing a 'url' (page to scrape) and 'title'. This starts the entire automation workflow.

## 2. HTTP Request - Scrape Web Page
Uses the provided URL to fetch the full HTML content of the target page. The raw HTML may include ads, navigation, and unrelated elements.

## 3. HTTP Request - OpenAI Extract Article (HTTP)
Sends the HTML to OpenAI GPT-4 to extract only the main article. Prompts the model to remove clutter and return a clean, readable article.

## 4. Function - Format Markdown
Wraps the AI output in Jekyll-compatible Markdown with frontmatter. Creates the filename and commit message for GitHub.

## 5. HTTP Request - Push to GitHub
Pushes the Markdown file to the 'wojtechx/aiwiki' GitHub repo using the GitHub API. Triggers GitHub Pages to publish the article.

## 6. Respond to Webhook
Returns a success message with the filename to the client (form, API, or script).
