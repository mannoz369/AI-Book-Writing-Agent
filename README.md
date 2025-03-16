# AI-BOOK-WRITING-AGENT
# Automated Book Writer with Gemini and GitHub Actions

This project automates the process of writing a book using Gemini (Google's generative AI) and GitHub Actions. It utilizes CrewAI to orchestrate a multi-agent system that plans, writes, and formats chapters, then commits them to a GitHub repository daily.

## Features

* **Automated Book Generation:** Generates book chapters daily using Gemini.
* **Multi-Agent System:** Uses CrewAI to manage planning, writing, and formatting agents.
* **GitHub Integration:** Commits chapters to a GitHub repository automatically.
* **Markdown Formatting:** Ensures chapters are formatted in Markdown for readability.
* **Scheduled Execution:** Uses GitHub Actions to run the script daily at a specified time.

## Prerequisites

* **Google Cloud Account:**
    * Access to the Gemini API.
    * A Google Cloud project with the Gemini API enabled.
    * Google API key.
* **GitHub Account:**
    * A GitHub repository to store the book.
    * A GitHub Personal Access Token (PAT) with `repo` or fine-grained repository permissions.
* **Python 3.9+:**
    * Python installed on your local machine (for initial setup).
* **Python Libraries:**
    * `crewai`
    * `google-generativeai`
    * `PyGithub`
    * `requests`

## Setup

1.  **Clone the Repository:**
    ```bash
    git clone [your-repository-url]
    cd [your-repository-directory]
    ```

2.  **Install Dependencies:**
    ```bash
    pip install crewai google-generativeai PyGithub requests
    ```

3.  **Configure Environment Variables:**
    * Set your Google API key and GitHub PAT as environment variables:
        * `GOOGLE_API_KEY`: Your Gemini API key.
        * `GITHUB_TOKEN`: Your GitHub PAT.
    * It is recomended to store these as GitHub secrets.

4.  **GitHub Secrets:**
    * In your GitHub repository, go to "Settings" > "Secrets and variables" > "Actions".
    * Add the following repository secrets:
        * `GOOGLE_API_KEY`: Your Google Gemini API key.
        * `GITHUB_TOKEN`: Your GitHub Personal Access Token.

5.  **Configure Repository Information:**
    * In the Python script (`your_script_name.py`), update the following variables:
        * `GITHUB_USERNAME`: Your GitHub username.
        * `REPO_OWNER`: The repository owner's username.
        * `REPO_NAME_PART`: The repository name.
        * `BRANCH`: The branch to commit to (usually `main`).

6.  **Create GitHub Actions Workflow:**
    * Create a directory `.github/workflows` in your repository.
    * Create a file `daily_book_writer.yml` in the `workflows` directory.
    * Copy and paste the workflow code from the provided example into the YAML file.
    * Modify the python version, and the python file name if needed.
    * Commit and push the changes to your repository.

7.  **Run the Script (Initial Setup):**
    * Run the Python script locally to create the initial book plan:
        ```bash
        python your_script_name.py
        ```
    * This will create `book_plan.md` in your repository.

8.  **Automated Execution:**
    * GitHub Actions will now automatically run the script daily at 1:00 AM UTC (or the schedule you configured).

## Workflow

1.  **Planning:** The `planning_agent` generates a book plan and chapter titles.
2.  **Writing:** The `writing_agent` writes a chapter based on the plan and previous chapters.
3.  **Formatting:** The `formatting_agent` formats the chapter in Markdown.
4.  **Committing:** The script commits the formatted chapter to the GitHub repository.

## Notes

* Ensure your GitHub token has the necessary permissions to commit changes to your repository.
* Monitor the GitHub Actions workflow runs for any errors.
* Change the cron schedule in the github actions file to modify the time that the script runs.
* Replace `your_script_name.py` with the actual name of your python file.
