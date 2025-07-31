Project Summary:
----------------------------

This is a simple full-stack app where:

- The frontend is a basic HTML form served using NGINX inside a Docker container.
- The backend is a Python Flask app, also running in a container.
- Both containers talk to each other via a Docker network.

This project helped me learn:
✅ Dockerfile creation
✅ Container networking
✅ Flask app handling form data

----------------------------
📁 Folder Structure I Created:
----------------------------

devops_project/
├── frontend/
│   ├── index.html
│   └── Dockerfile
├── backend/
│   ├── app.py
│   └── Dockerfile

----------------------------
🌐 What I Did – Step by Step:
----------------------------

1. ✅ Created a basic `index.html` with a form (name + email).
2. ✅ Wrote a `Dockerfile` in frontend to copy `index.html` into `/usr/share/nginx/html`.
3. ✅ Created `app.py` in backend – a Flask app to handle `/submit` POST request.
4. ✅ Wrote backend `Dockerfile` that installs Flask and runs `app.py`.
5. ✅ Built both Docker images:

   ```bash
   cd backend
   sudo docker build -t rajashree/backend-app .

   cd ../frontend
   sudo docker build -t rajashree/frontend-app .
✅ Created a custom Docker network:

sudo docker network create rajashree-net

✅ Ran containers on that network:

# Backend
sudo docker run -d -p 5000:5000 --network rajashree-net --name backend rajashree/backend-app

# Frontend
sudo docker run -d -p 8081:80 --network rajashree-net --name frontend rajashree/frontend-app


✅ Opened http://localhost:8081 in the browser → filled form → clicked Submit

⚠️ Got some "Error contacting backend" initially 😩
→ Solved by checking container logs, using curl, fixing port conflicts,
and making sure the backend is reachable as http://backend:5000

✅ Tested POST from inside frontend container using:

curl -X POST http://backend:5000/submit \
  -H "Content-Type: application/json" \
  -d '{"name":"Rajashree", "email":"rajashree@example.com"}'
It returned: "User saved successfully!" 🎉

