#Primero clonamos el repositorio 
```bash
git clone [https://](https://github.com/Jreyesh26/fhir-demographics.git)
``` 

# installs nvm (Node Version Manager)
```bash
curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.39.7/install.sh | bash
``` 

# download and install Node.js
```bash
nvm install 20
``` 

# verifies the right Node.js version is in the environment
```bash
node -v # should print `v20.14.0`
``` 

# verifies the right NPM version is in the environment
```bash
npm -v # should print `10.7.0`
```
#Ejecutamos npm install para instalar las dependencias
```bash
npm install
```

#Creamos la imagen con docker-compose
```bash
docker-compose up --build -d
```
#Iniciamos la app
```bash
npm run dev
```
#Por lo general el host y el puerto es: http://localhost:5173
