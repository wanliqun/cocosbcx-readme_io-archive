---
title: "1.2.2 Source Code Compilation"
slug: "122-source-code-compilation"
excerpt: "Cocos-BCX supports Ubuntu 16.04 (xenial)、Ubuntu 18.04 (bionic)、CentOS 7 and MacOS (only for High Sierra version practice test) compiling。\n\nPrerequisites: \nCocos-BCX source code repository：https://github.com/Cocos-BCX/cocos-mainnet\nIf you want to run Ubuntu and CentOS environment in virtual environment，please install docker or vmware \nIf you want to use docker in China，adding registry mirror to improve downlaod speed of image is recommended.\n{\n  \"registry-mirrors\" : [\n    \"https://hub-mirror.c.163.com\",\n    \"http://docker.mirrors.ustc.edu.cn/\",\n    \"https://1nj0zren.mirror.aliyuncs.com/\"\n  ]\n}\nYou may also need sudo permission to install package-dependent software\n\n1. Ubuntu 16.04 \n\nIf you need to run Ubuntu 16.04 under the docker container, please run the following command on the command line:\n\ndocker run -itd -v $(pwd)/cocos-mainnet:/cocos-mainnet --name \ncocosbcx-ubuntu-16.04  ubuntu:16.04 bash\n\n\nIf your server's operating environment is in China, it is recommended that you add the"
hidden: false
createdAt: "2019-06-24T06:44:02.917Z"
updatedAt: "2020-06-01T03:47:31.240Z"
---
To be updated