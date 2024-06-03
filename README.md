### 使用Windows WSL來安裝Ollama 3與open-webui

本範例會將Ollama 3安裝在Windows的WSL裡，並使用WSL中的docker安裝open-webui並以port 8888對外連線

#### 安裝Ollama 3

1. 在windows開啟命令提示字元或終端機
2. 輸入`wsl`進入WSL系統，我的WSL版本是`Ubuntu 22.04`
3. Ollama 3官網有提供安裝指令，指令為`curl -fsSL https://ollama.com/install.sh | sh`
4. 安裝完畢後，執行`sudo systemctl status ollama`確認服務執行狀態
5. 呼叫'curl http://localhost:11434' 確認ollama是否可正確回應，應該要回應`Ollama is running`

#### 安裝Open-webui

1. docker指令：`docker run --network host -d -e PORT=8888 -e OLLAMA_BASE_URL=http://127.0.0.1:11434 -v open-webui:/app/backend/data --name open-webui --restart always ghcr.io/open-webui/open-webui:main`
2. 打開瀏覽器，輸入網址：`http://localhost:8888`，應該會開啟open webui的登入畫面
3. 依照此Youtube影片設定與使用：`https://youtu.be/JpQC0W91E6k?si=cfjHuaEtUUMvAMER`