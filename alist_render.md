#m.daocloud.io/docker.io/xhofe/alist:v3.40.0
#PORT=5244
#PUID=0
#GUID=0
#TZ=Asia/Shanghai

# alist-render

### Deploy Alist to Render
[![Deploy to Render](https://render.com/images/deploy-to-render-button.svg)](https://render.com/deploy)

### database
You may need to use another remote MySQL database as instance restarts will lose data.
Recommended Free MySQL Databases:
- https://turso.tech/
- https://remotemysql.com/
- https://www.freesqldatabase.com/

services:
  # A Docker web service
  - type: web
    name: alist
    env: docker
    buildCommand: |
      wget https://github.com/alist-org/alist/releases/download/v3.40.0/alist-linux-amd64.tar.gz -O alist.tar.gz
      tar -zxvf alist.tar.gz
      chmod +x alist
    startCommand: ./alist server
    region: oregon # optional (defaults to oregon)
    plan: free # optional (defaults to starter)
    healthCheckPath: /

    envVars:
      - key: PORT
        value: 5244
      - key: DB_TYPE
        # value: sqlite3
        sync: false
      - key: DB_HOST
        # value: db_host
        sync: false
      - key: DB_PORT
        # value: 3306
        sync: false
      - key: DB_USER
        # value: db_user
        sync: false
      - key: DB_PASS
        # value: db_password
        sync: false
      - key: DB_NAME
        # value: db_name
        sync: false
      - key: DB_TABLE_PREFIX
        # value: alist_
        sync: false
      - key: CDN
        # value: https://npm.elemecdn.com/alist-web@$version/dist
        sync: false
