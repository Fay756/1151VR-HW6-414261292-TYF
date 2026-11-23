遊戲玩法
點擊九宮格任一格，盤子會移動到該格中央
接蘋果 +10 分 
接炸彈 -20 分 
勝利條件: 在時間內達到該關目標分數即過關
失敗: 時間結束時分數未達標，按R重玩本關

步驟
3×3舞台 : 9個Cube組成，中心座標為 (-1~1, 0, -1~1) 
調整相機位置
Directional Light產生陰影:Shadow Type設為Soft Shadows
可移動的盤子BasketController，射線偵測點擊位置並四捨五入到格子中心
保持在舞台範圍內，以Mathf.Clamp將座標限制在 -1~1
掉落物Rigidbody + Collider，Tag 分別為Apple、Bomb
從上往下掉、掉出畫面 Destroy，ItemController以固定速度下落，y < -3 時 Destroy
Prefab 與 Factory，ItemFactory定時、隨機位置產生，依機率產生 Bomb
Interval、Speed、BombRate皆為Inspector可調參數
UI: TextMeshPro 顯示 Score、Timer、Level
Director: GameDirector 更新 UI、接收加分通知、時間到停止遊戲
關卡設計: 4 個關卡，難度逐關提升

運作流程
1. GameDirector開始某一關，把該關的 Interval / Speed / BombRate 傳給ItemFactory
2. ItemFactory依參數在九宮格上方隨機位置產生蘋果或炸彈。
3. 物品往下掉，盤子接到時觸發 OnTriggerEnter，GameDirector加減分
4. 時間結束時GameDirector比對分數與目標，達標進入下一關，未達標則顯示失敗並可重玩。

關卡設計
難度參數集中在GameDirector的Levels陣列，每關可在Inspector調整

各關參數
關卡|秒數|分數目標|間隔|速度|炸彈機率
| Level 1 | 30 秒 | 100 | 1.2 秒 | 4 | 15% |
| Level 2 | 30 秒 | 180 | 0.9 秒 | 5 | 25% |
| Level 3 | 30 秒 | 200 | 0.7 秒 | 7 | 25% |
| Level 4 | 30 秒 | 200 | 0.5 秒 | 8 | 25% |
