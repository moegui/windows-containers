# How to run Jenkins Windows image

Start an “elevated” PowerShell (run it as administrator). Search for PowerShell, right-click, and choose Run as administrator. Move to repository cloned and following the steps:

## 1) Build image

```powershell
 docker build -t moegui/jenkins .\jenkins\.
```

## 2) Run image

```powershell
docker run --name jenkins -e TZ=Etc/GMT-3 -p 8080:8080 moegui/jenkins
```

## 3) Connect to Jenkins

+ Jenkins = http://localhost:8080 (user: jenkinks pass: jenkinks)