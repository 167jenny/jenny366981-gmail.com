# jenny366981-gmail.com
<!DOCTYPE html>
<html lang="zh-Hant">
<head>
  <meta charset="UTF-8">
  <title>小蝦時光機｜故事館互動遊戲</title>
  <style>
    body {
      font-family: "Noto Sans TC", sans-serif;
      background: #f0f8ff;
      text-align: center;
      padding: 20px;
    }
    h1 {
      color: #0077aa;
    }
    .container {
      display: flex;
      justify-content: space-around;
      margin-top: 30px;
    }
    .column {
      width: 40%;
      background: #fff;
      border-radius: 10px;
      padding: 20px;
      box-shadow: 0 0 10px #ccc;
    }
    .item {
      margin: 15px;
      cursor: grab;
    }
    .dropzone {
      border: 2px dashed #aaa;
      padding: 30px;
      min-height: 100px;
      margin-bottom: 20px;
    }
    .correct {
      border-color: green;
    }
    .done-btn {
      padding: 10px 20px;
      background-color: #00aa88;
      color: white;
      font-size: 16px;
      border: none;
      border-radius: 6px;
      cursor: pointer;
      display: none;
    }
  </style>
</head>
<body>

  <h1>🕰️ 小蝦時光機</h1>
  <p>幫小蝦把「過去」的農具配對到「現在」的對應工具上吧！</p>

  <div class="container">
    <div class="column" id="past">
      <h2>🪵 過去的物件</h2>
      <img src="old_tool.png" alt="傳統鋤頭" class="item" draggable="true" id="hoe">
      <img src="old_basket.png" alt="竹籃" class="item" draggable="true" id="basket">
      <img src="old_dustpan.png" alt="木畚箕" class="item" draggable="true" id="dustpan">
    </div>
    <div class="column" id="present">
      <h2>🔧 現在的物件</h2>
      <div class="dropzone" data-match="hoe">🛠️ 電動耕耘機</div>
      <div class="dropzone" data-match="dustpan">🪣 塑膠收穫桶</div>
      <div class="dropzone" data-match="basket">📦 現代物流箱</div>
    </div>
  </div>

  <button class="done-btn" id="doneBtn">✅ 任務完成！領取徽章</button>

  <script>
    const items = document.querySelectorAll('.item');
    const dropzones = document.querySelectorAll('.dropzone');
    let matched = 0;

    items.forEach(item => {
      item.addEventListener('dragstart', e => {
        e.dataTransfer.setData("text/plain", item.id);
      });
    });

    dropzones.forEach(zone => {
      zone.addEventListener('dragover', e => e.preventDefault());

      zone.addEventListener('drop', e => {
        e.preventDefault();
        const draggedId = e.dataTransfer.getData("text/plain");
        const matchId = zone.getAttribute('data-match');

        if (draggedId === matchId && !zone.classList.contains('correct')) {
          zone.classList.add('correct');
          zone.innerHTML += ` <span style="color:green;">✔️</span>`;
          matched++;
          document.getElementById(draggedId).style.display = "none";
          if (matched === 3) {
            document.getElementById("doneBtn").style.display = "block";
          }
        } else {
          alert("配對錯囉～再想想看！");
        }
      });
    });
  </script>

</body>
</html>
