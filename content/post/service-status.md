+++
title = "システム状況"
date = "2023-12-29"
description = "Service Status"
categories = [
    "サーバー",
]
+++

<style> .success { color: green; } .failure { color: red; } </style>
<nav id=TableOfContents></nav>
<div id="result">現在、確認作業を行っております。しばらくお待ちください。</div>
<ul>
<li>Chrunbits: Special Deals - 3GB GENTLEMAN'S YEARLY VPS<div id="asuhara" class="loading">確認中...</div></li>
<li>MoeCloud: UK CN2 GIA Super, Upsteam: Kirino LLC <div id="kirino" class="loading">確認中...</div></li>
<li>Churros: JPBGP Premium, Upsteam: Akari Networks<div id="akari" class="loading">確認中...</div></li>
</ul>
<p>ここに表示されていない障害がある場合は、<a href=/support>サポート</a>までお問い合わせください。</p>

<script>
function checkWebsite(url, resultElement) {
    resultElement.className = 'loading';

    return fetch(url)
        .then(response => {
            if (response.ok) {
                resultElement.className = 'success';
                resultElement.textContent = '利用可能';
                return true;
            } else {
                resultElement.className = 'failure';
                resultElement.textContent = '機能停止';
                return false;
            }
        })
        .catch(error => {
            resultElement.className = 'failure';
            resultElement.textContent = '機能停止';
            return false;
        });
}


document.addEventListener('DOMContentLoaded', async function () {
    var asuharaElement = document.getElementById('asuhara');
    var kirinoElement = document.getElementById('kirino');
    var akariElement = document.getElementById('akari');
    var resultElement = document.getElementById('result');

    async function checkAllWebsites() {
        try {
            const results = await Promise.all([
                checkWebsite('https://asuhara.eu.org', asuharaElement),
                checkWebsite('https://kirino.asuhara.eu.org', kirinoElement),
                checkWebsite('https://akari.asuhara.eu.org', akariElement)
            ]);

            if (results.every(result => result)) {
                resultElement.textContent = 'すべてのサーバーは正常に稼働しています。';
            } else {
                resultElement.textContent = '一部のサーバーが利用できません。';
            }
        } catch (error) {
            resultElement.textContent = '一部のサーバーが利用できません。';
        }
    }

    await checkAllWebsites();
});


</script>