### 使用Windows WSL來安裝Ollama 3與open-webui

本範例會將Ollama 3安裝在Windows的WSL裡，並使用WSL中的docker安裝open-webui並以port 8888對外連線

#### 安裝WSL

1. 執行 `wsl install`
2. 進入wsl系統

#### 安裝Docker

1. 執行 `sudo apt update`
2. 執行 `sudo apt upgrade`
3. 執行 `sudo apt-get install ca-certificates curl gnupg`
4. 執行 `sudo install -m 0755 -d /etc/apt/keyrings`
5. 執行 `sudo curl -fsSL https://download.docker.com/linux/ubuntu/gpg -o /etc/apt/keyrings/docker.asc`
6. 執行 `sudo chmod a+r /etc/apt/keyrings/docker.asc`
7. 執行
   
    ```bash
    echo \
    "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.asc] https://download.docker.com/linux/ubuntu \
    $(. /etc/os-release && echo "${UBUNTU_CODENAME:-$VERSION_CODENAME}") stable" | \
    sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
    ```
    
    <aside>
    💡 以上是匯入docker的金鑰資訊
    
    </aside>
    
8. 執行 `sudo apt-get update`
9. 執行 `sudo apt-get install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin`
   
    <aside>
    💡 以上是安裝docker
    
    </aside>
    
10. 執行 `sudo usermod -aG docker {your_login_name}`
11. 執行 `sudo systemctl start docker`
12. 執行 `sudo systemctl enable docker`

#### 安裝Ollama 3

1. 在windows開啟命令提示字元或終端機
2. 輸入`wsl`進入WSL系統，我的WSL版本是`Ubuntu 22.04`
3. Ollama 3官網有提供安裝指令，指令為`curl -fsSL https://ollama.com/install.sh | sh`
4. 安裝完畢後，執行`sudo systemctl status ollama`確認服務執行狀態
5. 呼叫`curl http://localhost:11434` 確認ollama是否可正確回應，應該要回應`Ollama is running`

#### 安裝Open-webui

1. docker指令：`docker run --network host -d -e PORT=8888 -e OLLAMA_BASE_URL=http://127.0.0.1:11434 -v open-webui:/app/backend/data --name open-webui --restart always ghcr.io/open-webui/open-webui:main`
2. 打開瀏覽器，輸入網址：`http://localhost:8888`，應該會開啟open webui的登入畫面
3. 依照此Youtube影片設定與使用：`https://youtu.be/JpQC0W91E6k?si=cfjHuaEtUUMvAMER`
