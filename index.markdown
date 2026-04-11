---
layout: default2
title: "主页"
permalink: /
---

<style type="text/css">
    /* 核心页面布局 */
    .academic-page {
        /*font-family: 'serif', -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, Helvetica, Arial, sans-serif;*/
        font-family: 'Georgia', 'Times New Roman', 'SimSun', 'Noto Serif SC', serif;
        color: #333;
        line-height: 1.6;
        display: flex;
        flex-wrap: wrap;
        max-width: 1800px;
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
    /* 论文列表项布局 */
    .pub-item {
        display: flex;
        gap: 25px;
        margin-bottom: 35px;
        align-items: flex-start;
    }
        /* News 部分专用样式 - 更紧凑的间距 */
    .news-list li {
        margin-bottom: 6px; /* 从 12px 减小到 6px */
        line-height: 1.4;   /* 控制行高 */
    }
    
    /* 论文图片区域 */
        /* 1. 修改图片容器，增加 relative 定位 */
    .pub-image {
        flex-shrink: 0;
        width: 200px;
        height: 120px; /* 新增：固定高度，防止图片太矮 */
        border-radius: 8px;
        overflow: hidden;
        box-shadow: 0 2px 8px rgba(0,0,0,0.1);
        background: #f5f5f5;
        position: relative; /* 新增：为了让里面的标签能定位 */
    }
    
    /* 2. 修改图片本身，让它充满容器 */
    .pub-image img {
        width: 100%;
        height: 100%; /* 新增：高度占满 */
        object-fit: cover; /* 新增：关键属性！裁剪图片以充满容器，不留白边 */
        display: block;
        transition: transform 0.3s ease;
    }
    
    .pub-image:hover img {
        transform: scale(1.02);
    }

    /* 3. 新增：图片左上角标签的样式 (类似图3中的 arXiv 2026) */
    .pub-img-badge {
        position: absolute;
        top: 10px;
        left: 10px;
        background-color: #1d4e89; /* 深蓝色背景 */
        color: white;
        padding: 3px 8px;
        font-size: 12px;
        font-weight: bold;
        border-radius: 4px;
        z-index: 10; /* 保证在图片上层 */
        box-shadow: 0 2px 4px rgba(0,0,0,0.2);
    }
    .contact-info li {
        list-style: none;
        display: flex;
        gap: 16px; /* 图标间距 */
        align-items: center;
    }
    
    .contact-info a {
        color: #555; /* 图标默认颜色 */
        font-size: 1.2rem; /* 图标大小 */
        transition: color 0.3s ease, transform 0.2s ease;
        display: inline-flex;
        padding: 6px; /* 扩大点击区域 */
        border-radius: 4px;
    }
    
    .contact-info a:hover {
        color: #007bff; /* 悬停颜色，可按品牌色定制 */
        transform: translateY(-2px); /* 轻微上浮效果 */
    }
    
    /* 可选：不同平台悬停色 */
    .contact-info a[href*="github.com"]:hover { color: #333; }
    .contact-info a[href*="linkedin.com"]:hover { color: #0077b5; }
    .contact-info a[href*="scholar.google.com"]:hover { color: #4285f4; }
    .contact-info a[href^="mailto:"]:hover { color: #ea4335; }
    
    /* 论文内容区域 */
    .pub-content {
        flex: 1;
        min-width: 0;
    }

/* 响应式设计 */
@media (max-width: 768px) {
    .pub-item {
        flex-direction: column;
    }
    
    .pub-image {
        width: 100%;
        max-width: 400px;
        margin: 0 auto;
    }
}
    
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
            <img class="hp-photo" src="./image/photo.jpg" alt="Xiuwei Chen">
        </div>
        <div class="author-name">Xiuwei Chen</div>
        <div class="author-title">
            Ph.D. Student<br>
            HCP Lab, SYSU </div>
        <ul class="contact-info">
            <li>
                <a href="mailto:chenxw83@mail2.sysu.edu.cn" target="_blank" title="Email" aria-label="Email">
                    <i class="fas fa-envelope"></i>
                </a>
                <a href="https://scholar.google.com/citations?user=313kmTAAAAAJ&hl=zh-CN" target="_blank" title="Google Scholar" aria-label="Google Scholar">
                    <i class="fas fa-graduation-cap"></i>
                </a>
                <a href="https://github.com/chen-xw" target="_blank" title="GitHub" aria-label="GitHub">
                    <i class="fab fa-github"></i>
                </a>
                <a href="https://www.linkedin.com/in/your-profile" target="_blank" title="LinkedIn" aria-label="LinkedIn">
                    <i class="fab fa-linkedin"></i>
                </a>
            </li>
        </ul>
    </div>

    <div class="academic-main">
        
        <div class="section-title">About Me</div> <p>
             I am currently a Ph.D candidate in HCP Group at <a href="https://sai.sysu.edu.cn/">Sun Yat-sen University (SYSU)</a>, supervised by <a href="https://scholar.google.com/citations?user=voxznZAAAAAJ&hl=zh-CN">Prof. Xiaodan Liang</a>. I received my Master's degree at the <a href="https://www.sysu.edu.cn/">Sun Yat-sen University (SYSU)</a>, supervised by <a href="https://xb-chang.github.io/">Prof. Xiaobin Chang</a>. Prior to SYSU, I obtained a B.Eng from <a href="https://www.tyut.edu.cn/">TYUT</a> and majored in Computer Science and Technology (CS) in 2021.
        </p>
        <p>
            My research interests focus on <strong>Multimodal Reasoning</strong>, including the <strong>Understanding</strong> and <strong>Self-Improvement</strong>. Priored that, my focus on Person Re-identification and Incremental Learning.
        </p>

        <div class="section-title">🔥 News</div> <ul class="custom-list news-list">
            <li><span class="date-text"><strong>[2026.02]</strong></span> 🎉 One paper (<a href="https://arxiv.org/abs/2503.06764">SemHiTok</a>) is accepted by ICLR 2026.</li>
            <li><span class="date-text"><strong>[2025.12]</strong></span> 🔥 We release <a href="https://arxiv.org/abs/2502.15130">EVA</a>, a framework that internalizes explicit tool calling into the model's intrinsic capabilities.</li>
            <li><span class="date-text"><strong>[2025.07]</strong></span> 🔥 We release <a href="https://c2-evo.github.io">C2-Evo</a>, a method for co-evolving models and data, an agent for drawing auxiliary line.</li>
            <li><span class="date-text"><strong>[2025.02]</strong></span> 🔥 We release <a href="https://arxiv.org/abs/2502.15130">TransMamba</a>, a simple method to quickly adapt Transformer models to the Mamba framework.</li>
            <li><span class="date-text"><strong>[2023.10]</strong></span> 🎉 One paper is accepted by PRCV 2023.</li>
            <li><span class="date-text"><strong>[2023.07]</strong></span> 🎉 One paper (<a href="https://arxiv.org/abs/2308.13305">DRC</a>) is accepted by ICCV 2023.</li>
            <li><span class="date-text"><strong>[2021.01]</strong></span> Welcome to my new homepage!</li>
        </ul>

        <div class="section-title">📝 Publications and Preprints</div>
        <ul class="pub-list">

            <li>
                <div class="pub-item">
                    <div class="pub-image">
                        <!-- 在这里添加标签，文字可以改成 arXiv 2025 等 -->
                        <span class="pub-img-badge">ICLR 2026</span> 
                        <img src="./image/SemHiTok.png" alt="MME-CoF Benchmark">
                    </div>
                    <div class="pub-content">
                        <div class="pub-title-row">
                            <span class="badge tag-conf">ICLR 2026</span> <a href="https://arxiv.org/abs/2503.06764">SemHiTok: A Unified Image Tokenizer via Semantic-Guided Hierarchical Codebook for Multimodal Understanding and Generation</a> 
                        </div>
                        <div class="pub-authors">
                            Zisheng Chen, Chunwei Wang, Runhui Huang, Hongbin Xu, Xiuwei Chen, Jun Zhou, Jianhua Han, Hang Xu, Xiaodan Liang
                        </div>
                        <div style="font-style: italic; color: #666; font-size: 14px;">ICLR 2026</div> 
                        <div class="pub-links"> 
                            <a href="https://arxiv.org/abs/2503.06764" class="pub-btn">PDF</a>
                        </div>  
                    </div>    
                </div>   
            </li>

            <!-- 论文 1 示例 -->
            <li>
                <div class="pub-item">
                    <div class="pub-image">
                        <!-- 在这里添加标签，文字可以改成 arXiv 2025 等 -->
                        <span class="pub-img-badge">arXiv 2025</span> 
                        <img src="./image/eva.png" alt="MME-CoF Benchmark">
                    </div>
                    <div class="pub-content">
                        <div class="pub-title-row">
                            <span class="badge tag-arxiv">Arxiv</span> <a href="https://arxiv.org/abs/2502.15130">Latent Visual States for Efficient Multimodal Reasoning</a> 
                        </div>
                        <div class="pub-authors">
                            Xiuwei Chen, Wentao Hu, Xiao Dong, Sihao Lin, Zisheng Chen, Meng Cao, Yina Zhuang, Jianhua Han, Hang Xu, Xiaodan Liang
                        </div>
                        <div style="font-style: italic; color: #666; font-size: 14px;">arXiv 2025</div> 
                        <div class="pub-links"> 
                            <a href="https://arxiv.org/abs/2502.15130" class="pub-btn">PDF</a>
                            <a href="https://github.com/chen-xw/TransMamba-main" class="pub-btn">Code</a>
                            <a href="https://github.com/chen-xw/TransMamba-main" class="pub-btn">Project Page</a>
                        </div>  
                    </div>    
                </div>   
            </li>
            
            <!-- 论文 2 示例 (记得改标签文字) -->
            <li>
                <div class="pub-item">
                    <div class="pub-image">
                        <span class="pub-img-badge">arXiv 2025</span>
                        <img src="./image/c2evo.png" alt="MME-CoF Benchmark">
                    </div>
                    <div class="pub-content">
                        <!-- ... 内容保持不变 ... -->
                         <div class="pub-title-row">
                            <span class="badge tag-arxiv">Arxiv</span> <a href="https://c2-evo.github.io/">C2-Evo: Co-Evolving Multimodal Data and Model for Self-Improving Reasoning</a> 
                        </div>
                        <div class="pub-authors">
                            Xiuwei Chen, Wentao Hu, Hanhui Li, Jun Zhou, Zisheng Chen, Meng Cao, Yihan Zeng, Kui Zhang, Yu-Jie Yuan, Jianhua Han, Hang Xu, Xiaodan Liang
                        </div>
                        <div style="font-style: italic; color: #666; font-size: 14px;">arXiv 2025</div> 
                        <div class="pub-links"> 
                            <a href="https://arxiv.org/abs/2507.16518" class="pub-btn">PDF</a>
                            <a href="https://github.com/chen-xw/C2-Evo" class="pub-btn">Code</a>
                            <a href="https://c2-evo.github.io/" class="pub-btn">Project Page</a>
                        </div>  
                    </div>    
                </div>   
            </li>
            
            <!-- 论文 3 示例 -->
            <li>
                <div class="pub-item">
                    <div class="pub-image">
                        <span class="pub-img-badge">arXiv 2025</span>
                        <img src="./image/transmamba.png" alt="MME-CoF Benchmark">
                    </div>
                    <div class="pub-content">
                         <!-- ... 内容保持不变 ... -->
                         <div class="pub-title-row">
                            <span class="badge tag-arxiv">Arxiv</span> <a href="https://arxiv.org/abs/2502.15130">TransMamba: Fast Universal Architecture Adaption from Transformers to Mamba</a> 
                        </div>
                        <div class="pub-authors">
                            Xiuwei Chen, Wentao Hu, Xiao Dong, Sihao Lin, Zisheng Chen, Meng Cao, Yina Zhuang, Jianhua Han, Hang Xu, Xiaodan Liang
                        </div>
                        <div style="font-style: italic; color: #666; font-size: 14px;">arXiv 2025</div> 
                        <div class="pub-links"> 
                            <a href="https://arxiv.org/abs/2502.15130" class="pub-btn">PDF</a>
                            <a href="https://github.com/chen-xw/TransMamba-main" class="pub-btn">Code</a>
                            <a href="https://github.com/chen-xw/TransMamba-main" class="pub-btn">Project Page</a>
                        </div>  
                    </div>    
                </div>   
            </li>
            
            <!-- 论文 4 示例 -->
            <li>
                <div class="pub-item">
                    <div class="pub-image">
                        <span class="pub-img-badge">ICCV 2023</span>
                        <img src="./image/drc.png" alt="MME-CoF Benchmark">
                    </div>
                    <div class="pub-content">
                        <!-- ... 内容保持不变 ... -->
                        <div class="pub-title-row">
                            <span class="badge tag-conf">ICCV 2023</span> <a href="https://arxiv.org/abs/2308.13305">Dynamic Residual Classifier for Class Incremental Learning</a> 
                        </div>
                        <div class="pub-authors">
                            Xiuwei Chen, Xiaobin Chang 
                        </div>
                        <div style="font-style: italic; color: #666; font-size: 14px;">ICCV 2023</div> 
                        <div class="pub-links"> 
                            <a href="https://arxiv.org/abs/2308.13305" class="pub-btn">PDF</a>
                            <a href="https://github.com/chen-xw/DRC-CIL" class="pub-btn">Code</a>
                            <a href="https://github.com/chen-xw/DRC-CIL" class="pub-btn">Project Page</a>
                        </div>  
                    </div>    
                </div>   
            </li>
            
        </ul>


        <div class="section-title">🎓 Educations</div> <ul class="custom-list">
            <li><span class="date-text">2024.09 - now,</span>  PhD Student, Sun Yat-sen University (SYSU) </li>
            <li><span class="date-text">2021.09 - 2024.06,</span>  Master of CS, Sun Yat-sen University (SYSU) </li>
            <li><span class="date-text">2017.09 - 2021.06,</span>  Bachelor of CS, The Taiyuan University of Technology (TYUT) </li>
        </ul>

        <div class="section-title">💼  Experiences</div> <ul class="custom-list">
            <li><span class="date-text">2025.08 - now,</span>  Research Intern, YinWang 2030 Lab, Supervisor: Hang Xu, Jianhua Han</li>
            <li><span class="date-text">2024.07 - 2025.07,</span>  Research Intern, Huawei Noah's Ark Lab, Supervisor: Hang Xu, Jianhua Han, Yihan Zeng </li>
            <li><span class="date-text">2023.06 - 2023.08,</span>  Algorithm Intern, Hikvision Research Institute, Supervisor: Jun Che </li>
        </ul>


        <p align="center" style="font-size: 13px; color: #999; margin-top: 60px; border-top: 1px solid #eaeaea; padding-top: 15px;">
            &copy; 2026 Xiuwei Chen. Last update: 2026.02.
        </p>

    </div>
</div>
