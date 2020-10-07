# AboutDocker

# Docker create container
* docker run --restart=always --gpus all -itd -p SSH_PORT:22 -p JUPYTER_PORT:8888 -p VSCODE_PORT:8080 -e"NAME=..." -e"PASSWORD=..." IMAGE (example)
* docker run -v OUTER_DIR:INNER_DIR (container 使用外部資料夾)
* docker run -p OUTER_PORT:INNER_PORT (container 自定義PORT)
* docker run --restart=always (container 自動重啟)
* docker run --gpus all (container 使用GPU資源)
* docker run -e "NAME=..." (container 定義內部環境變數)
* docker run -itd (container 使用標準輸入並在背景執行)

# Docker Instructions
* docker exec -it "你的名稱" bash (使用bash進入container)
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
