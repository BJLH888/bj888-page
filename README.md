<!DOCTYPE html>
<html lang="zh-CN">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>全能体育</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
            font-family: "Microsoft YaHei", sans-serif;
        }

        body {
            background: #f5f7fa;
            padding: 20px;
        }

        /* 顶部账户栏 */
        .top-bar {
            background: #fff;
            padding: 20px 30px;
            border-radius: 12px;
            box-shadow: 0 2px 8px rgba(0,0,0,0.05);
            display: flex;
            justify-content: space-between;
            align-items: center;
            margin-bottom: 25px;
            flex-wrap: wrap;
            gap: 15px;
        }

        .balance-item {
            font-size: 15px;
            color: #333;
        }

        .balance-item span {
            font-weight: bold;
            color: #e64340;
            margin-left: 5px;
        }

        .view-switch {
            display: flex;
            gap: 8px;
        }

        .view-btn {
            padding: 8px 25px;
            border: none;
            border-radius: 6px;
            cursor: pointer;
            font-size: 14px;
        }

        .view-btn.pc {
            background: #2563eb;
            color: white;
        }

        .view-btn.h5 {
            background: #e5e7eb;
            color: #333;
        }

        .action-buttons {
            display: flex;
            gap: 10px;
        }

        .action-btn {
            padding: 10px 25px;
            border: none;
            border-radius: 6px;
            color: white;
            font-size: 15px;
            cursor: pointer;
            text-decoration: none;
            display: inline-block;
            text-align: center;
        }

        .deposit { background: #2563eb; }
        .withdraw { background: #16a34a; }
        .refresh { background: #f97316; }

        /* 模块网格 */
        .grid-container {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(220px, 1fr));
            gap: 20px;
        }

        .grid-card {
            background: #fff;
            border-radius: 12px;
            padding: 30px 20px;
            text-align: center;
            box-shadow: 0 2px 8px rgba(0,0,0,0.05);
            cursor: pointer;
            transition: transform 0.2s;
        }

        .grid-card:hover {
            transform: translateY(-3px);
        }

        .card-icon {
            font-size: 45px;
            margin-bottom: 15px;
        }

        .card-title {
            font-size: 16px;
            color: #333;
            margin-bottom: 8px;
        }

        .card-value {
            font-size: 14px;
            color: #888;
        }

        /* 背景色区分 */
        .bg-1 { background: #fff7ed; }
        .bg-2 { background: #eff4ff; }
        .bg-3 { background: #f0fdf4; }
        .bg-4 { background: #fdf4ff; }
        .bg-5 { background: #fef2f7; }
        .bg-6 { background: #fefce8; }
        .bg-7 { background: #eef7ff; }
        .bg-8 { background: #fffbeb; }

        /* 跳转页面样式 */
        .page-container {
            display: none;
            background: #fff;
            padding: 30px;
            border-radius: 12px;
            box-shadow: 0 2px 8px rgba(0,0,0,0.05);
        }

        .page-container.active {
            display: block;
        }

        .back-btn {
            background: #e5e7eb;
            border: none;
            padding: 1px 25px;
            border-radius: 6px;
            cursor: pointer;
            font-size: 15px;
            margin-bottom: 25px;
        }

        .page-title {
            font-size: 20px;
            margin-bottom: 25px;
            color: #333;
        }

        .payment-grid {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(140px, 1fr));
            gap: 15px;
        }

        .payment-item {
            border: 1px solid #e5e7eb;
            border-radius: 8px;
            padding: 15px;
            text-align: center;
            cursor: pointer;
            transition: all 0.2s;
        }

        .payment-item:hover, .payment-item.active {
            border-color: #2563eb;
            background: #eff6ff;
        }

        .payment-tag {
            background: #ef4444;
            color: white;
            font-size: 11px;
            padding: 2px 6px;
            border-radius: 4px;
            display: inline-block;
            margin-bottom: 8px;
        }

        .withdraw-tabs {
            display: flex;
            gap: 10px;
            margin-bottom: 25px;
            flex-wrap: wrap;
        }

        .withdraw-tab {
            padding: 10px 20px;
            border: 1px solid #d1d5db;
            background: white;
            border-radius: 6px;
            cursor: pointer;
            font-size: 14px;
        }

        .withdraw-tab.active {
            border-color: #2563eb;
            background: #eff6ff;
            color: #2563eb;
        }
    </style>
</head>
<body>
    <!-- 主页面 -->
    <div id="main-page">
        <div class="top-bar">
            <div class="balance-item">
                账户总额：<span>0.00</span>
                &nbsp;&nbsp;现金额度：<span>0.00</span>
                &nbsp;&nbsp;钱包额度：<span>0.00</span>
            </div>
            <div class="view-switch">
                <button class="view-btn pc">PC</button>
                <button class="view-btn h5">H5</button>
            </div>
            <div class="action-buttons">
                <a class="action-btn deposit" onclick="showPage('deposit-page')">存款</a>
                <a class="action-btn withdraw" onclick="showPage('withdraw-page')">取款</a>
                <a class="action-btn refresh" onclick="location.reload()">刷新</a>
            </div>
        </div>

        <div class="grid-container">
            <div class="grid-card bg-1">
                <div class="card-icon">💰</div>
                <div class="card-title">钱包驻留金额</div>
                <div class="card-value">0.00</div>
            </div>
            <div class="grid-card bg-2">
                <div class="card-icon">⚽</div>
                <div class="card-title">体育</div>
                <div class="card-value">0.00</div>
            </div>
            <div class="grid-card bg-3">
                <div class="card-icon">🎲</div>
                <div class="card-title">真人</div>
                <div class="card-value">0.00</div>
            </div>
            <div class="grid-card bg-4">
                <div class="card-icon">🀄</div>
                <div class="card-title">棋牌</div>
                <div class="card-value">0.00</div>
            </div>
            <div class="grid-card bg-5">
                <div class="card-icon">⚔️</div>
                <div class="card-title">电竞</div>
                <div class="card-value">0.00</div>
            </div>
            <div class="grid-card bg-6">
                <div class="card-icon">🎫</div>
                <div class="card-title">彩票</div>
                <div class="card-value">0.00</div>
            </div>
            <div class="grid-card bg-7">
                <div class="card-icon">🐟</div>
                <div class="card-title">电游</div>
                <div class="card-value">0.00</div>
            </div>
            <div class="grid-card bg-8">
                <div class="card-icon">🦁</div>
                <div class="card-title">老虎机</div>
                <div class="card-value">0.00</div>
            </div>
        </div>
    </div>

    <!-- 存款页面 -->
    <div id="deposit-page" class="page-container">
        <button class="back-btn" onclick="showPage('main-page')">← 返回</button>
        <h2 class="page-title">存款方式</h2>
        <div class="payment-grid">
            <div class="payment-item">
                <span class="payment-tag">加送0.3%</span>
                <div>快捷虚拟币</div>
            </div>
            <div class="payment-item">
                <span class="payment-tag">推荐</span>
                <div>EB直充</div>
            </div>
            <div class="payment-item">
                <span class="payment-tag">加送0.3%</span>
                <div>EBpay虚拟币</div>
            </div>
            <div class="payment-item">
                <span class="payment-tag">推荐</span>
                <div>EBpay</div>
            </div>
            <div class="payment-item">
                <span class="payment-tag">推荐</span>
                <div>支付宝支付宝</div>
            </div>
            <div class="payment-item">
                <div>支付宝零钱</div>
            </div>
            <div class="payment-item">
                <div>云闪付零钱</div>
            </div>
            <div class="payment-item">
                <span class="payment-tag">推荐</span>
                <div>微信零钱</div>
            </div>
            <div class="payment-item">
                <span class="payment-tag">推荐</span>
                <div>支付宝速存</div>
            </div>
            <div class="payment-item">
                <div>支付宝</div>
            </div>
            <div class="payment-item">
                <div>云闪付转卡</div>
            </div>
            <div class="payment-item">
                <div>微信转卡</div>
            </div>
            <div class="payment-item">
                <div>京东转卡</div>
            </div>
            <div class="payment-item">
                <div>数字人民币</div>
            </div>
            <div class="payment-item">
                <div>支付宝H5</div>
            </div>
            <div class="payment-item">
                <div>网银转账</div>
            </div>
            <div class="payment-item">
                <div>U卡支付</div>
            </div>
            <div class="payment-item">
                <div>icash.one</div>
            </div>
            <div class="payment-item">
                <div>HK转数快</div>
            </div>
        </div>
    </div>

    <!-- 取款页面 -->
    <div id="withdraw-page" class="page-container">
        <button class="back-btn" onclick="showPage('main-page')">← 返回</button>
        <h2 class="page-title">取款方式</h2>
        <div class="withdraw-tabs">
            <button class="withdraw-tab">微信取款</button>
            <button class="withdraw-tab active">EBpay提币(即时到账)</button>
            <button class="withdraw-tab">数字人民币取款</button>
            <button class="withdraw-tab">极速取款</button>
            <button class="withdraw-tab">支付宝取款</button>
        </div>
        <div style="margin-top: 20px; color: #666;">
            <p>到账EBpay地址：</p>
            <p style="margin-top: 10px; padding: 12px; background: #f9fafb; border-radius: 6px;">请输入地址...</p>
        </div>
    </div>

    <script>
        // 页面切换函数
        function showPage(pageId) {
            // 隐藏所有页面
            document.querySelectorAll('.page-container').forEach(p => {
                p.classList.remove('active');
            });
            // 显示主页面或指定页面
            if (pageId === 'main-page') {
                document.getElementById('main-page').style.display = 'block';
            } else {
                document.getElementById('main-page').style.display = 'none';
                document.getElementById(pageId).classList.add('active');
            }
        }
    </script>
</body>
</html>
