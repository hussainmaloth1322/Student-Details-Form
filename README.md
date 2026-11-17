# Q10 – Student Details Form

**Question-paper requirements:** HTML/JavaScript form, mandatory-field validation, Git/GitHub, Jenkins build, Docker image and running container.

## A. Run directly
Open `index.html` in Chrome, or use VS Code Live Server. Test:
- Submit with empty fields: mandatory-field warning.
- Enter an invalid email: email warning.
- Enter all valid fields: success message.

This is a front-end lab form; it does not save records to a database.

## B. GitHub
Create an empty repository and push this folder using the general Git commands in the top-level README.

## C. Docker
```powershell
docker build -t student-form .
docker run -d -p 8081:80 --name student-form-container student-form
docker ps
```
Open `http://localhost:8081`.

To stop/remove:
```powershell
docker rm -f student-form-container
```

## D. Jenkins
The included Jenkinsfile uses Windows `bat` steps and starts the form on host port 8081, leaving the usual Jenkins UI port 8080 free.

1. Push this folder's contents to its own GitHub repository (so Dockerfile is at repository root).
2. Jenkins → New Item → Pipeline.
3. Pipeline Definition: **Pipeline script from SCM**.
4. SCM: Git; enter repository URL; Branch: `*/main`; Script Path: `Jenkinsfile`.
5. Save → Build Now.
6. Check Console Output and open `http://localhost:8081`.

The Jenkins Windows agent must have Docker CLI installed and access to the Docker Engine. If your Jenkins agent is Linux, the supplied Windows `bat` commands must be converted to `sh`.
