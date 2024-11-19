# HW-9 RestAPI for Creating QR Codes:
- This project provides a REST API to generate, retrieve, and delete QR codes. Built using FastAPI, the application supports Docker deployment and provides an OpenAPI specification for testing.

 ## Key Features:
- Generate QR Codes: Create QR codes from provided data.
- Retrieve QR Codes: View and download previously generated QR codes.
- Delete QR Codes: Remove QR codes from the server.
- OpenAPI Documentation: Interactive API documentation available at /docs.

# Instruction:
1. First create git Clone
2. Create virtual environment:  python3 -m virtualvenv
3. Activate virtual environment: source venv/bin/activate
4. Install Required Dependencies
   - pip install fastapi 
   - pip install uvicorn
   - sudo apt install python3-dotenv Python3-jose
- Install requirements: pip install -r requirements.txt and pip freeze > requirements.txt

## Fix error:
  - when I run pytest showed error :
  - 2024-11-19 16:44:46 - root - ERROR - Permission denied when trying to create directory qr_codes:[Errno 13] Permission denied: 'qr_codes'
  - --> Solution:
  1. add Default directory path using environment variable in file app/service/qr_service.py
   - QR_DIRECTORY = Path(os.getenv("QR_DIRECTORY", "/tmp/qr_codes"))

  2. Update app/main.py to Use the Default Path Replace the hardcoded path with the new QR_DIRECTORY:
   - from pathlib import Path
   - QR_DIRECTORY = Path(os.getenv("QR_DIRECTORY", "/tmp/qr_codes"))
   - create_directory(QR_DIRECTORY) 
  3. Modify DockerFile add  writable directory exists and set appropriate permissions during the build process: 
   - RUN mkdir -p /tmp/qr_codes && chmod -R 777 /tmp/qr_codes

## Docker Instructions:
1. sign in docker account and run docker
2.  Buliding docker image:
 - docker build -t hw-9_qrcodeapi . 
3. run pytest locally to check that it works locally
 - docker run hw-9_qrcodeapi pytest

4. Start the application with docker compose:

 1. docker compose up --build
 2. Goto http://localhost/docs to view openapi spec documentation
 3. Click "authorize" input username: admin password: secret
 4. I did Test making,  retrieving, and deleting QR codes on the spec page. 
  -  when I Get qr_codes TryOut and generate view hyperlink and copy this link new tab  QR-code generated.

5. Alternative Run:

 1. start application with ./start.sh OR uvicorn app.main:app --host 0.0.0.0 --port 8000 --reload
 2. Goto http://localhost:8000/docs to view openapi spec documentation
 3. Click "authorize" input username: admin password: secret
 4. I did Test making,  retrieving, and deleting QR codes on the spec page. 
 - when I Get qr_codes TryOut and generate view hyperlink and copy this link new tab not generate QR-code.
 
## Docker Container link :
-  https://hub.docker.com/repository/docker/nishi2110/hw-9apiqrcode/Tags 

## Endpoints:
1. Generate QR Code
- Use the POST /qr_codes endpoint to create a QR code.
- Input your desired data, and a QR code image will be generated.

2. Retrieve QR Codes
- Use the GET /qr_codes endpoint to view available QR codes.
- Click on the generated hyperlink to view or download the QR code.

3. Delete QR Code
- Use the DELETE /qr_codes/{filename} endpoint to delete a specific QR code.

## Docker Command:
- This command removes unused build cache to free up disk space: docker builder prune -a
