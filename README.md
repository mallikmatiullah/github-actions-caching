# Docker Cache Demo

This repository demonstrates how to use GitHub Actions and Docker Buildx to efficiently cache Docker layers, significantly reducing build times and optimizing workflows.

## Overview
By leveraging Docker Buildx and GitHub Actions, this demo:
- Caches individual Docker layers to avoid redundant builds.
- Uses the `actions/cache` action to store the build context.
- Reuses cached layers for faster subsequent builds.

## Key Components
1. **GitHub Actions Workflow**
   - A CI/CD workflow to build and cache Docker layers.

2. **Dockerfile**
   - A sample Dockerfile to build a simple Python Flask application.

3. **Flask Application**
   - A minimal Flask app serving as the application to test the caching mechanism.

## Repository Structure
```
.
├── .github/workflows/ci.yml  # GitHub Actions workflow
├── Dockerfile                              # Dockerfile for the app
├── requirements.txt                        # Python dependencies
└── app.py                                  # Flask application
```

## Steps to Execute the Demo

### 1. Clone the Repository
```bash
git clone https://github.com/mallikmatiullah/github-actions-caching.git
cd github-actions-caching.git
```

### 2. Prepare the Repository
Ensure the following files are present:
- `.github/workflows/docker-cache-demo.yml`
- `Dockerfile`
- `requirements.txt` with the following content:
  ```
  flask
  ```
- `app.py` with the following content:
  ```python
  from flask import Flask
  app = Flask(__name__)

  @app.route('/')
  def hello():
      return "Hello, Docker Cache Demo!"

  if __name__ == "__main__":
      app.run(host="0.0.0.0", port=8080)
  ```

### 3. Push to GitHub
Push the repository to GitHub to trigger the workflow:
```bash
git add .
git commit -m "Initial commit"
git push origin main
```

### 4. Monitor Workflow Execution
Go to the **Actions** tab in your GitHub repository to monitor the progress of the workflow. Verify that caching is being utilized by checking the logs.

### 5. Run the Docker Image Locally (Optional)
To test the Docker image locally:
```bash
docker build -t demo-app .
docker run -p 8080:8080 demo-app
```
Visit `http://localhost:8080` to see the application running.

## Notes
- Ensure proper indentation in the `app.py` file as Python requires consistent indentation.
- The workflow uses `ubuntu-latest` as the runner. Modify it as needed for specific requirements.

## License
This project is open-source and available under the [MIT License](LICENSE).

