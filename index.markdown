---
layout: default2
title: "主页"
permalink: /
---

<style type="text/css">
    /* 核心页面布局 */
    .academic-page {
        font-family: 'Lato', -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, Helvetica, Arial, sans-serif;
        color: #333;
        line-height: 1.6;
        display: flex;
        flex-wrap: wrap;
        max-width: 1050px;
        margin: 0 auto;
        padding: 40px 10px;
        /* 【关键修改1】确保 flex 子元素在顶部对齐，这是 sticky 生效的前提 */
        align-items: flex-start; 
    }
    
    /* =========================================
       左侧边栏：悬浮固定设计 (Sticky Sidebar)
       ========================================= */
    .academic-sidebar {
        width: 260px;
        padding-right: 40px;
        /* 【关键修改2】让左侧悬浮固定 */
        position: -webkit-sticky; /* 兼容 Safari */
        position: sticky;
        top: 40px; /* 距离屏幕顶部的距离 */
        /* 确保侧边栏不会无限制拉伸 */
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
    .contact-info a:hover { color: #1772d0; }

    /* =========================================
       右侧主内容区：自由滚动
       ========================================= */
    .academic-main {
        flex: 1;
        min-width: 0;
    }
    .academic-main p { font-size: 15px; margin-bottom: 15px; text-align: justify; }
    .academic-main a { color: #1772d0; text-decoration: none; }
    .academic-main a:hover { text-decoration: underline; }
    
    .section-title {
        font-size: 24px;
        font-weight: bold;
        margin-top: 0; /* 第一栏顶部对齐 */
        margin-bottom: 20px;
        border-bottom: 1px solid #eaeaea;
        padding-bottom: 8px;
        color: #222;
    }
    .section-title:not(:first-child) {
        margin-top: 40px;
    }

    ul.custom-list { list-style-type: none; padding-left: 0; margin-top: 0; }
    ul.custom-list li { margin-bottom: 12px; position: relative; padding-left: 18px; font-size: 14.5px; }
    ul.custom-list li::before { content: "•"; position: absolute; left: 0; color: #666; font-size: 18px; line-height: 1.4; }
    .date-text { font-style: italic; color: #555; margin-right: 5px; }

    /* 论文列表样式 */
    .pub-category { font-size: 18px; font-weight: bold; margin-top: 25px; margin-bottom: 15px; color: #333; }
    ul.pub-list { list-style: none; padding: 0; margin: 0; }
    ul.pub-list li { margin-bottom: 25px; font-size: 14.5px; }
    .pub-title-row { margin-bottom: 4px; }
    .pub-title-row a { font-weight: bold; color: #1772d0; font-size: 16px; }
    .pub-authors { color: #444; margin-bottom: 5px; }
    .pub-authors strong { color: #111; font-weight: 700; }
    
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
    .pub-btn:hover { background: #f5f5f5; color: #1772d0; border-color: #1772d0; }

    /* 手机端自适应响应式：屏幕变小时取消悬浮，变成上下排版 */
    @media (max-width: 768px) {
        .academic-page { flex-direction: column; align-items: center; }
        .academic-sidebar { 
            width: 100%; 
            padding-right: 0; 
            text-align: center; 
            margin-bottom: 30px; 
            /* 手机端取消 sticky 悬浮 */
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
            <li><i class="fas fa-envelope"></i> <a href="mailto:chenxw83@mail2.sysu.edu.cn">Email</a></li>
            <li><i class="fas fa-graduation-cap"></i> <a href="https://scholar.google.com/citations?user=313kmTAAAAAJ&hl=zh-CN">Google Scholar</a></li>
            <li><i class="fab fa-github"></i> <a href="https://github.com/chen-xw">Github</a></li>
        </ul>
    </div>

    <div class="academic-main">
        
        <div class="section-title">About Me</div>
        <p>
            I am currently a Ph.D candidate at <a href="https://www.sysu.edu.cn/">Sun Yat-sen University (SYSU)</a>. My research interests focus on <strong>Multimodal Reasoning</strong>, including Understanding and Self-Improvement.
        </p>
        <p>
            I will be entering the job market in 2027. Please feel free to reach out if you have opportunities!
        </p>

        <div class="section-title">🔥 News</div>
        <ul class="custom-list">
            <li><span class="date-text">2025.10:</span> 🔥 Release Are Video Models Ready as Zero-Shot Reasoners?</li>
            <li><span class="date-text">2025.09:</span> 🎉 Three papers are accepted by NeurIPS 2025.</li>
            <li><span class="date-text">2024.09:</span> I have passed Ph.D. Qualifying Examination.</li>
        </ul>

        <div class="section-title">📝 Publications</div>

        <ul class="pub-list">
            <li>
                <div class="pub-title-row">
                    <a href="#">Are Video Models Ready as Zero-Shot Reasoners? An Empirical Study with the MME-CoF Benchmark</a>
                </div>
                <div class="pub-authors">
                    Ziyu Guo*, Xinyan Chen*, Renrui Zhang*, Ruichuan An*, Yu Qi*, <strong>Xiuwei Chen</strong>, Xiangtai Li, Manyuan Zhang, Hongsheng Li, Pheng-Ann Heng
                </div>
                <div style="font-style: italic; color: #666; font-size: 14px;">CVPR 2026 Findings</div>
                
                <div class="pub-links">
                    <a href="#" class="pub-btn">PDF</a>
                    <a href="#" class="pub-btn">Code</a>
                    <a href="#" class="pub-btn">Project Page</a>
                    <a href="#" class="pub-btn">Benchmark</a>
                </div>
            </li>
            
            <li>
                <div class="pub-title-row">
                    <a href="#">MME-CoF-Pro: Evaluating Reasoning Coherence in Video Generative Models with Text and Visual Hints</a>
                </div>
                <div class="pub-authors">
                    Yu Qi*, Xinyi Xu*, Ziyu Guo*, Siyuan Ma*, Renrui Zhang, <strong>Xiuwei Chen</strong>, Ruichuan An, Pheng-Ann Heng
                </div>
                <div style="font-style: italic; color: #666; font-size: 14px;">arXiv 2026</div>
                <div class="pub-links">
                    <a href="#" class="pub-btn">PDF</a>
                    <a href="#" class="pub-btn">Code</a>
                </div>
            </li>
        </ul>

        <p align="center" style="font-size: 13px; color: #999; margin-top: 60px; border-top: 1px solid #eaeaea; padding-top: 15px;">
            &copy; 2026 Xiuwei Chen.
        </p>

    </div>
</div>
