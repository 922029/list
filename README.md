<!DOCTYPE html>
<html lang="ja">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>行きたいとこリスト</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            text-align: center;
        }
        ul {
            list-style: none;
            padding: 0;
        }
        li {
            background: #f0f0f0;
            margin: 5px;
            padding: 10px;
            border-radius: 5px;
            display: flex;
            justify-content: space-between;
            align-items: center;
        }
        .add-btn {
            background-color: green;
            color: white;
            border: none;
            padding: 5px 10px;
            cursor: pointer;
            font-size: 16px;
        }
        .remove-btn {
            background-color: transparent;
            color: red;
            border: none;
            font-size: 20px;
            cursor: pointer;
        }
    </style>
</head>
<body>
    <h2>近畿</h2>

    <div class="region">
        <h4>大阪</h4>
        <input type="text" class="placeInput" placeholder="追加する場所を入力">
        <button class="add-btn" onclick="addPlace(this)">追加</button>
        <ul class="placeList" id="osakaList"></ul>
    </div>

    <div class="region">
        <h4>京都</h4>
        <input type="text" class="placeInput" placeholder="追加する場所を入力">
        <button class="add-btn" onclick="addPlace(this)">追加</button>
        <ul class="placeList" id="kyotoList"></ul>
    </div>

    <div class="region">
        <h4>兵庫</h4>
        <input type="text" class="placeInput" placeholder="追加する場所を入力">
        <button class="add-btn" onclick="addPlace(this)">追加</button>
        <ul class="placeList" id="hyogoList"></ul>
    </div>

    <div class="region">
        <h4>奈良</h4>
        <input type="text" class="placeInput" placeholder="追加する場所を入力">
        <button class="add-btn" onclick="addPlace(this)">追加</button>
        <ul class="placeList" id="naraList"></ul>
    </div>

    <div class="region">
        <h4>和歌山</h4>
        <input type="text" class="placeInput" placeholder="追加する場所を入力">
        <button class="add-btn" onclick="addPlace(this)">追加</button>
        <ul class="placeList" id="wakayamaList"></ul>
    </div>

    <script>
        // ページ読み込み時にローカルストレージからリストを復元
        window.onload = function() {
            restoreList("osakaList");
            restoreList("kyotoList");
            restoreList("hyogoList");
            restoreList("naraList");
            restoreList("wakayamaList");
        };

        // 入力した場所をローカルストレージに保存し、リストに追加
        function addPlace(button) {
            const region = button.parentElement;
            const input = region.querySelector(".placeInput");
            const list = region.querySelector(".placeList");
            const placeName = input.value.trim();

            if (placeName === "") return;

            const li = document.createElement("li");
            li.innerHTML = placeName + ' <button class="remove-btn" onclick="removePlace(this)">×</button>';

            list.appendChild(li);
            input.value = "";

            // ローカルストレージに保存
            saveList(list.id);
        }

        // 削除ボタンを押したときにその場所を削除
        function removePlace(button) {
            const list = button.parentElement.parentElement;
            button.parentElement.remove();

            // ローカルストレージに再保存
            saveList(list.id);
        }

        // リストをローカルストレージに保存
        function saveList(listId) {
            const listItems = document.getElementById(listId).getElementsByTagName("li");
            const places = [];
            for (let item of listItems) {
                places.push(item.firstChild.textContent.trim());
            }
            localStorage.setItem(listId, JSON.stringify(places));
        }

        // ローカルストレージからリストを復元
        function restoreList(listId) {
            const savedPlaces = localStorage.getItem(listId);
            if (savedPlaces) {
                const places = JSON.parse(savedPlaces);
                const list = document.getElementById(listId);
                for (let place of places) {
                    const li = document.createElement("li");
                    li.innerHTML = place + ' <button class="remove-btn" onclick="removePlace(this)">×</button>';
                    list.appendChild(li);
                }
            }
        }
    </script>
</body>
</html>
