# docker-compose configuration to run OverLeaf(sharelatex) community edition

기본적으로 제공되는 [overleaf/overleaf](https://github.com/overleaf/overleaf) 저장소 내 docker-compose.yml 파일이 올바르게 동작하지 않아서, overleaf 5.1 버전(2024/08 기준)에서 잘 동작하게 수정한 docker-compose 설정 파일.

### 사용 방법
1. Build dgr_overleaf_full(change name what you want!) docker image from sharelatex/sharelatex official overleaf docker image
```
# clone github repository
git clone https://github.com/dalgarak/overleaf_community_docker $HOME/overleaf-docker

# change directory to build texlive full-scheme overleaf image
cd overleaf-docker/full-texlive
# build overleaf docker image with texlive full-scheme
./build.sh
```

2. To launch overleaf+mongodb v6+redis, just run following commands:
```
cd $HOME/overleaf-docker
# change overleaf http port configuration (default: 9080) in docker-compose.yml
# then launch docker-compose
./launch.sh
```

3. if you want to stop docker-compose, just execute following commands:
```
cd $HOME/overleaf-docker
docker-compose down
```

### acknowledgement
 * This repository contains [laekov/panleaf](https://github.com/laekov/panleaf) codes, which distributed under Apache-2.0 License. Copyright 2021, laekov., All rights reserved.
