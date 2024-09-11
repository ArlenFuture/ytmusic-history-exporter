# YouTube Music History Exporter

**ytmusic-history-exporter** 是一個簡單的工具，用於從 YouTube Music 的播放紀錄頁面中擷取歌曲標題和網址，並將結果保存為 JSON 文件。

## 功能

- 擷取 YouTube Music 播放紀錄中的歌曲標題和網址
- 生成 JSON 格式的下載文件

## 使用說明

1. 打開 [YouTube Music 播放紀錄頁面](https://music.youtube.com/history)（確保你已經登入並且播放紀錄已經載入）。

2. 打開瀏覽器的開發者工具（按 `F12` 或 `Ctrl+Shift+I` / `Cmd+Option+I`）。

3. 切換到「Console」面板。

4. 將以下程式碼複製並貼上到控制台中，然後按 Enter：

   ```javascript
   // 選擇所有符合條件的 <a> 元素
   const linkElements = document.querySelectorAll('a.yt-simple-endpoint.style-scope.yt-formatted-string');

   // 提取標題和網址
   const songs = Array.from(linkElements).map(linkElement => {
       return {
           title: linkElement.textContent.trim(),  // 擷取歌曲標題
           url: linkElement.href                    // 擷取網址
       };
   });

   // 將結果轉換為 JSON 字串
   const jsonOutput = JSON.stringify(songs, null, 2);  // `null` 和 `2` 用於格式化輸出，使其更易讀

   // 建立 Blob 物件
   const blob = new Blob([jsonOutput], { type: 'application/json' });

   // 建立下載連結
   const url = URL.createObjectURL(blob);
   const a = document.createElement('a');
   a.href = url;
   a.download = 'songs.json';  // 文件名
   a.textContent = 'Download JSON';

   // 自動點擊下載連結
   a.click();

   // 清理 URL 對象
   URL.revokeObjectURL(url);
   ```
## 注意事項
- 請確保你的播放紀錄頁面已經載入完畢，並且播放紀錄已經顯示在頁面上。
- 本工具僅用於個人用途，不保證與 YouTube Music 未來版本的相容性。

## 貢獻
歡迎提交問題報告和功能請求。如果你有任何改進建議，請發送拉取請求。

## 授權
這個專案使用 MIT License 授權。詳情請參閱 LICENSE 文件。
