<!DOCTYPE html>
<html lang="pt-br">

<head>

<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">

<title>IC ARTES Comunicação Visual</title>

<style>

*{
    margin:0;
    padding:0;
    box-sizing:border-box;
    font-family:Arial, Helvetica, sans-serif;
}

body{
    background:#050505;
    color:white;
    overflow:hidden;
}

.container{
    display:flex;
    height:100vh;
}

/* SIDEBAR */

.sidebar{
    width:390px;
    background:linear-gradient(180deg,#0a0a0a,#111827);
    border-right:1px solid #222;
    padding:20px;
    overflow:auto;
}

.logo h1{
    font-size:45px;
    font-weight:900;
}

.logo span{
    color:#ffd000;
}

.logo p{
    color:#aaa;
    margin-top:5px;
}

.titulo{
    margin-top:25px;
    margin-bottom:20px;
    color:#ffd000;
    font-size:28px;
    font-weight:bold;
}

.label{
    display:block;
    margin-top:15px;
    margin-bottom:8px;
    font-size:16px;
}

.sidebar input,
.sidebar textarea,
.select{
    width:100%;
    padding:14px;
    border:none;
    border-radius:12px;
    font-size:16px;
    background:#1f2937;
    color:white;
}

.sidebar textarea{
    min-height:180px;
    resize:none;
}

.btn{
    width:100%;
    padding:15px;
    border:none;
    border-radius:12px;
    margin-top:15px;
    cursor:pointer;
    font-size:17px;
    font-weight:bold;
    transition:0.2s;
}

.btn:hover{
    transform:scale(1.02);
}

.btn-add{
    background:#ffd000;
    color:black;
}

.btn-clear{
    background:#374151;
    color:white;
}

.btn-print{
    background:#0f9d58;
    color:white;
}

/* LISTA */

.lista-titulo{
    margin-top:30px;
    margin-bottom:15px;
    color:#ffd000;
    font-size:24px;
    font-weight:bold;
}

.lista{
    display:flex;
    flex-direction:column;
    gap:12px;
}

.item{
    background:#111827;
    border:1px solid #333;
    border-radius:14px;
    padding:12px;
    display:flex;
    align-items:center;
    gap:12px;
}

.thumb{
    width:70px;
    height:100px;
    background:white;
    border-radius:8px;
    overflow:hidden;
    flex-shrink:0;
}

.thumb-top{
    background:red;
    color:#ffe066;
    text-align:center;
    font-size:13px;
    font-weight:bold;
    padding:5px;
}

.thumb-preco{
    text-align:center;
    color:red;
    font-size:24px;
    font-weight:900;
    margin-top:25px;
}

.info{
    flex:1;
}

.info h3{
    font-size:18px;
    margin-bottom:5px;
}

.info p{
    color:#ffd000;
    font-size:22px;
    font-weight:bold;
}

.info span{
    color:#aaa;
    font-size:14px;
}

.acoes{
    display:flex;
    flex-direction:column;
    gap:8px;
}

.icon{
    width:38px;
    height:38px;
    background:#1f2937;
    border-radius:10px;
    display:flex;
    justify-content:center;
    align-items:center;
    cursor:pointer;
}

/* PREVIEW */

.preview{
    flex:1;
    padding:20px;
    overflow:auto;
}

.preview h2{
    color:#ffd000;
    margin-bottom:20px;
    font-size:34px;
}

.grid{
    display:flex;
    flex-wrap:wrap;
    gap:20px;
    justify-content:center;
}

/* CARTAZ */

.cartaz{
    background:white;
    position:relative;
    overflow:hidden;
    border
