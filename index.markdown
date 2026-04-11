---
layout: default2
title: "主页"
permalink: /
---

<style type="text/css">
    /* 核心页面布局 */
    .academic-page {
        font-family: 'serif', -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, Helvetica, Arial, sans-serif;
        color: #333;
        line-height: 1.6;
        display: flex;
        flex-wrap: wrap;
        max-width: 1050px;
        margin: 0 auto;
        padding: 40px 10px;
        align-items: flex-start; 
    }
    
    /* 左侧边栏：悬浮固定设计 (Sticky Sidebar) */
    .academic-sidebar {
        width: 260px;
        padding-right: 40px;
        position: -webkit-sticky; /* 兼容 Safari */
        position: sticky;
        top: 40px; /* 距离屏幕顶部的距离 */
        height: max-content; 
    }
    .hp-photo-container {
        width: 200px;
        height: 200px;
        border-radius: 50%;
        overflow: hidden;
        margin: 0 auto 15px auto;
        border: 2px solid #eaeaea;
        box-shadow: 0 4px 10px rgba(0,0,0,0.1);
    }
    .hp-photo {
        width: 100%;
        height: 100%;
        object-fit: cover;
    }
    .author-name { font-size: 26px; font-weight: 700; text-align: center; color: #222; margin-bottom: 5px; }
    .author-title { font-size: 14.5px; text-align: center; color: #555; margin-bottom: 20px; line-height: 1.4; }
    
    .contact-info { list-style: none; padding: 0; margin: 0; }
    .contact-info li { margin-bottom: 12px; font-size: 14.5px; display: flex; align-items: center; justify-content: center; }
    .contact-info i { width: 20px; color: #444; text-align: center; margin-right: 8px; font-size: 16px; }
    .contact-info a { color: #333; text-decoration: none; transition: color 0.2s; }
    .contact-info a:hover { color: #1d4e89; } /* 链接悬停颜色也改为深蓝色 */

    /* 右侧主内容区：自由滚动 */
    .academic-main {
        flex: 1;
        min-width: 0;
    }
    .academic-main p { font-size: 15px; margin-bottom: 15px; text-align: justify; }
    .academic-main a { color: #1d4e89; text-decoration: none; } /* 链接颜色也改为深蓝色 */
    .academic-main a:hover { text-decoration: underline; }
    
    /* =========================================
       任务 1: 设置通用章节标题颜色为深蓝色 
       ========================================= */
    .section-title {
        font-size: 24px;
        font-weight: bold;
        margin-top: 0; /* 第一栏顶部对齐 */
        margin-bottom: 20px;
        border-bottom: 1px solid #eaeaea;
        padding-bottom: 8px;
        color: #1d4e89; /* 深蓝色 `#1d4e89` */
    }
    .section-title:not(:first-child) {
        margin-top: 40px;
    }

    ul.custom-list { list-style-type: none; padding-left: 0; margin-top: 0; }
    ul.custom-list li { margin-bottom: 12px; position: relative; padding-left: 18px; font-size: 14.5px; }
    ul.custom-list li::before { content: "•"; position: absolute; left: 0; color: #666; font-size: 18px; line-height: 1.4; }
    .date-text { font-style: italic; color: #555; margin-right: 5px; }

    /* =========================================
       任务 3: Publications 列表修改成第三个图这种形式 (仿截图标签和按钮)
       ========================================= */
    
    /* 标签 (Badges) */
    .badge {
        display: inline-block;
        padding: 3px 8px;
        font-size: 12px;
        font-weight: 600;
        border-radius: 4px;
        color: white;
        margin-right: 8px;
        vertical-align: text-bottom;
        line-height: 1;
    }
    .tag-arxiv { background-color: #f59e0b; } /* Arxiv 橙黄 */
    .tag-conf { background-color: #8b5cf6; }  /* 会议 紫色/蓝色 */
    .tag-blog { background-color: #10b981; }  /* 绿色 */

    /* 论文列表标题是深蓝色的链接 (将在 CSS 中设置链接颜色) */
    ul.pub-list { list-style: none; padding: 0; margin: 0; }
    ul.pub-list li { margin-bottom: 25px; font-size: 14.5px; }
    .pub-title-row { margin-bottom: 4px; }
    .pub-title-row a { font-weight: bold; color: #1d4e89; font-size: 16px; } /* 任务 3.2: 标题链接是深蓝色 */
    .pub-authors { color: #444; margin-bottom: 5px; } /* 普通作者颜色 */
    .pub-authors strong { color: #111; font-weight: 700; } /* 确保用户名字加粗 */
    
    /* 仿照图中的底部按钮 (PDF / Code / Dataset 等) */
    .pub-links { display: flex; gap: 8px; margin-top: 8px; }
    .pub-btn { 
        display: inline-block; 
        padding: 2px 8px; 
        font-size: 12px; 
        color: #333; 
        border: 1px solid #ccc; 
        border-radius: 4px; 
        text-decoration: none !important;
        transition: background 0.2s;
    }
    .pub-btn:hover { background: #f5f5f5; color: #1d4e89; border-color: #1d4e89; }

    /* 手机端自适应响应式 */
    @media (max-width: 768px) {
        .academic-page { flex-direction: column; align-items: center; }
        .academic-sidebar { 
            width: 100%; 
            padding-right: 0; 
            text-align: center; 
            margin-bottom: 30px; 
            position: static; 
        }
        .contact-info li { justify-content: center; }
    }
</style>

<link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/5.15.3/css/all.min.css">

<div class="academic-page">

    <div class="academic-sidebar">
        <div class="hp-photo-container">
            <img class="hp-photo" src="./imgs/photo.jpg" alt="Xiuwei Chen">
        </div>
        <div class="author-name">Xiuwei Chen</div>
        <div class="author-title">
            Ph.D. Candidate<br>
            HCP Lab, SYSU </div>
        <ul class="contact-info">
            <li><i class="fas fa-envelope"></i> <a href="mailto:chenxw83@mail2.sysu.edu.cn"></a>
            <i class="fas fa-graduation-cap"></i> <a href="#"></a>
            <i class="fab fa-github"></i> <a href="https://github.com/chen-xw"></a>
            <i class="fab fa-linkedin"></i> <a href="#"></a></li>
        </ul>
    </div>

    <div class="academic-main">
        
        <div class="section-title">About Me</div> <p>
            I am currently a Ph.D candidate at <a href="https://www.sysu.edu.cn/">Sun Yat-sen University (SYSU)</a>. My research interests focus on <strong>Multimodal Reasoning</strong>, including Understanding and Self-Improvement.
        </p>
        <p>
            I will be entering the job market in 2027. Please feel free to reach out if you have opportunities!
        </p>

        <div class="section-title">🔥 News</div> <ul class="custom-list">
            <li><span class="date-text">2025.10:</span> 🔥 Release Are Video Models Ready as Zero-Shot Reasoners?</li>
            <li><span class="date-text">2025.09:</span> 🎉 Three papers are accepted by NeurIPS 2025.</li>
            <li><span class="date-text">2024.09:</span> I have passed Ph.D. Qualifying Examination.</li>
        </ul>

        <div class="section-title">🛠️ Projects</div> <ul class="custom-list">
            <li>
                <a href="#" style="font-weight: bold;">UlmEvalkit: An open-source toolkit for evaluating unified large multi-modal models and generative models</a><br>
                <strong>Xiuwei Chen</strong>, Renrui Zhang, Yankai Shu, Yuyang Peng, Zhuofan Zong, Yuchen Duan, Zihao Wang, Jiaming Liu, Hao Chen, Ziyu Guo, Junyan Ye, Rui Liu, Pheng Ann Heng, Shanghang Zhang, Hongsheng Li.
            </li>
        </ul>

        <div class="section-title">📝 Publications</div> <div class="pub-category">o1/R1-like CoT Reasoning for Generation</div>
        <ul class="pub-list">
            <li>
                <div class="pub-title-row">
                    <span class="badge tag-arxiv">Arxiv</span> <a href="#">Are Video Models Ready as Zero-Shot Reasoners? An Empirical Study with the MME-CoF Benchmark</a> </div>
                <div class="pub-authors">
                    Ziyu Guo*, Xinyan Chen*, Renrui Zhang*, Ruichuan An*, Yu Qi*, <strong>Xiuwei Chen</strong>, Xiangtai Li, Manyuan Zhang, Hongsheng Li, Pheng-Ann Heng </div>
                <div style="font-style: italic; color: #666; font-size: 14px;">CVPR 2026 Findings</div> <div class="pub-links"> <a href="#" class="pub-btn">PDF</a>
                    <a href="#" class="pub-btn">Code</a>
                    <a href="#" class="pub-btn">Project Page</a>
                    <a href="#" class="pub-btn">Benchmark</a>
                </div>
            </li>
            
            <li>
                <div class="pub-title-row">
                    <span class="badge tag-conf">NeurIPS 2025</span> <a href="#">T2I-R1: Reinforcing Image Generation with Collaborative Semantic-level and Token-level CoT</a> </div>
                <div class="pub-authors">
                    <strong>Xiuwei Chen</strong>*, Ziyu Guo*, Renrui Zhang*, Zhuofan Zong, Hao Li, Le Zhuo, Shilin Yan, Pheng-Ann Heng, Hongsheng Li </div>
                <div style="font-style: italic; color: #666; font-size: 14px;">NeurIPS 2025</div> <div class="pub-links"> <a href="#" class="pub-btn">PDF</a>
                    <a href="#" class="pub-btn">Code</a>
                    <a href="#" class="pub-btn">Project Page</a>
                </div>
            </li>
        </ul>

        <div class="pub-category">o1/R1-like CoT Reasoning for Understanding</div>
        <ul class="pub-list">
            <li>
                <div class="pub-title-row">
                    <span class="badge tag-conf">ECCV 2024</span> <a href="#">MathVerse: Does Your Multi-modal LLM Truly See the Diagrams in Visual Math Problems?</a> </div>
                <div class="pub-authors">
                    Renrui Zhang*, <strong>Xiuwei Chen</strong>*, Yichi Zhang*, Haokun Lin, Ziyu Guo, Pengshuo Qiu, Aojun Zhou, Pan Lu, Aojun Zhou, Kai-Wei Chang, Peng Gao, Hongsheng Li </div>
                <div style="font-style: italic; color: #666; font-size: 14px;">ECCV 2024</div> <div class="pub-links"> <a href="#" class="pub-btn">PDF</a>
                    <a href="#" class="pub-btn">Code</a>
                    <a href="#" class="pub-btn">Project Page</a>
                    <a href="#" class="pub-btn">Dataset</a>
                </div>
            </li>
        </ul>

        <p align="center" style="font-size: 13px; color: #999; margin-top: 60px; border-top: 1px solid #eaeaea; padding-top: 15px;">
            &copy; 2026 Xiuwei Chen. Last update: 2024.05.
        </p>

    </div>
</div>
