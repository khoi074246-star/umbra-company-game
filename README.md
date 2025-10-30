import zipfile
import os

# Tạo cấu trúc thư mục cho Limbo v1.0
base_dir = '/mnt/data/Limbo_v1.0'
os.makedirs(base_dir, exist_ok=True)
os.makedirs(os.path.join(base_dir, 'assets/characters'), exist_ok=True)
os.makedirs(os.path.join(base_dir, 'assets/audio'), exist_ok=True)
os.makedirs(os.path.join(base_dir, 'data'), exist_ok=True)

# Tạo placeholder nhạc nền loop.mp3 (file rỗng)
with open(os.path.join(base_dir, 'assets/audio/loop.mp3'), 'wb') as f:
    f.write(b'')

# Tạo placeholder index.html với các chức năng cơ bản
index_html_content = """
<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<title>Limbo v1.0</title>
<style>
body { background: #0d0d0d; color: #fff; font-family: Arial; margin:0; padding:0;}
header { background:#1a1a1a; padding:10px; text-align:center; font-size:24px;}
nav { display:flex; justify-content:center; margin:10px;}
button { margin:5px; padding:10px 20px; background:#333; color:#fff; border:none; cursor:pointer;}
#game { padding:20px; text-align:center;}
</style>
</head>
<body>
<header>Limbo v1.0</header>
<nav>
<button onclick="showSection('characters')">Characters</button>
<button onclick="showSection('story')">Story</button>
<button onclick="showSection('shop')">Shop</button>
</nav>
<div id="game">
<p>Welcome to Limbo! Placeholder content.</p>
<div id="section-content"></div>
</div>
<audio id="bgm" src="assets/audio/loop.mp3" loop autoplay></audio>
<script>
function showSection(sec){
  document.getElementById('section-content').innerHTML = '<p>Loading '+sec+'...</p>';
}
</script>
</body>
</html>
"""

with open(os.path.join(base_dir, 'index.html'), 'w', encoding='utf-8') as f:
    f.write(index_html_content)

# Tạo placeholder JSON files
with open(os.path.join(base_dir, 'data/sinners.json'), 'w', encoding='utf-8') as f:
    f.write('{"sinners":[]}')

with open(os.path.join(base_dir, 'data/cantos.json'), 'w', encoding='utf-8') as f:
    f.write('{"cantos":[]}')

with open(os.path.join(base_dir, 'data/shop.json'), 'w', encoding='utf-8') as f:
    f.write('{"shop_items":[]}')

# Nén thành zip
zip_path = '/mnt/data/Limbo_v1.0.zip'
with zipfile.ZipFile(zip_path, 'w', zipfile.ZIP_DEFLATED) as zipf:
    for root, dirs, files in os.walk(base_dir):
        for file in files:
            file_path = os.path.join(root, file)
            arcname = os.path.relpath(file_path, base_dir)
            zipf.write(file_path, arcname)

zip_path
