# lab11
Below is a **clear, exam-ready, step-by-step guide** to run the **“Build a Docker Container from a Custom Dockerfile”** program exactly as shown in your images (Program-1).

---

## ✅ Prerequisites

* Docker installed and running
  Check using:

  ```bash
  docker --version
  ```

---

## 📁 Step 1: Create Project Directory

```bash
mkdir Program-1
cd Program-1
```

---

## 📄 Step 2: Create `Dockerfile`

```bash
nano Dockerfile
```

**Paste the following content exactly:**

```dockerfile
# Use a slim Python base image
FROM python:3.9-slim

# Set the working directory inside the container
WORKDIR /app

# Copy the requirements file and install dependencies
COPY requirements.txt .
RUN pip install --no-cache-dir -r requirements.txt

# Copy the application code
COPY . .

# Set Flask environment variables
ENV FLASK_APP=app.py
ENV FLASK_RUN_HOST=0.0.0.0
ENV FLASK_RUN_PORT=5000

# Expose the port the Flask app will run on
EXPOSE 5000

# Define the command to run the Flask application
CMD ["flask", "run"]
```

Save and exit: **CTRL + X → Y → Enter**

---

## 🐍 Step 3: Create `app.py`

```bash
nano app.py
```

**Paste:**

```python
from flask import Flask

app = Flask(__name__)

@app.route("/")
def hello():
    return "Hello, Docker!"

if __name__ == "__main__":
    app.run(host="0.0.0.0", port=5000)
```

Save and exit.

---

## 📦 Step 4: Create `requirements.txt`

```bash
nano requirements.txt
```

**Add:**

```
flask
```

Save and exit.

---

## 🏗️ Step 5: Build Docker Image

Run this inside `Program-1` directory:

```bash
docker build -t program-1 .
```

✔️ Image will be created successfully.

Verify:

```bash
docker images
```

---

## ▶️ Step 6: Run Docker Container

```bash
docker run -d -p 5000:5000 --name flask-container program-1
```

Check running container:

```bash
docker ps
```

---

## 🌐 Step 7: Test the Application

Open browser and visit:

```
http://localhost:5000
```

✅ Output displayed:

```
Hello, Docker!
```

---

## 🛑 Step 8: Stop & Remove (Optional)

```bash
docker stop flask-container
docker rm flask-container
```

---

## 📌 Final Folder Structure

```
Program-1/
│
├── Dockerfile
├── app.py
└── requirements.txt
```

---


