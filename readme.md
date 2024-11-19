# RestAPI for Creating QR Codes:
- I followed instruction and Install and run API.

# Install
1. First create git Clone
2. Make virtual environment:  python3 -m virtualvenv
3. Activate virtual environment: source venv/bin/activate
  Install:
   pip install fastapi 
   pip install uvicorn
   sudo apt install python3-dotenv
4. Install requirements: pip install -r requirements.txt and pip freeze > requirements.txt
5. Note: make sure docker is started
6. run pytest locally to check that it works locally
7. Start the app with docker compose up --build
8. Goto http://localhost/docs to view openapi spec documentation
9. Click "authorize" input username: admin password: secret
10. Test making,  retrieving, and deleting QR codes on the spec page. 



docker builder prune -a
