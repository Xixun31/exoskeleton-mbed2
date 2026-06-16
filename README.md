## 🐧 Ubuntu 開發流程 (實驗室機台)

### 建立新實驗資料夾 (以 labx 為例)
```
mkdir labx
cd labx
```

### 建立 Mbed OS 連結與複製必要設定
```
ln -s ../mbed-os .
cp ../Document/CMakeLists.txt .
cp ../Document/mbed_app.json5 .
code main.cpp
```

### 編譯與燒錄 (Compile & Flash)
```
mkdir build && cd build
cmake .. -GNinja -DMBED_TARGET=NUCLEO_F446RE
```

### 使用 Ninja 進行燒錄
```
sudo ninja flash-MbedCEHelloWorld
```

### 序列埠監控與截圖
```
#Monitor:
sudo microcom --port=/dev/ttyACM0 --speed=115200
#Exit: Ctrl-\ 然後按 Ctrl-C
```
```
#Screenshot:
gnome-screenshot -d 5
#(延遲 5 秒後截圖)
```

### python venv
```
source ~/mbed2/venv/bin/activate
deactivate
```

## 🍎 macOS 開發流程 (個人電腦)

### 建立新實驗資料夾 (以 labx 為例)
```
mkdir labx
cd labx
```

### 建立 Mbed OS 連結與複製必要設定
```
ln -s ../mbed-os .
cp ../Document/CMakeLists.txt .
cp ../Document/mbed_app.json5 .
code main.cpp
```

### 編譯與燒錄 (Compile & Flash)
```
mkdir build && cd build
cmake .. -GNinja -DMBED_TARGET=NUCLEO_F446RE
```

### 在 build 資料夾內執行
```
sudo ninja flash-MbedCEHelloWorld
```

### 手動燒錄 (Flash)
```
cp MbedCEHelloWorld.bin /Volumes/NUCLEO_F446RE/
sync
```

### 序列埠監控 (Serial Port) 確認裝置名稱
```
ls /dev/cu.usbmodem*
```

### 使用 minicom 連線 (請根據 ls 結果修改 modem 編號)
```
minicom -D /dev/cu.usbmodem1103 -b 115200
```

### python venv
```
source ~/mbed2/venv/bin/activate
deactivate
```

## ⚙️ Mbed OS 設定檔與 VS Code Snippets 說明

### Mbed 應用程式設定 (mbed_app.json5)
在專案目錄下創建的 `mbed_app.json5` 主要用來設定硬體參數與編譯模式：
```json5
{
    "target_overrides": {
        "*": {
            // 預設序列埠傳輸率為 115200
            "platform.stdio-baud-rate": 115200,
            "platform.stdio-buffered-serial": 1
        },
        "NUCLEO_F446RE": {
            // NUCLEO_F446RE 預設使用完整 RTOS 模式。若要改用裸機模式以加速編譯與減小體積，可取消註解下行：
            // "target.application-profile": "bare-metal"
        }
    }
}
```

### 💡 VS Code 快速程式碼片段 (Snippets)
為了方便快速建立專案，已在 VS Code 中設定了兩個快捷 Snippets。在空白檔案中輸入對應的 `Prefix` 並按下 `Tab` 或 `Enter` 即可展開模板：

1. **`CMakeLists.txt` 快速生成**
   * **Prefix**: `mbed-cmake`
   * **功能**：一鍵生成 `CMakeLists.txt` 完整模板，展開後只需輸入**專案名稱**（如 `lab1`）即可。

2. **`mbed_app.json5` 快速生成**
   * **Prefix**: `mbed-app`
   * **功能**：一鍵生成上述預設包含 `NUCLEO_F446RE` 的 `mbed_app.json5` 設定模板。

# exoskeleton-mbed2
# exoskeleton-mbed2
