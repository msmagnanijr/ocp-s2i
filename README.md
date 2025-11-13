# Todo Frontend - OpenShift S2I Demo

Simple HTML/JavaScript frontend for the Todo API, demonstrating Source-to-Image (S2I) deployment on OpenShift.

## Features

- ✨ Modern, responsive UI
- 📊 Real-time task statistics
- ✅ Add, complete, and delete tasks
- 🔄 Auto-refresh every 30 seconds
- 🎨 Beautiful gradient design

## Local Development

Simply open `index.html` in a browser. Make sure the API is running on `http://localhost:5000`.

## Deploy to OpenShift using S2I

### Option 1: Using oc new-app (Recommended)

```bash
# Create the frontend app using nginx S2I
oc new-app nginx:latest~https://github.com/YOUR-USERNAME/YOUR-REPO.git \
  --context-dir=frontend \
  --name=todo-frontend

# Expose the service
oc expose svc/todo-frontend

# Get the URL
oc get route todo-frontend
```

### Option 2: From Local Directory

```bash
# Create a binary build
oc new-build nginx:latest --binary=true --name=todo-frontend

# Start the build from local directory
oc start-build todo-frontend --from-dir=. --follow

# Create the deployment
oc new-app todo-frontend

# Expose the service
oc expose svc/todo-frontend
```

### Option 3: Using YAML

```bash
oc apply -f openshift-s2i.yaml
```

## Configuration

The frontend automatically detects the API URL:
- **Local development**: Uses `http://localhost:5000`
- **Production**: Uses `/api` path (proxied by nginx to backend service)

## Project Structure

```
frontend/
├── index.html       # Main application
├── nginx.conf       # Nginx configuration for S2I
└── README.md        # This file
```

## API Endpoints Used

- `GET /` - Health check
- `GET /tasks` - List all tasks
- `POST /tasks` - Create task
- `PUT /tasks/:id` - Update task
- `DELETE /tasks/:id` - Delete task

## Browser Compatibility

Works on all modern browsers:
- Chrome/Edge 90+
- Firefox 88+
- Safari 14+

---

Created for Red Hat Container Workshop
