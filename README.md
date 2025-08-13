# toxiaoyuan
<!DOCTYPE html>
<html lang="zh-CN">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>To XiaoYuan</title>
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <style>
        :root {
            --neon-pink: #ff00ff;
            --neon-blue: #00ffff;
            --bg-dark: #111;
        }
        
        body {
            background-color: #000;
            color: #fff;
            font-family: 'Arial', sans-serif;
            line-height: 1.6;
            padding: 20px;
            margin: 0;
            min-height: 100vh;
            overflow-x: hidden;
        }
        
        .container {
            max-width: 800px;
            margin: 0 auto;
            position: relative;
        }
        
        /* 霓虹文字效果 */
        .neon-first-line {
            color: #fff;
            text-shadow: 
                0 0 5px #fff,
                0 0 15px var(--neon-pink),
                0 0 30px var(--neon-pink);
            font-size: 1.3rem;
            font-weight: bold;
            display: block;
            margin-bottom: 8px;
        }
        
        .neon-title {
            font-size: 2.5rem;
            text-shadow: 
                0 0 5px #fff,
                0 0 15px var(--neon-pink),
                0 0 30px var(--neon-pink),
                0 0 60px var(--neon-pink);
            animation: glow 2s infinite alternate;
            margin: 20px 0;
            text-align: center;
        }
        
        @keyframes glow {
            0% { text-shadow: 0 0 5px #fff, 0 0 10px var(--neon-pink); }
            100% { text-shadow: 0 0 15px #fff, 0 0 30px var(--neon-pink), 0 0 60px var(--neon-pink); }
        }
        
        p {
            margin: 0 0 15px 0;
            color: #ddd;
        }
        
        /* 音乐播放器 */
        .music-player {
            width: 100%;
            margin: 20px 0;
            background: rgba(255,255,255,0.1);
            border-radius: 10px;
            padding: 15px;
            border: 1px solid var(--neon-pink);
            position: relative;
        }
        
        .music-info {
            display: flex;
            align-items: center;
            margin-bottom: 10px;
        }
        
        .music-cover {
            width: 60px;
            height: 60px;
            background: linear-gradient(45deg, #ff00ff, #00ffff);
            border-radius: 8px;
            margin-right: 15px;
            display: flex;
            align-items: center;
            justify-content: center;
            font-size: 24px;
        }
        
        /* 图片样式 */
        .image-gallery {
            display: grid;
            grid-template-columns: repeat(auto-fill, minmax(300px, 1fr));
            gap: 20px;
            margin: 30px 0;
        }
        
        .gallery-item {
            position: relative;
            overflow: hidden;
            border-radius: 8px;
            border: 1px solid #333;
            transition: all 0.3s ease;
        }
        
        .gallery-item:hover {
            transform: translateY(-5px);
            box-shadow: 0 10px 20px rgba(255,0,255,0.3);
        }
        
        .gallery-item img {
            width: 100%;
            height: auto;
            display: block;
            transition: transform 0.5s;
        }
        
        .gallery-item:hover img {
            transform: scale(1.05);
        }
        
        .gallery-caption {
            padding: 10px;
            background: rgba(0,0,0,0.7);
            text-align: center;
        }
        
        /* 游戏按钮样式 */
        .game-btn {
            background: var(--neon-pink);
            color: white;
            border: none;
            padding: 10px 20px;
            border-radius: 5px;
            cursor: pointer;
            font-weight: bold;
            margin: 10px 5px;
            transition: all 0.3s;
        }
        
        .game-btn:hover {
            transform: scale(1.05);
            box-shadow: 0 0 15px var(--neon-pink);
        }
        
        /* 小游戏区域 */
        #gameArea {
            display: none;
            position: fixed;
            top: 50%;
            left: 50%;
            transform: translate(-50%, -50%);
            width: 80%;
            max-width: 500px;
            background: rgba(0,0,0,0.9);
            border: 2px solid var(--neon-pink);
            border-radius: 10px;
            padding: 20px;
            z-index: 1000;
            text-align: center;
        }
        
        #gameCanvas {
            background: #111;
            border: 1px solid #333;
            margin: 10px auto;
            display: block;
        }
        
        /* 方向键控制提示 */
        .controls {
            display: flex;
            flex-direction: column;
            align-items: center;
            margin-top: 10px;
        }
        
        .arrow-row {
            display: flex;
        }
        
        .arrow-key {
            width: 30px;
            height: 30px;
            background: rgba(255,255,255,0.1);
            border: 1px solid var(--neon-pink);
            display: flex;
            align-items: center;
            justify-content: center;
            margin: 2px;
            border-radius: 3px;
        }
        
        /* 错误提示 */
        .error-message {
            color: #ff5555;
            text-align: center;
            padding: 10px;
            margin: 10px 0;
            border: 1px solid #ff5555;
            border-radius: 5px;
            display: none;
        }
        
        /* 响应式设计 */
        @media (max-width: 768px) {
            .neon-title { font-size: 1.8rem; }
            .image-gallery { grid-template-columns: 1fr; }
        }
        
        /* 交互按钮 */
        #backToTop, #secretBtn, #gameLaunchBtn {
            position: fixed;
            width: 50px;
            height: 50px;
            border-radius: 50%;
            color: white;
            border: none;
            cursor: pointer;
            font-size: 1.2rem;
            z-index: 99;
            opacity: 0.7;
            transition: all 0.3s;
        }
        
        #backToTop {
            bottom: 30px;
            right: 30px;
            background: var(--neon-pink);
            box-shadow: 0 0 10px var(--neon-pink);
            display: none;
        }
        
        #secretBtn {
            bottom: 30px;
            left: 30px;
            background: #333;
            border: 2px solid var(--neon-pink);
        }
        
        #gameLaunchBtn {
            bottom: 100px;
            left: 30px;
            background: #333;
            border: 2px solid var(--neon-blue);
        }
        
        #backToTop:hover, #secretBtn:hover, #gameLaunchBtn:hover {
            opacity: 1;
            transform: scale(1.1);
        }
        
        /* 分隔线样式 */
        hr {
            border: 0;
            height: 1px;
            background: linear-gradient(to right, transparent, var(--neon-pink), transparent);
            margin: 40px 0;
        }
        
        /* 跑马灯效果 */
        marquee {
            padding: 10px 0;
            color: var(--neon-pink);
            font-size: 1.2rem;
            text-shadow: 0 0 10px var(--neon-pink);
        }
        
        /* 星空背景效果 */
        .stars {
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            pointer-events: none;
            z-index: -1;
        }
        
        .star {
            position: absolute;
            background: white;
            border-radius: 50%;
            animation: twinkle var(--duration) infinite ease-in-out;
        }
        
        @keyframes twinkle {
            0%, 100% { opacity: 0.2; }
            50% { opacity: 1; }
        }
        
        /* 音乐可视化 */
        #visualizer {
            height: 60px;
            width: 100%;
            margin-top: 10px;
            display: flex;
            align-items: flex-end;
            justify-content: center;
        }
        
        .bar {
            width: 4px;
            margin: 0 2px;
            background: linear-gradient(to top, var(--neon-pink), var(--neon-blue));
            border-radius: 2px;
        }
        
        /* 视频容器 */
        .video-container {
            position: relative;
            padding-bottom: 56.25%;
            height: 0;
            overflow: hidden;
            margin: 20px 0;
        }
        
        .video-container iframe {
            position: absolute;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            border: none;
        }
        
        /* 播放列表 */
        .playlist {
            margin-top: 15px;
            max-height: 200px;
            overflow-y: auto;
            border-top: 1px solid rgba(255,255,255,0.1);
            padding-top: 10px;
        }
        
        .playlist-item {
            padding: 8px;
            margin: 5px 0;
            background: rgba(255,255,255,0.05);
            border-radius: 5px;
            cursor: pointer;
            transition: all 0.2s;
        }
        
        .playlist-item:hover {
            background: rgba(255,255,255,0.1);
        }
        
        .playlist-item.active {
            background: rgba(255,0,255,0.2);
            border-left: 3px solid var(--neon-pink);
        }
    </style>
</head>
<body>
    <!-- 星空背景 -->
    <div class="stars" id="stars"></div>
    
    <div class="container">
        <!-- 交互按钮 -->
        <button id="backToTop" title="返回顶部">↑</button>
        <button id="secretBtn" title="点击有惊喜">?</button>
        <button id="gameLaunchBtn" title="玩个小游戏">🎮</button>
        
        <h1 class="neon-title"><i class="fas fa-gift"></i> To Xian Yuan</h1>
        
        <section>
            <span class="neon-first-line">我想了一下如果直接发txt文档的话可能有点麻烦，所以我就把文档内容给放在这儿吧</span>
            <p>其实原本我还打算去买点东西给你的不过在暑托期间预算就花完了抱歉抱歉，我后边会补上滴😉</p>
            
            <hr>
            
            <div class="gallery-item">
                <img src="https://i.ibb.co/YBRLYKQw/mmexport1751690392842.jpg" 
                     alt="猜猜我保存的目的😉" 
                     loading="lazy">
                <div class="gallery-caption">猜猜我保存的目的😉</div>
            </div>
            
            <h2><marquee>———————— S U Y U A N ————————</marquee></h2>
        </section>
        
      <!-- 音乐播放器部分 -->
<section>
    <span class="neon-first-line">1.mp3</span>
    <div class="music-player">
        <div class="music-info">
            <div class="music-cover">
                <i class="fas fa-music"></i>
            </div>
            <div>
                <h3 id="nowPlaying" style="margin:0">选择歌曲播放</h3>
                <p style="margin:5px 0 0;color:#aaa;">点击下方列表选择歌曲</p>
            </div>
        </div>
        <audio id="mainAudio" controls style="width:100%">
            您的浏览器不支持音频播放
        </audio>
        <div id="visualizer"></div>
        <div id="musicError" class="error-message">
            音乐加载失败，请点击歌曲重试或检查网络
        </div>
        
        <div class="playlist">
            <div class="playlist-item active" 
                 data-src="https://music.163.com/song/media/outer/url?id=1694104.mp3" 
                 data-title="LJones - Soul Below">
                Soul Below - LJones
            </div>
            <div class="playlist-item" 
                 data-src="https://music.163.com/song/media/outer/url?id=1309995372.mp3" 
                 data-title="beabadoobee - Coffee">
                Coffee - beabadoobee
            </div>
            <div class="playlist-item" 
                 data-src="https://music.163.com/song/media/outer/url?id=420478436.mp3" 
                 data-title="Charlie Puth/Selena Gomez - We Don't Talk Anymore">
                We Don't Talk Anymore - Charlie Puth/Selena Gomez
            </div>
            <div class="playlist-item" 
                 data-src="https://music.163.com/song/media/outer/url?id=1311427648.mp3" 
                 data-title="She Her Her Hers - Episode 33">
                Episode 33 - She Her Her Hers
            </div>
        </div>
        
        <p style="text-align:center;font-size:0.8em;color:#aaa;">
            <i class="fas fa-info-circle"></i> 如果音乐无法播放，请尝试刷新页面或更换浏览器
        </p>
    </div>
            <p>肯定应该拷你喜欢的歌呢（不过我不知道你的歌单）🧐</p>
            <p>只能拷一些大众歌曲和我根据零散信息来挑一些歌了😲</p>
            <p>不过我还是挺纠结有些调有点低（也就是emo型吧？不过我个人认为其实也可以换一个角度来听也算是"治愈"了）我不想一些东西会勾起负面情绪（不过个人认为抛开这个不谈，有些这种类型的歌还是挺好听的😁）而且人的情绪是多样的，刻意压抑某种情绪何尝又不是另一种病态呢？🧐 所以我还是决定拷一点（其实本来曲库就不多（bushi🤓</p>
            <p>（补）其实我还是想问问歌单的，不过你完美的假期一样只有这一次所以还是没问……不过我拷的都比较少，删掉不好听的也方便一点，内存卡插手机里即可传输文件</p>
        </section>
        
        <!-- 其他内容部分 -->
        <section>
            <span class="neon-first-line">2.一些呃……话？</span>
            <p>还有这个高中不乘哦，只有18天假期😭所以时间比我预想中还要紧迫，估计后面这一年时间更少了（连着上7个月😂）</p>
            <p>当然从我上高三开始高一高二就有双休了（我们这边是这样，不知道你们那儿怎么样）😉所以我希望你高中一定要结交新朋友，有一个能融入圈子的朋友（这样相处就容易许多了😁），恕我不能在你刚进高中这一年里过多回复🙃我相信你可以的😉👍</p>
            <p>你的一个朋友圈可真是帮了大忙呀，帮我提供了很多思路😄😋</p>
        </section>
        
        <hr>
        
        <!-- 图片画廊 -->
        <section>
            <span class="neon-first-line">收集的图片</span>
            <div class="image-gallery">
                <div class="gallery-item">
                    <img src="https://i.ibb.co/1tzxFLVy/t04bcacd5bbced0e9e5.webp" 
                         alt="记者德罗斯" 
                         loading="lazy">
                    <div class="gallery-caption">记者德罗斯</div>
                </div>
                
                <div class="gallery-item">
                    <img src="https://i.ibb.co/pvLPh7tP/1272144343.jpg" 
                         alt="画家瓦格·艾尔登" 
                         loading="lazy">
                    <div class="gallery-caption">画家瓦格·艾尔登</div>
                </div>
                
                <div class="gallery-item">
                    <img src="https://i.ibb.co/zTWbx4ML/IMG-20250806-211836.jpg" 
                         alt="记者德罗斯" 
                         loading="lazy">
                    <div class="gallery-caption">这个也是记者德罗斯</div>
                </div>
                
                <div class="gallery-item">
                    <img src="https://i.ibb.co/9Hx2PgwF/1390385243.jpg" 
                         alt="同人图" 
                         loading="lazy">
                    <div class="gallery-caption">这个是我找的呃……同人图？</div>
                </div>
                
                <div class="gallery-item">
                    <img src="https://i.ibb.co/wx0c8Tg/419285932.jpg" 
                         alt="游戏角色" 
                         loading="lazy">
                    <div class="gallery-caption">嗯，这是单独的，但总感觉和游戏不是一个画风呢🧐</div>
                </div>
                
                <div class="gallery-item">
                    <img src="https://i.ibb.co/nNY5G5Rd/IMG-20250806-211933.jpg" 
                         alt="酷拉皮卡" 
                         loading="lazy">
                    <div class="gallery-caption">这个是全职猎人中的酷拉皮卡（应该是吧？）😶</div>
                </div>
            </div>
        </section>
        
        <section>
            <span class="neon-first-line">3.一些建议（可能引人不适辩证观看）</span>
            <p>英语始终是我恨呀……我也知道光给出建议其实也没什么用，每个人都知道词汇量十分重要，就是这个学科提分慢，短期内没什么成效，记忆量又大，又容易忘，语法又烦人，本身也无聊会给我一些打击🤓不过我希望你能有个不会管太紧的老师，如果教育方法不当是很容易厌恶这个学科的（bushi</p>
            <p>我这里呢是在英语课上只记单词，不听课，对我这种词汇量少的低分有些用，语法就不去掌握了，作文老师没多少时间看语法错误，语法填空的前提还是词汇量，其他就没语法什么事了，所以我的建议是可以放弃语法，拿多出来的时间全砸单词上（不过每个人的方法都不一样，结果也不同，我的就仅作参考啦😁）</p>
            <p>数学我只列举几个非常重要的：1.在高一学高三还得用上的</p>
            <p>2.考试固定NPC的</p>
            <p>（1）对指数函数</p>
            <p>1.基本不等式（二级定论如：极值，柯西）其它就做了解，还有几个常用的我记不住了🙂</p>
            <p>2.古典概型（别忘太干净就行，高三下册最后一章还要扯一扯，但只是帮助理解，如果忘了，也能理解的，只是可能上课有些老师讲不清的话就有点难受，毕竟考试错了简单的会很心痛的）</p>
            <p>（2）（仅高三试卷，其它学期都不重要了，高三试卷和高考的模板最像）</p>
            <p>1.数列（高二）</p>
            <p>2.圆锥曲线（高一）（个人感觉最难）</p>
            <p>3.统计概率（高三）</p>
            <p>4.立体几何（高二）</p>
            <p>5.导数（高三）（综合性高，但是比2好拿分）</p>
            <marquee>       E       N       D</marquee>
        </section>
        
        <hr>
        
        <section>
            <span class="neon-first-line">4.补充</span>
            <p>目标很重要呀，动力的重要来源，别像我一样，动力不源于目标，而是一时脑热，是没有上进的</p>
            <p>当然我也不会给你无效的情感支持，个人感觉那种只顾正面安慰的话是无效的，我就现实一点的说</p>
            <p>在四川，能够出头的人只能是少数，成都和绵阳已经把本就不多本科率给占完了，考生数量和学校数量比失衡，所以，最后的结果不一定是好的，所以我的建议是观察一下时局，找找学习以外的出路做最后的保障，在四川，学习不一定是最轻松的出路</p>
            <p>所谓的高等中学其实看似过线率高，但是不代表能有大学读，正常来说，公办本科的掉档线都比本科线高几十分，过本科线一些只能读民办本科😂而且就光拿我们学校来看，其实学风也不太正，不然我不会有这种感觉的，很多人都在摆烂，所以别觉得没上普高就怎么样，其实都差不多，而职校的环境可能更适合找除学习以外的出路（总体来说都有好有坏）</p>
            <p>当然目前来看读书仍是必须的，不能因为我的个人主观意识上的观念而改变，社会需要人才，即使不一定是对文化方面有需求但读书仍是最主要的选拔（以上为个人观点仅供参考）</p>
        </section>
        
        <hr>
        
        <section>
            <span class="neon-first-line">2025.8.9日的又一次补充</span>
            <p>我之前有提过ps吧，小小的去研究了一下（大概20分钟的样子）进行了一个简单的ps（第一次，所以质量不咋滴，请谅解）😉</p>
            
            <div class="gallery-item">
                <img src="https://i.ibb.co/gLPTgvRz/Image-1754695568896.png" 
                     alt="PS作品" 
                     loading="lazy">
                <div class="gallery-caption">你能找出P掉水印的痕迹吗？😉</div>
            </div>
            
            <marquee>嘻嘻</marquee>
        </section>
        
        <hr>
        
        <footer>
            <p class="neon-first-line">由于没系统学习HTML，这些格式比较粗制滥造，小游戏无法正常运行，歌曲不能加载（这个倒是网易云音乐的限制），视频只能通过链接观看，嗯，这些就是已知的问题……对头</p>
            <p>2025年8月</p>
        </footer>
    </div>

    <!-- 小游戏弹窗 -->
    <div id="gameArea">
        <h2 class="neon-first-line" style="text-align:center;">霓虹接球游戏</h2>
        <p>使用方向键移动，接住掉落的球</p>
        <canvas id="gameCanvas" width="400" height="400"></canvas>
        
        <div class="controls">
            <div class="arrow-row">
                <div class="arrow-key">↑</div>
            </div>
            <div class="arrow-row">
                <div class="arrow-key">←</div>
                <div class="arrow-key">↓</div>
                <div class="arrow-key">→</div>
            </div>
        </div>
        
        <div>
            <button class="game-btn" id="startGame">开始游戏</button>
            <button class="game-btn" id="closeGame">关闭</button>
        </div>
        <p id="gameScore" style="font-size:1.2rem;">得分: 0</p>
    </div>

    <script>
        // 返回顶部按钮
        const backToTopBtn = document.getElementById('backToTop');
        window.addEventListener('scroll', () => {
            if (window.pageYOffset > 300) {
                backToTopBtn.style.display = 'block';
            } else {
                backToTopBtn.style.display = 'none';
            }
        });
        
        backToTopBtn.addEventListener('click', () => {
            window.scrollTo({ top: 0, behavior: 'smooth' });
        });
        
        // 图片点击放大效果
        document.querySelectorAll('.gallery-item img').forEach(img => {
            img.addEventListener('click', function() {
                const overlay = document.createElement('div');
                overlay.style.position = 'fixed';
                overlay.style.top = '0';
                overlay.style.left = '0';
                overlay.style.width = '100vw';
                overlay.style.height = '100vh';
                overlay.style.backgroundColor = 'rgba(0,0,0,0.9)';
                overlay.style.display = 'flex';
                overlay.style.justifyContent = 'center';
                overlay.style.alignItems = 'center';
                overlay.style.zIndex = '100';
                overlay.style.cursor = 'zoom-out';
                
                const enlargedImg = new Image();
                enlargedImg.src = this.src;
                enlargedImg.style.maxHeight = '90vh';
                enlargedImg.style.maxWidth = '90vw';
                enlargedImg.style.objectFit = 'contain';
                
                overlay.appendChild(enlargedImg);
                document.body.appendChild(overlay);
                
                overlay.addEventListener('click', () => {
                    document.body.removeChild(overlay);
                });
            });
        });
        
        // 秘密按钮功能 - 包含B站视频
        document.getElementById('secretBtn').addEventListener('click', function() {
            const secretMsg = document.createElement('div');
            secretMsg.innerHTML = `
                <span class="neon-first-line" style="font-size:2rem;">🎁 惊喜彩蛋 🎁</span>
                <p style="margin:15px 0;font-size:1.2rem;">我在学校的精神状态Belike:</p>
                <div class="video-container">
                    <iframe src="//player.bilibili.com/player.html?bvid=BV1D3u6zzE63&high_quality=1&autoplay=0" 
                            scrolling="no" 
                            frameborder="no" 
                            framespacing="0" 
                            allowfullscreen="true">
                    </iframe>
                </div>
                <p style="margin-top:10px;font-size:0.9rem;color:#aaa;">视频来源：bilibili</p>
                <p style="color:#888;font-size:0.8rem;">如果视频无法加载，请<a href="https://www.bilibili.com/video/BV1D3u6zzE63" target="_blank" style="color:var(--neon-pink);">点击这里</a>前往B站观看</p>
            `;
            
            secretMsg.style.position = 'fixed';
            secretMsg.style.top = '50%';
            secretMsg.style.left = '50%';
            secretMsg.style.transform = 'translate(-50%, -50%)';
            secretMsg.style.backgroundColor = 'rgba(0,0,0,0.95)';
            secretMsg.style.padding = '20px';
            secretMsg.style.borderRadius = '10px';
            secretMsg.style.border = '2px solid var(--neon-pink)';
            secretMsg.style.zIndex = '101';
            secretMsg.style.textAlign = 'center';
            secretMsg.style.maxWidth = '90%';
            secretMsg.style.width = '600px';
            secretMsg.style.maxHeight = '90vh';
            secretMsg.style.overflowY = 'auto';

            const closeBtn = document.createElement('button');
            closeBtn.textContent = '关闭';
            closeBtn.style.marginTop = '15px';
            closeBtn.style.padding = '8px 20px';
            closeBtn.style.background = 'var(--neon-pink)';
            closeBtn.style.border = 'none';
            closeBtn.style.borderRadius = '5px';
            closeBtn.style.cursor = 'pointer';
            closeBtn.style.fontWeight = 'bold';

            secretMsg.appendChild(closeBtn);
            document.body.appendChild(secretMsg);

            closeBtn.addEventListener('click', () => {
                document.body.removeChild(secretMsg);
            });
            
            // 点击弹窗外部也关闭
            secretMsg.addEventListener('click', (e) => {
                if(e.target === secretMsg) {
                    document.body.removeChild(secretMsg);
                }
            });
        });
        
        // 创建星空背景
        function createStars() {
            const starsContainer = document.getElementById('stars');
            const starCount = 100;
            
            for (let i = 0; i < starCount; i++) {
                const star = document.createElement('div');
                star.classList.add('star');
                
                // 随机大小 (1-3px)
                const size = Math.random() * 2 + 1;
                star.style.width = `${size}px`;
                star.style.height = `${size}px`;
                
                // 随机位置
                star.style.left = `${Math.random() * 100}%`;
                star.style.top = `${Math.random() * 100}%`;
                
                // 随机闪烁时间 (2-5秒)
                star.style.setProperty('--duration', `${Math.random() * 3 + 2}s`);
                
                starsContainer.appendChild(star);
            }
        }
        
        // 音乐播放器功能
        function initMusicPlayer() {
            const audio = document.getElementById('mainAudio');
            const nowPlaying = document.getElementById('nowPlaying');
            const playlistItems = document.querySelectorAll('.playlist-item');
            const musicError = document.getElementById('musicError');
            
            // 初始化播放第一首歌
            const firstSong = playlistItems[0];
            audio.src = firstSong.dataset.src;
            nowPlaying.textContent = firstSong.dataset.title;
            
            // 错误处理
            audio.addEventListener('error', function() {
                musicError.style.display = 'block';
            });
            
            // 播放列表点击事件
            playlistItems.forEach(item => {
                item.addEventListener('click', function() {
                    // 更新活跃状态
                    playlistItems.forEach(i => i.classList.remove('active'));
                    this.classList.add('active');
                    
                    // 切换歌曲
                    audio.src = this.dataset.src;
                    nowPlaying.textContent = this.dataset.title;
                    musicError.style.display = 'none';
                    
                    audio.play().catch(e => {
                        console.log('自动播放被阻止:', e);
                        musicError.style.display = 'block';
                    });
                });
            });
            
            // 音乐可视化
            function initVisualizer() {
                const visualizer = document.getElementById('visualizer');
                
                // 清空现有可视化条
                visualizer.innerHTML = '';
                
                // 创建32个音频条
                for (let i = 0; i < 32; i++) {
                    const bar = document.createElement('div');
                    bar.className = 'bar';
                    visualizer.appendChild(bar);
                }
                
                // 设置音频分析
                try {
                    const audioContext = new (window.AudioContext || window.webkitAudioContext)();
                    const analyser = audioContext.createAnalyser();
                    const source = audioContext.createMediaElementSource(audio);
                    
                    source.connect(analyser);
                    analyser.connect(audioContext.destination);
                    analyser.fftSize = 64;
                    
                    const bufferLength = analyser.frequencyBinCount;
                    const dataArray = new Uint8Array(bufferLength);
                    
                    function updateVisualizer() {
                        requestAnimationFrame(updateVisualizer);
                        analyser.getByteFrequencyData(dataArray);
                        
                        const bars = document.getElementsByClassName('bar');
                        for (let i = 0; i < bars.length; i++) {
                            const value = dataArray[i] / 255;
                            const height = value * 60;
                            bars[i].style.height = `${height}px`;
                            bars[i].style.opacity = `${0.1 + value * 0.9}`;
                        }
                    }
                    
                    audio.addEventListener('play', () => {
                        audioContext.resume().then(() => {
                            updateVisualizer();
                        });
                    });
                } catch (e) {
                    console.log('音频可视化不支持:', e);
                }
            }
            
            initVisualizer();
        }
        
        // 小游戏功能 - 接球游戏
        function initGame() {
            const gameArea = document.getElementById('gameArea');
            const gameCanvas = document.getElementById('gameCanvas');
            const ctx = gameCanvas.getContext('2d');
            const startBtn = document.getElementById('startGame');
            const closeBtn = document.getElementById('closeGame');
            const scoreDisplay = document.getElementById('gameScore');
            
            // 游戏变量
            let gameRunning = false;
            let score = 0;
            let basket = {
                x: gameCanvas.width / 2 - 50,
                y: gameCanvas.height - 30,
                width: 100,
                height: 20,
                speed: 8
            };
            
            let balls = [];
            let lastDropTime = 0;
            
            // 绘制篮子
            function drawBasket() {
                ctx.fillStyle = '#FF9800';
                ctx.fillRect(basket.x, basket.y, basket.width, basket.height);
                ctx.fillStyle = '#795548';
                ctx.fillRect(basket.x + 40, basket.y - 10, 20, 10);
            }
            
            // 创建新球
            function createBall() {
                const now = Date.now();
                if (now - lastDropTime > 1000) { // 每秒掉落一个球
                    balls.push({
                        x: Math.random() * (gameCanvas.width - 30),
                        y: 0,
                        radius: 10 + Math.random() * 10,
                        color: `hsl(${Math.random() * 360}, 100%, 50%)`,
                        speed: 2 + Math.random() * 3
                    });
                    lastDropTime = now;
                }
            }
            
            // 绘制球
            function drawBalls() {
                balls.forEach(ball => {
                    ctx.beginPath();
                    ctx.arc(ball.x, ball.y, ball.radius, 0, Math.PI * 2);
                    ctx.fillStyle = ball.color;
                    ctx.fill();
                });
            }
            
            // 更新球位置
            function updateBalls() {
                for (let i = balls.length - 1; i >= 0; i--) {
                    balls[i].y += balls[i].speed;
                    
                    // 检测是否接到球
                    if (balls[i].y + balls[i].radius > basket.y && 
                        balls[i].x > basket.x && 
                        balls[i].x < basket.x + basket.width) {
                        score++;
                        scoreDisplay.textContent = `得分: ${score}`;
                        balls.splice(i, 1);
                        continue;
                    }
                    
                    // 移除超出屏幕的球
                    if (balls[i].y > gameCanvas.height) {
                        balls.splice(i, 1);
                    }
                }
            }
            
            // 键盘控制
            const keys = {};
            window.addEventListener('keydown', (e) => {
                keys[e.key] = true;
            });
            
            window.addEventListener('keyup', (e) => {
                keys[e.key] = false;
            });
            
            // 更新篮子位置
            function updateBasket() {
                if ((keys['ArrowLeft'] || keys['a']) && basket.x > 0) {
                    basket.x -= basket.speed;
                }
                if ((keys['ArrowRight'] || keys['d']) && basket.x < gameCanvas.width - basket.width) {
                    basket.x += basket.speed;
                }
            }
            
            // 游戏主循环
            function gameLoop() {
                if (!gameRunning) return;
                
                // 清空画布
                ctx.clearRect(0, 0, gameCanvas.width, gameCanvas.height);
                
                // 创建新球
                createBall();
                
                // 更新和绘制
                updateBasket();
                updateBalls();
                drawBasket();
                drawBalls();
                
                requestAnimationFrame(gameLoop);
            }
            
            // 开始游戏
            startBtn.addEventListener('click', () => {
                if (!gameRunning) {
                    gameRunning = true;
                    score = 0;
                    balls = [];
                    scoreDisplay.textContent = `得分: ${score}`;
                    gameLoop();
                }
            });
            
            // 关闭游戏
            closeBtn.addEventListener('click', () => {
                gameRunning = false;
                gameArea.style.display = 'none';
            });
            
            // 游戏启动按钮
            document.getElementById('gameLaunchBtn').addEventListener('click', () => {
                gameArea.style.display = 'block';
            });
        }
        
        // 页面加载后执行
        window.addEventListener('load', () => {
            createStars();
            initMusicPlayer();
            initGame();
        });
    </script>
</body>
</html>
