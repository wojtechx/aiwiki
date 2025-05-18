# AI Wiki Article Automation - Workflow Explanation
_Generated on 2025-05-18_

## Workflow Title
AI-Powered Wiki Article Automation with Fallback Handling and GitHub Integration

## 1. Webhook Node – Receive Article URL
Starts the automation when a POST request is sent to the webhook with a JSON body containing a `url`. This URL points to the page from which the article will be extracted.

## 2. HTTP Request – Scrape Web Page
Fetches the full HTML content of the target page using the provided URL. This raw HTML includes navigation, scripts, and non-article elements.

## 3. Function – Clean HTML
Cleans the raw HTML to make it more suitable for AI processing. This involves removing problematic characters and formatting it for GPT processing.

## 4. OpenAI Message Model – Generate Title and Content
Sends the cleaned HTML to OpenAI GPT-4.1 Mini, prompting it to generate:
- A **clear, AI-written article title**
- The **clean, readable article body**  
The model responds with a strict JSON object. If parsing fails, a fallback is triggered.

## 5. Code – Parse + Format + Fallback
Parses the OpenAI output, and:
- Generates a **slug-based filename**
- Wraps the content in **Jekyll-compatible Markdown**
- Routes failed AI responses to a separate `/fallback/` folder

## 6. GitHub Get – Check for Existing File
Queries the GitHub repository (`wojtechx/aiwiki`) to check if the file already exists. If it does, retrieves its `sha` for versioning.

## 7. Merge – Combine New + Existing Metadata
Merges the newly generated content with the GitHub `sha` (if any) to decide whether to **update or create** a file.

## 8. Set Fields – Normalize Output
Maps final values like `filename`, `markdown`, `sha`, and `commit_message` to unified output fields.

## 9. IF – Decide: Update or Create
If a `sha` is present → update the file  
If not → remove `sha` and prepare to create new file

## 10. GitHub Update (if exists)
Updates the existing file on GitHub using the GitHub API and the retrieved `sha`.

## 11. GitHub Create (if new)
Creates a new file in the appropriate subfolder (e.g. `posts/` or `fallback/`) with the markdown content and commit message.

## Final Result
The article is published to GitHub Pages via the repository's `main` branch. Failed AI responses are saved for manual review. A clean commit history is maintained with meaningful messages like:

