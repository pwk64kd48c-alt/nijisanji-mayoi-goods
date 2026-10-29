
<!DOCTYPE html>
<html lang="ja">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1">
<title>にじさんじ｜迷子グッズ</title>
<style>
*{box-sizing:border-box}
:root{--bg:#f5f5f5;--line:#e5e5e5;--text:#444;--sub:#999}
body{margin:0;background:var(--bg);color:var(--text);font-family:-apple-system,BlinkMacSystemFont,"Helvetica Neue",sans-serif;font-size:14px}
header{background:white;text-align:center;padding:26px 14px 20px;border-bottom:1px solid var(--line)}
header h1{font-size:23px;letter-spacing:3px;margin:0 0 8px}
header p{font-size:10px;color:var(--sub);letter-spacing:2px;margin:0}
main{max-width:900px;margin:auto;padding:15px}
.panel{background:#fff;border:1px solid var(--line);border-radius:12px;padding:15px;margin-bottom:15px}
h2{font-size:15px;margin:0 0 14px;font-weight:600}
h3{font-size:13px;margin:16px 0 9px}
label{display:block;font-size:12px;color:#777;margin-bottom:6px}
input,select,textarea{width:100%;min-width:0;padding:11px;border:1px solid #ddd;border-radius:7px;background:#fff;color:#444;font-size:14px}
input:focus,select:focus,textarea:focus{outline:none;border-color:#999}
input[type=checkbox]{width:auto}
button{border:1px solid #ddd;border-radius:7px;padding:10px 12px;background:white;color:#555;font-size:12px;cursor:pointer}
button:active{opacity:.65}
.primary{background:#555;color:white;border-color:#555}
.small{padding:6px 9px;font-size:11px}
.danger{color:#999}
.field{margin-bottom:13px}
.row{display:flex;gap:8px;align-items:center}
.row input,.row select{flex:1;min-width:0}
.row button{flex-shrink:0}
.hint{font-size:11px;color:#999;line-height:1.8}
.chips{display:flex;flex-wrap:wrap;gap:7px;margin-top:12px}
.chip{display:flex;align-items:center;gap:7px;background:#f6f6f6;border:1px solid #e2e2e2;border-radius:20px;padding:7px 10px;font-size:12px}
.chip button{padding:0;border:0;background:transparent;color:#999}
.filters{display:grid;grid-template-columns:1fr 1fr;gap:10px}
.wide{grid-column:1/-1}
.checkline{display:flex;align-items:center;gap:8px;margin:12px 0}
.checkline label{margin:0}
#cancelEdit{display:none}
.preview{margin-top:8px}
.preview img{max-width:140px;max-height:140px;object-fit:contain}
.count{font-size:12px;color:#999;margin:14px 0}
.goods-grid{display:grid;grid-template-columns:repeat(2,minmax(0,1fr));gap:11px}
.goods-card{background:white;border:1px solid var(--line);border-radius:10px;overflow:hidden;min-width:0}
.goods-image{aspect-ratio:1/1;background:#f1f1f1;display:flex;align-items:center;justify-content:center;color:#aaa;overflow:hidden}
.goods-image img{width:100%;height:100%;object-fit:contain}
.goods-info{padding:10px}
.goods-group{font-size:10px;color:#999;margin-bottom:4px}
.goods-liver{font-size:12px;color:#777;margin-bottom:5px;overflow-wrap:anywhere}
.goods-name{font-size:14px;font-weight:600;line-height:1.5;overflow-wrap:anywhere}
.goods-type{font-size:11px;color:#999;margin-top:5px}
.goods-quantity{margin-top:7px;font-size:13px}
.exchange{display:inline-block;margin-top:7px;padding:4px 7px;background:#f1f1f1;border-radius:4px;font-size:10px}
.card-actions{display:flex;gap:5px;margin-top:10px}
.card-actions button{flex:1;padding:8px 2px}
.empty{grid-column:1/-1;text-align:center;padding:35px 10px;background:white;border:1px dashed #ddd;border-radius:10px;color:#aaa;line-height:2}
footer{text-align:center;color:#aaa;font-size:10px;padding:22px}
@media(min-width:600px){.goods-grid{grid-template-columns:repeat(3,minmax(0,1fr))}main{padding:22px}}
</style>
</head>
<body>
<header>
  <h1>迷子グッズ</h1>
  <p>NIJISANJI GOODS MANAGEMENT</p>
</header>

<main>
  <section class="panel">
    <h2>グループ管理</h2>
    <div class="row">
      <input id="groupInput" placeholder="グループ名を入力">
      <button class="primary" id="addGroup">追加</button>
    </div>
    <p class="hint">ユニット名やグループ名を自由に登録できるよ。</p>
    <div class="chips" id="groupList"></div>
  </section>

  <section class="panel">
    <h2>ライバー管理</h2>
    <div class="field">
      <label for="liverInput">ライバー名</label>
      <input id="liverInput" placeholder="ライバー名を入力">
    </div>
    <div class="field">
      <label for="liverGroup">所属グループ</label>
      <select id="liverGroup">
        <option value="">グループ未設定・ソロ</option>
      </select>
    </div>
    <button class="primary" id="addLiver">ライバーを追加</button>
    <div class="chips" id="liverList"></div>
  </section>

  <section class="panel" id="formPanel">
    <h2 id="formTitle">グッズ登録</h2>
    <form id="goodsForm">
      <div class="field">
        <label for="gLiver">ライバー</label>
        <select id="gLiver" required>
          <option value="">ライバーを選択</option>
        </select>
      </div>
      <div class="field">
        <label for="gName">グッズ名・絵柄</label>
        <input id="gName" placeholder="例：チェキ 第○弾" required>
      </div>
      <div class="field">
        <label for="gType">グッズ種類</label>
        <select id="gType">
          <option>缶バッジ</option>
          <option>チェキ・カード</option>
          <option>アクリルスタンド</option>
          <option>アクリルキーホルダー</option>
          <option>ブロマイド</option>
          <option>特典</option>
          <option>ぬいぐるみ</option>
          <option>紙類</option>
          <option>その他</option>
        </select>
      </div>
      <div class="field">
        <label for="gQuantity">個数</label>
        <input id="gQuantity" type="number" min="1" value="1" required>
      </div>
      <div class="field">
        <label for="gImage">グッズ画像（任意）</label>
        <input id="gImage" type="file" accept="image/*">
        <div id="imagePreview" class="preview"></div>
        <p class="hint">画像は縮小して保存するよ。編集時に画像を選ばなければ、元の画像を引き継ぐよ。</p>
      </div>
      <div class="checkline">
        <input id="gReexchange" type="checkbox">
        <label for="gReexchange">⭐️ 再交換分</label>
      </div>
      <div class="row">
        <button class="primary" type="submit" id="saveButton">登録する</button>
        <button type="button" id="cancelEdit">キャンセル</button>
      </div>
    </form>
  </section>

  <section class="panel">
    <h2>グッズ一覧</h2>
    <div class="filters">
      <div>
        <label for="filterGroup">グループ</label>
        <select id="filterGroup"><option value="">すべて</option></select>
      </div>
      <div>
        <label for="filterLiver">ライバー</label>
        <select id="filterLiver"><option value="">すべて</option></select>
      </div>
      <div>
        <label for="filterType">グッズ種類</label>
        <select id="filterType">
          <option value="">すべて</option>
          <option>缶バッジ</option>
          <option>チェキ・カード</option>
          <option>アクリルスタンド</option>
          <option>アクリルキーホルダー</option>
          <option>ブロマイド</option>
          <option>特典</option>
          <option>ぬいぐるみ</option>
          <option>紙類</option>
          <option>その他</option>
        </select>
      </div>
      <div>
        <label for="filterExchange">再交換分</label>
        <select id="filterExchange">
          <option value="">すべて</option>
          <option value="yes">⭐️ 再交換分のみ</option>
          <option value="no">再交換分以外</option>
        </select>
      </div>
      <div class="wide">
        <label for="search">キーワード検索</label>
        <input id="search" placeholder="ライバー名・グッズ名">
      </div>
    </div>
    <div class="count" id="count"></div>
    <div class="goods-grid" id="goodsGrid"></div>
  </section>
</main>

<footer>NIJISANJI GOODS · MY LIST</footer>

<script>
const STORAGE_KEY = "nijisanjiMayoiGoodsData_v2";
let data = {groups:[],livers:[],goods:[]};
let editingId = null;
let selectedImage = "";
let imageChanged = false;

const $ = id => document.getElementById(id);
const makeId = () => Date.now().toString(36)+Math.random().toString(36).slice(2,8);

function esc(value){
  return String(value ?? "").replace(/[&<>"']/g,c=>({
    "&":"&amp;","<":"&lt;",">":"&gt;",'"':"&quot;","'":"&#39;"
  })[c]);
}
function loadData(){
  try{
    const saved=localStorage.getItem(STORAGE_KEY);
    if(saved){
      const d=JSON.parse(saved);
      data.groups=Array.isArray(d.groups)?d.groups:[];
      data.livers=Array.isArray(d.livers)?d.livers:[];
      data.goods=Array.isArray(d.goods)?d.goods:[];
    }
  }catch(e){alert("保存データを読み込めなかったよ。")}
}
function saveData(){
  try{
    localStorage.setItem(STORAGE_KEY,JSON.stringify(data));
    return true;
  }catch(e){
    alert("保存できなかったよ。画像を小さくして再度試してね。");
    return false;
  }
}
function liverById(id){return data.livers.find(x=>x.id===id)}
function groupById(id){return data.groups.find(x=>x.id===id)}
function groupName(liver){
  const g=liver&&groupById(liver.groupId);
  return g?g.name:"グループ未設定";
}
function fillSelect(id,items,firstLabel,selected){
  const el=$(id);
  el.innerHTML=`<option value="">${esc(firstLabel)}</option>`+
    items.map(x=>`<option value="${esc(x.id)}">${esc(x.name)}</option>`).join("");
  if(selected && items.some(x=>x.id===selected))el.value=selected;
}
function render(){
  renderGroups();
  renderLivers();
  renderSelects();
  renderGoods();
}
function renderGroups(){
  $("groupList").innerHTML=data.groups.length?data.groups.map(g=>`
    <div class="chip">
      <span>${esc(g.name)}</span>
      <button type="button" data-action="delete-group" data-id="${esc(g.id)}" aria-label="削除">×</button>
    </div>`).join(""):'<span class="hint">グループはまだ登録されていないよ。</span>';
}
function renderLivers(){
  $("liverList").innerHTML=data.livers.length?data.livers.map(l=>`
    <div class="chip">
      <span>${esc(l.name)} <span style="color:#999">/ ${esc(groupName(l))}</span></span>
      <button type="button" data-action="edit-liver" data-id="${esc(l.id)}">編集</button>
      <button type="button" data-action="delete-liver" data-id="${esc(l.id)}">×</button>
    </div>`).join(""):'<span class="hint">ライバーはまだ登録されていないよ。</span>';
}
function renderSelects(){
  const oldL=$("gLiver").value;
  const oldGroup=$("filterGroup").value;
  const oldFilterL=$("filterLiver").value;
  const oldEditGroup=$("liverGroup").value;
  fillSelect("liverGroup",data.groups,"グループ未設定・ソロ",oldEditGroup);
  fillSelect("gLiver",data.livers,"ライバーを選択",oldL);
  fillSelect("filterGroup",data.groups,"すべて",oldGroup);
  fillSelect("filterLiver",data.livers,"すべて",oldFilterL);
}
function renderGoods(){
  const groupFilter=$("filterGroup").value;
  const liverFilter=$("filterLiver").value;
  const typeFilter=$("filterType").value;
  const exchangeFilter=$("filterExchange").value;
  const keyword=$("search").value.trim().toLowerCase();

  let list=data.goods.filter(g=>{
    const liver=liverById(g.liverId);
    if(!liver)return false;
    if(groupFilter && liver.groupId!==groupFilter)return false;
    if(liverFilter && liver.id!==liverFilter)return false;
    if(typeFilter && g.type!==typeFilter)return false;
    if(exchangeFilter==="yes"&&!g.reexchange)return false;
    if(exchangeFilter==="no"&&g.reexchange)return false;
    const text=(liver.name+" "+groupName(liver)+" "+g.name+" "+g.type).toLowerCase();
    if(keyword&&!text.includes(keyword))return false;
    return true;
  });

  $("count").textContent=`${list.length} 件 / 合計 ${list.reduce((n,g)=>n+Number(g.quantity||0),0)} 個`;
  $("goodsGrid").innerHTML=list.length?list.map(g=>{
    const liver=liverById(g.liverId);
    return `<article class="goods-card">
      <div class="goods-image">
        ${g.image?`<img src="${g.image}" alt="${esc(g.name)}">`:'画像なし'}
      </div>
      <div class="goods-info">
        <div class="goods-group">${esc(groupName(liver))}</div>
        <div class="goods-liver">${esc(liver.name)}</div>
        <div class="goods-name">${esc(g.name)}</div>
        <div class="goods-type">${esc(g.type)}</div>
        <div class="goods-quantity">個数：${Number(g.quantity)||0}</div>
        ${g.reexchange?'<div class="exchange">⭐️ 再交換分</div>':''}
        <div class="card-actions">
          <button type="button" data-action="edit-good" data-id="${esc(g.id)}">編集</button>
          <button type="button" data-action="delete-good" data-id="${esc(g.id)}">削除</button>
        </div>
      </div>
    </article>`;
  }).join(""):'<div class="empty">グッズはまだ登録されていないよ。<br>上のフォームから登録してね。</div>';
}

$("addGroup").addEventListener("click",()=>{
  const name=$("groupInput").value.trim();
  if(!name){alert("グループ名を入力してね！");return}
  if(data.groups.some(g=>g.name.toLowerCase()===name.toLowerCase())){
    alert("同じグループ名が登録されているよ。");return;
  }
  data.groups.push({id:makeId(),name});
  $("groupInput").value="";
  if(saveData())render();
});
$("groupInput").addEventListener("keydown",e=>{
  if(e.key==="Enter"){e.preventDefault();$("addGroup").click()}
});

let editingLiverId=null;
$("addLiver").addEventListener("click",()=>{
  const name=$("liverInput").value.trim();
  const groupId=$("liverGroup").value;
  if(!name){alert("ライバー名を入力してね！");return}
  if(data.livers.some(l=>l.name.toLowerCase()===name.toLowerCase()&&l.id!==editingLiverId)){
    alert("同じ名前のライバーが登録されているよ。");return;
  }
  if(editingLiverId){
    const l=liverById(editingLiverId);
    if(l){l.name=name;l.groupId=groupId}
    editingLiverId=null;
    $("addLiver").textContent="ライバーを追加";
  }else{
    data.livers.push({id:makeId(),name,groupId});
  }
  $("liverInput").value="";
  $("liverGroup").value="";
  if(saveData())render();
});

$("goodsForm").addEventListener("submit",async e=>{
  e.preventDefault();
  const liverId=$("gLiver").value;
  const name=$("gName").value.trim();
  const quantity=Number($("gQuantity").value);
  if(!liverById(liverId)){alert("ライバーを選択してね！");return}
  if(!name||!Number.isFinite(quantity)||quantity<1){alert("グッズ名と個数を確認してね！");return}
  let image=selectedImage;
  const file=$("gImage").files[0];
  if(file){
    try{image=await resizeImage(file)}catch(err){
      alert("画像を読み込めなかったよ。別の画像で試してね。");return;
    }
  }
  const item={
    id:editingId||makeId(),liverId,name,
    type:$("gType").value,quantity,
    image:image||"",reexchange:$("gReexchange").checked
  };
  if(editingId){
    const index=data.goods.findIndex(g=>g.id===editingId);
    if(index>=0)data.goods[index]=item;
  }else data.goods.unshift(item);
  if(saveData()){
    resetForm();
    render();
    $("formPanel").scrollIntoView({behavior:"smooth",block:"start"});
  }
});
function resizeImage(file){
  return new Promise((resolve,reject)=>{
    const reader=new FileReader();
    reader.onerror=reject;
    reader.onload=()=>{
      const img=new Image();
      img.onerror=reject;
      img.onload=()=>{
        const max=700;
        const scale=Math.min(1,max/Math.max(img.width,img.height));
        const canvas=document.createElement("canvas");
        canvas.width=Math.max(1,Math.round(img.width*scale));
        canvas.height=Math.max(1,Math.round(img.height*scale));
        canvas.getContext("2d").drawImage(img,0,0,canvas.width,canvas.height);
        resolve(canvas.toDataURL("image/jpeg",0.78));
      };
      img.src=reader.result;
    };
    reader.readAsDataURL(file);
  });
}
$("gImage").addEventListener("change",()=>{
  const file=$("gImage").files[0];
  if(file){
    const url=URL.createObjectURL(file);
    $("imagePreview").innerHTML=`<img src="${url}" alt="画像プレビュー">`;
  }else{
    $("imagePreview").innerHTML=selectedImage?`<img src="${selectedImage}" alt="登録済み画像">`:"";
  }
});
function resetForm(){
  editingId=null;selectedImage="";imageChanged=false;
  $("goodsForm").reset();
  $("gQuantity").value=1;
  $("imagePreview").innerHTML="";
  $("formTitle").textContent="グッズ登録";
  $("saveButton").textContent="登録する";
  $("cancelEdit").style.display="none";
  $("gImage").value="";
}
$("cancelEdit").addEventListener("click",resetForm);

document.addEventListener("click",e=>{
  const btn=e.target.closest("button[data-action]");
  if(!btn)return;
  const id=btn.dataset.id;
  const action=btn.dataset.action;

  if(action==="delete-group"){
    const g=groupById(id);
    if(!g||!confirm(`「${g.name}」を削除する？\n所属ライバーはグループ未設定になるよ。`))return;
    data.groups=data.groups.filter(x=>x.id!==id);
    data.livers.forEach(l=>{if(l.groupId===id)l.groupId=""});
    if(saveData())render();
  }
  if(action==="edit-liver"){
    const l=liverById(id);if(!l)return;
    editingLiverId=id;
    $("liverInput").value=l.name;
    $("liverGroup").value=l.groupId||"";
    $("addLiver").textContent="ライバーを更新";
    $("liverInput").scrollIntoView({behavior:"smooth",block:"center"});
    $("liverInput").focus();
  }
  if(action==="delete-liver"){
    const l=liverById(id);if(!l)return;
    if(!confirm(`「${l.name}」と登録済みグッズを削除する？`))return;
    data.livers=data.livers.filter(x=>x.id!==id);
    data.goods=data.goods.filter(x=>x.liverId!==id);
    if(saveData())render();
  }
  if(action==="edit-good"){
    const g=data.goods.find(x=>x.id===id);if(!g)return;
    editingId=id;selectedImage=g.image||"";
    $("gLiver").value=g.liverId;
    $("gName").value=g.name;
    $("gType").value=g.type;
    $("gQuantity").value=g.quantity;
    $("gReexchange").checked=!!g.reexchange;
    $("gImage").value="";
    $("imagePreview").innerHTML=selectedImage?`<img src="${selectedImage}" alt="登録済み画像">`:"";
    $("formTitle").textContent="グッズ編集";
    $("saveButton").textContent="変更を保存";
    $("cancelEdit").style.display="block";
    $("formPanel").scrollIntoView({behavior:"smooth",block:"start"});
  }
  if(action==="delete-good"){
    const g=data.goods.find(x=>x.id===id);if(!g)return;
    if(!confirm(`「${g.name}」を削除する？`))return;
    data.goods=data.goods.filter(x=>x.id!==id);
    if(saveData())render();
  }
});

["filterGroup","filterLiver","filterType","filterExchange"].forEach(id=>{
  $(id).addEventListener("change",()=>{
    if(id==="filterGroup"){
      const groupId=$("filterGroup").value;
      const liverSelect=$("filterLiver");
      const previous=liverSelect.value;
      const livers=groupId?data.livers.filter(l=>l.groupId===groupId):data.livers;
      fillSelect("filterLiver",livers,"すべて",previous);
    }
    renderGoods();
  });
});
$("search").addEventListener("input",renderGoods);

loadData();
render();
</script>
</body>
</html>
