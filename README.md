<!DOCTYPE html>
<html lang="zh-CN">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>来自孙涛的跨年祝福</title>
    <style>
        body {
            margin: 0;
            padding: 0;
            background: linear-gradient(135deg, #ff9a9e 0%, #fecfef 99%, #fecfef 100%);
            height: 100vh;
            overflow: hidden; /* 防止弹窗过多导致页面出现滚动条 */
            font-family: "Microsoft YaHei", "Heiti SC", sans-serif;
            user-select: none;
        }

        /* 模拟的弹窗样式 */
        .wish-card {
            position: absolute;
            width: 280px;
            padding: 25px 15px 15px 15px; /* 顶部padding增加，为署名留空间 */
            background-color: #fff0f0;
            border: 2px solid #ffb3b3;
            border-radius: 12px;
            box-shadow: 0 10px 25px rgba(0,0,0,0.2);
            color: #d60000;
            font-weight: bold;
            font-size: 16px;
            text-align: center;
            display: flex;
            align-items: center;
            justify-content: center;
            min-height: 80px;
            opacity: 0;
            transform: scale(0.5);
            animation: popIn 0.5s cubic-bezier(0.175, 0.885, 0.32, 1.275) forwards;
            pointer-events: auto; /* 允许点击 */
            cursor: pointer;
            z-index: 100;
        }

        /* 弹窗出现的动画 */
        @keyframes popIn {
            to {
                opacity: 1;
                transform: scale(1);
            }
        }

        /* 左上角署名样式 */
        .signature {
            position: absolute;
            top: 6px;
            left: 10px;
            font-size: 11px;
            color: #ff6b6b;
            font-weight: normal;
        }

        /* 关闭按钮的小叉叉 */
        .close-btn {
            position: absolute;
            top: 5px;
            right: 8px;
            font-size: 12px;
            color: #999;
            cursor: pointer;
        }
        
        .close-btn:hover {
            color: #d60000;
        }

        /* 结束后的重置按钮 */
        #reset-btn {
            display: none;
            position: fixed;
            bottom: 30px;
            left: 50%;
            transform: translateX(-50%);
            z-index: 10000;
            background-color: rgba(255, 255, 255, 0.9);
            color: #d60000;
            border: 2px solid #d60000;
            padding: 10px 30px;
            font-size: 16px;
            border-radius: 30px;
            cursor: pointer;
            box-shadow: 0 4px 10px rgba(0,0,0,0.1);
        }

        #reset-btn:hover {
            background-color: #d60000;
            color: white;
        }

    </style>
</head>
<body>

    <button id="reset-btn" onclick="location.reload()">再来亿遍</button>

    <script>
        // 52句祝福语数据
        const wishes = [
            "🎉 1. 新年快乐，万事如意！",
            "💰 2. 恭喜发财，红包拿来！",
            "🍎 3. 身体健康，百毒不侵！",
            "❤️ 4. 心想事成，美梦成真！",
            "😄 5. 笑口常开，好运连连！",
            "🚀 6. 工作顺利，步步高升！",
            "📚 7. 学业进步，逢考必过！",
            "✨ 8. 星光璀璨，未来可期！",
            "💑 9. 阖家幸福，甜甜蜜蜜！",
            "🐯 10. 生龙活虎，精神百倍！",
            "🧧 11. 财源广进，日进斗金！",
            "🍀 12. 吉星高照，福气满满！",
            "🍊 13. 大吉大利，顺顺当当！",
            "🐟 14. 年年有余，富富贵贵！",
            "🏠 15. 五福临门，喜气洋洋！",
            "🌈 16. 彩虹心情，天天开心！",
            "🌸 17. 花开富贵，锦上添花！",
            "🍭 18. 生活甜蜜，乐乐呵呵！",
            "💪 19. 身体棒棒，吃嘛嘛香！",
            "🚗 20. 出入平安，一路顺风！",
            "🏆 21. 金榜题名，独占鳌头！",
            "💼 22. 事业有成，大展宏图！",
            "👫 23. 友谊长存，常来常往！",
            "💍 24. 爱情美满，白头偕老！",
            "🎲 25. 运气爆棚，锦鲤附体！",
            "🎁 26. 惊喜不断，好事发生！",
            "🌞 27. 阳光普照，心情舒畅！",
            "🌙 28. 今夜好梦，睡个好觉！",
            "🌟 29. 闪闪发光，做最靓的仔！",
            "🔔 30. 平安喜乐，无忧无虑！",
            "🕯️ 31. 前程似锦，光芒万丈！",
            "🦅 32. 鹏程万里，扶摇直上！",
            "🐉 33. 龙马精神，活力四射！",
            "🌺 34. 青春永驻，永远十八！",
            "🌊 35. 一帆风顺，乘风破浪！",
            "💎 36. 财运亨通，腰缠万贯！",
            "🗝️ 37. 开启好运，把握机会！",
            "🎈 38. 烦恼全消，快乐加倍！",
            "🎨 39. 生活多彩，多姿多味！",
            "🏰 40. 建立基业，稳稳当当！",
            "🚢 41. 扬帆起航，勇往直前！",
            "🎠 42. 童心未泯，快乐简单！",
            "🎼 43. 歌声嘹亮，唱响未来！",
            "🕊️ 44. 和和气气，团团圆圆！",
            "🍇 45. 硕果累累，收获满满！",
            "🥂 46. 举杯共庆，美好时刻！",
            "🧩 47. 拼出未来，完美无缺！",
            "🎸 48. 激情飞扬，热血沸腾！",
            "🏖️ 49. 悠闲自在，享受生活！",
            "🎪 50. 精彩纷呈，好戏连台！",
            "🕰️ 51. 珍惜时光，不负韶华！",
            "🎆 52. 完美跨年，迎接新生！"
        ];

        function startWishes() {
            let index = 0;
            const totalWishes = wishes.length;

            // 定时器循环播放
            const interval = setInterval(() => {
                if (index >= totalWishes) {
                    clearInterval(interval);
                    // 显示重置按钮
                    setTimeout(() => {
                        document.getElementById('reset-btn').style.display = 'block';
                    }, 1000);
                    return;
                }

                createWishCard(wishes[index]);
                index++;
            }, 150); // 每150毫秒弹出一个
        }

        function createWishCard(text) {
            const card = document.createElement('div');
            card.className = 'wish-card';
            // 添加了signature span
            card.innerHTML = `<span class="signature">来自蔡王涛的祝福</span><span class="close-btn" onclick="this.parentElement.remove()">✕</span>${text}`;

            // 获取视口宽高
            const vw = window.innerWidth;
            const vh = window.innerHeight;

            // 卡片大概宽高 (配合CSS)
            const cardW = 280; 
            const cardH = 100;

            // 随机位置计算
            // 减去卡片宽高，防止出现在屏幕外
            const maxLeft = vw - cardW - 20; 
            const maxTop = vh - cardH - 20;

            // 确保不出现负数
            const randomX = Math.max(0, Math.random() * maxLeft);
            const randomY = Math.max(0, Math.random() * maxTop);

            // 随机旋转
            const rotation = (Math.random() * 20) - 10; // -10deg 到 10deg

            card.style.left = randomX + 'px';
            card.style.top = randomY + 'px';
            card.style.transform = `scale(0.5) rotate(${rotation}deg)`; 
            
            document.body.appendChild(card);

            // 增加层级
            card.style.zIndex = index + 100;
        }
        
        let index = 0;

        // 页面加载完成后立即自动开始
        window.onload = startWishes;

    </script>
</body>
</html>
