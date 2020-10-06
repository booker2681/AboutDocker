# AboutDocker

實驗室的dockerfile
> ### 目前建議使用 docker-for-ai-dev
[docker-for-ai-dev 指令產生器](https://p208p2002.github.io/docker-for-ai-dev/)

# Usage
* ubuntu 16.04
  * docker pull harryzhan/udic_ub16_ssh 
  * docker run -idt -p "ssh的port":22 --name "你的名稱" harryzhan/udic_ub16_ssh
  * docker exec -ti "你的名稱" bash (進入container)
  * passwd (建立root密碼)
  * ----即可遠端登入 使用者名稱為root----
  *  ./createDocker_harry.sh  (快速建立方法) (記得先修改檔案權限 chmod 777)
  *  (遇到 Text file busy 問題 用vim開啟檔案輸入 :set ff=unix 變更文件格式)

* nvidia docker
  * 目前有三個版本如下:
  * harryzhan/udic_nvidia_docker (tensorflow1.0) 大學長始祖版 未來可能不在維護 
  * udiclab/udic_nvidia_docker:tf1.15_torch1.3 (tensorflow1.5 & pytorch1.3) 實驗室目前預設版
* nvidia docker 使用
  * docker pull udiclab/udic_nvidia_docker 視需求與版本
  * sudo nvidia-docker run -itd -p $USER_PORT:22 -p $NOTEBOOK_PORT:8888 -p $TENSORBOARD_PORT:6006 --name "你的名稱" --hostname "你的名稱 "udiclab/udic_nvidia_docker
  * docker exec -ti "你的名稱" bash (進入container)
  * passwd (建立root密碼)
  * ----即可遠端登入 使用者名稱為root----
  *  ./createNvidiaDocker_udiclab.sh  (快速建立方法) (記得先修改檔案權限 chmod 777)
  *  (遇到 Text file busy 問題 用vim開啟檔案輸入 :set ff=unix 變更文件格式)
  
* volume (container 使用外部資料夾)
  * docker run -v 'outerdir':'innerdir'


# Docker Instructions
* docker ps -a (查看所有container)
* docker ps (查看開啟中的container)
* docker start "你的名稱" (啟動)
* docker stop "你的名稱" (停止)
* docker rm "你的名稱" (刪除)
* docker stats (查看container資源狀態)
* docker ps -a -s (查看每個container硬碟使用量)
* docker system df (查看container可清理的硬碟量)
* docker system prune -a (可清理一些沒使用的image與關閉的container)
* docker rm -v $(docker ps -a -q -f status=exited) (删除沒有開啟的container)
* docker volume rm $(docker volume ls -qf dangling=true) (刪除沒有掛載的volume)

# Docker Image
* docker pull 名稱 (下載image)
* docker build . -t 你的名稱(建立image)
* docker images (查看所有image)
* docker rmi 名稱(刪除image)
* docker rmi $(docker images --quiet --filter "dangling=true") (刪除所有none的)
* docker login (登入docker hub)
* docker push 名稱 (將image上傳到hub上)

# Docker Change Port
* ###必須關閉docker 才能有效###
* step1: 查看container ID
  * docker inspect "name"
* step2: 關閉docker
  * sudo service docker stop
* step3: 修改config.v2.json、hostconfig.json裡的port資訊
  * vim /var/lib/docker/containers/"container ID"/config.v2.json
  * vim /var/lib/docker/containers/"container ID"/hostconfig.json
* step4: 重啟docker
  * sudo service docker start

[Docker Change Port Mapping for an Existing Container](https://mybrainimage.wordpress.com/2017/02/05/docker-change-port-mapping-for-an-existing-container/)

[Tensorflow GPU setup on ubuntu 16.04](https://gist.github.com/theshaneyu/d9eda9f6f4fd9c8f4c75a4546f170a4e)

[Tensorflow GPU setup on ubuntu 18.04](https://gist.github.com/booker2681/80678885f1328be56399c701ea7af2c2)
