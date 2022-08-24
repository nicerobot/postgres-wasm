# pg-browser

## Requirements

1. Clone v86 repo, preferably in folder next to this repo(If you have it cloned somewhere else, update paths in build-contianer.js and build-state.js):
```bash
git clone git@github.com:copy/v86.git ../v86
```

Folder structure:

    ..
    ├── pg-browser        # This repo
    │   ├── images        # Linux images
    │   ├── build         
    │   └── ...           # Otjer files
    └── v86

2. In debian run `./build-container.sh` to build the Docker container and v86 images (requires docker)
3. Run `./build-state.js` to build a state image in order to skip the boot process
4. You should see a debian-state-base.bin file in images folder
## To run you have to just serve the static files in this folder:

1. Install http-server:
```bash
npm install http-server -g
```
2. Host static files:
```bash
http-server ./ 
```
3. Access in browser at `http://127.0.0.1:8081/`
4. The /ect/hosts file gets overwritten somewhere in the boot process. I built the image with a working hosts file at /etc/hosts.extra, lets copy that over in the browser terminal:
```bash
cp /etc/hosts.extra /etc/hosts
```
5. Restart postgres now that hosts file is working: 

```bash
service postgresql restart
```
6. Switch to postgres unix user:
```bash
su - postgres
```
7. Run psql:
```bash
psql
```
7. Tada! You should see a working psql terminal

 **_NOTE:_** This is obviously very hacky right now. We should be able to solve the hosts issue and also emulate the first few commansds. Also this is a huge debian image we need to build a small linux build with only the required packages.