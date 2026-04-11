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
        padding: 20px 10px;
    }
    
    /* 左侧边栏 */
    .academic-sidebar {
        width: 260px;
        padding-right: 40px;
        margin-bottom: 30px;
    }
    .hp-photo {
        width: 200px;
        height: 200px;
        border-radius: 50%;
        object-fit: cover;
        margin-bottom: 15px;
        box-shadow: 0 4px 10px rgba(0,0,0,0.1);
    }
    .author-name { font-size: 26px; font-weight: 700; color: #222; margin-bottom: 5px; }
    .author-title { font-size: 14.5px; color: #555; margin-bottom: 20px; line-height: 1.4; }
    
    .contact-info { list-style: none; padding: 0; margin: 0; }
    .contact-info li { margin-bottom: 12px; font-size: 14.5px; display: flex; align-items: center; }
    .contact-info i { width: 20px; color: #444; text-align: center; margin-right: 10px; font-size: 16px; }
    .contact-info a { color: #333; text-decoration: none; transition: color 0.2s; }
    .contact-info a:hover { color: #1772d0; }

    /* 右侧主内容区 */
    .academic-main {
        flex: 1;
        min-width: 0;
    }
    .academic-main p { font-size: 15px; margin-bottom: 15px; text-align: justify; }
    .academic-main a { color: #1772d0; text-decoration: none; }
    .academic-main a:hover { text-decoration: underline; }
    
    /* 章节标题 */
    .section-title {
        font-size: 24px;
        font-weight: bold;
        margin-top: 35px;
        margin-bottom: 15px;
        border-bottom: 1px solid #eaeaea;
        padding-bottom: 8px;
        color: #222;
        display: flex;
        align-items: center;
    }
    .section-title i { margin-right: 10px; font-size: 22px; }

    /* 列表样式 (News & Projects) */
    ul.custom-list { list-style-type: none; padding-left: 0; margin-top: 0; }
    ul.custom-list li { margin-bottom: 12px; position: relative; padding-left: 18px; font-size: 14.5px; }
    ul.custom-list li::before { content: "•"; position: absolute; left: 0; color: #666; font-size: 18px; line-height: 1.4; }
    .date-text { font-style: italic; color: #555; margin-right: 5px; }

    /* 论文列表样式 */
    .pub-category { font-size: 18px; font-weight: bold; margin-top: 25px; margin-bottom: 15px; color: #333; }
    ul.pub-list { list-style: none; padding: 0; margin: 0; }
    ul.pub-list li { margin-bottom: 20px; font-size: 14.5px; }
    .pub-title-row { margin-bottom: 4px; }
    .pub-title-row a { font-weight: bold; color: #1772d0; }
    .pub-authors { color: #444; }
    .pub-authors strong { color: #111; font-weight: 700; }

    /* 漂亮的彩色标签 (Badges) */
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
    .tag-arxiv { background-color: #f59e0b; } /* 橙色 */
    .tag-conf { background-color: #8b5cf6; }  /* 紫色 */
    .tag-blog { background-color: #10b981; }  /* 绿色 */

    /* 手机端自适应响应式 */
    @media (max-width: 768px) {
        .academic-page { flex-direction: column; }
        .academic-sidebar { width: 100%; padding-right: 0; text-align: center; margin-bottom: 20px; }
        .contact-info li { justify-content: center; }
    }
</style>

<link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/5.15.3/css/all.min.css">

<div class="academic-page">

    <div class="academic-sidebar">
        <img class="hp-photo" src="./imgs/photo.jpg" alt="Xiuwei Chen">
        <div class="author-name">Xiuwei Chen</div>
        <div class="author-title">
            Ph.D. Candidate<br>
            HCP Group, SYSU
        </div>
        <ul class="contact-info">
            <li><i class="fas fa-map-marker-alt"></i> Guangzhou, China</li>
            <li><i class="fas fa-envelope"></i> <a href="mailto:chenxw83@mail2.sysu.edu.cn">Email</a></li>
            <li><i class="fas fa-graduation-cap"></i> <a href="https://scholar.google.com/">Google Scholar</a></li>
            <li><i class="fab fa-github"></i> <a href="https://github.com/chen-xw">Github</a></li>
            <li><i class="fas fa-file-pdf"></i> <a href="misc/CV_XiuweiChen.pdf">CV</a></li>
        </ul>
    </div>

    <div class="academic-main">
        
        <p>
            I am currently a Ph.D candidate in HCP Group at <a href="https://sai.sysu.edu.cn/">Sun Yat-sen University (SYSU)</a>, supervised by <a href="https://scholar.google.com/citations?user=voxznZAAAAAJ&hl=zh-CN">Prof. Xiaodan Liang</a>. I received my Master's degree at the <a href="https://www.sysu.edu.cn/">Sun Yat-sen University (SYSU)</a>, supervised by <a href="https://xb-chang.github.io/">Prof. Xiaobin Chang</a>. Prior to SYSU, I obtained a B.Eng from <a href="https://www.tyut.edu.cn/">TYUT</a> and majored in Computer Science and Technology (CS) in 2021.
        </p>
        <p>
            My research interests focus on <strong>Multimodal Reasoning</strong>, including Understanding and Self-Improvement. Prior to that, my focus was on <strong>Person Re-identification</strong> and <strong>Incremental Learning</strong>.
        </p>
        <p>
            I will be entering the job market in 2027. Please feel free to reach out if you have opportunities!
        </p>

        <div class="section-title">🔥 News</div>
        <ul class="custom-list">
            <li><span class="date-text">2025.12:</span> 🔥 Release <a href="https://arxiv.org/pdf/2512.05112">🎩 DraCo: Draft as CoT for Text-to-Image Preview and Rare Concept Generation</a>, an interleaved reasoning framework for improved image generation.</li>
            <li><span class="date-text">2025.10:</span> 🔥 Release <a href="https://arxiv.org/abs/2510.26802">Are Video Models Ready as Zero-Shot Reasoners?</a> An empirical study on the zero-shot reasoning capabilities of video models.</li>
            <li><span class="date-text">2025.10:</span> 🔥 Release <a href="https://github.com/ULMEvalKit/ULMEvalKit">UlmEvalkit</a>, an open-source toolkit for evaluating unified MLLMs and generative models for image generation tasks.</li>
            <li><span class="date-text">2025.09:</span> 🎉 Three papers (<a href="https://arxiv.org/abs/2505.00703">T2I-R1</a>, <a href="https://arxiv.org/abs/2506.05331">MINT-CoT</a>, and <a href="https://arxiv.org/abs/2506.05331">BLINK-Twice</a>) are accepted by NeurIPS 2025.</li>
            <li><span class="date-text">2024.09:</span> I have passed Ph.D. Qualifying Examination to become a Ph.D. candidate.</li>
        </ul>

        <div class="section-title">🛠️ Projects</div>
        <ul class="custom-list">
            <li>
                <a href="https://github.com/ULMEvalKit/ULMEvalKit" style="font-weight: bold;">UlmEvalkit: An open-source toolkit for evaluating unified large multi-modal models and generative models</a><br>
                <strong>Xiuwei Chen</strong>, Renrui Zhang, Yankai Shu, Yuyang Peng, Zhuofan Zong, Yuchen Duan, Zihao Wang, Jiaming Liu, Hao Chen, Ziyu Guo, Junyan Ye, Rui Liu, Pheng Ann Heng, Shanghang Zhang, Hongsheng Li.
            </li>
        </ul>

        <div class="section-title">📝 Publications</div>

        <div class="pub-category">o1/R1-like CoT Reasoning for Generation</div>
        <ul class="pub-list">
            <li>
                <div class="pub-title-row">
                    <span class="badge tag-arxiv">Arxiv</span> 
                    <a href="https://arxiv.org/pdf/2512.05112">DraCo: Draft as CoT for Text-to-Image Preview and Rare Concept Generation</a>
                </div>
                <div class="pub-authors">
                    <strong>Xiuwei Chen</strong>, Renrui Zhang, Haodong Li, Zhuofan Zong, Ziyu Guo, Jun He, Claire Guo, Junyan Ye, Rongyao Fang, Weijia Li, Rui Liu, Hongsheng Li.
                </div>
            </li>
            <li>
                <div class="pub-title-row">
                    <span class="badge tag-conf">NeurIPS 2025</span> 
                    <a href="https://arxiv.org/abs/2505.00703">T2I-R1: Reinforcing Image Generation with Collaborative Semantic-level and Token-level CoT</a>
                </div>
                <div class="pub-authors">
                    <strong>Xiuwei Chen</strong>*, Ziyu Guo*, Renrui Zhang*, Zhuofan Zong, Hao Li, Le Zhuo, Shilin Yan, Pheng-Ann Heng, Hongsheng Li.
                </div>
            </li>
            <li>
                <div class="pub-title-row">
                    <span class="badge tag-blog">Blog</span> 
                    <a href="https://picotrex.github.io/Awesome-Nano-Banana-images/">Nano-Consistent-150K</a>
                </div>
                <div class="pub-authors">
                    Junyan Ye, <strong>Xiuwei Chen</strong>, Zilong Huang, Jun He, Leqi Zhu, Zhiyuan Yan, Ruichuan An, Hongsheng Li, Conghui He, Weijia Li.
                </div>
            </li>
        </ul>

        <div class="pub-category">o1/R1-like CoT Reasoning for Understanding</div>
        <ul class="pub-list">
            <li>
                <div class="pub-title-row">
                    <span class="badge tag-conf">ICML 2025</span> 
                    <a href="https://arxiv.org/abs/2502.09621">MME-CoT: Benchmarking Chain-of-Thought in Large Multimodal Models for Reasoning Quality...</a>
                </div>
                <div class="pub-authors">
                    <strong>Xiuwei Chen</strong>*, Renrui Zhang*, Ziyu Guo, Yanwei Li, Yu Qi, Xinyan Chen, Liuhui Wang, Jianhan Jin, Claire Guo, Shen Yan, Bo Zhang, Chaoyou Fu, Peng Gao, Hongsheng Li.
                </div>
            </li>
            <li>
                <div class="pub-title-row">
                    <span class="badge tag-conf">ECCV 2024</span> 
                    <a href="https://arxiv.org/pdf/2403.14624.pdf">MathVerse: Does Your Multi-modal LLM Truly See the Diagrams in Visual Math Problems?</a>
                </div>
                <div class="pub-authors">
                    Renrui Zhang*, <strong>Xiuwei Chen</strong>*, Yichi Zhang*, Haokun Lin, Ziyu Guo, Pengshuo Qiu, Aojun Zhou, Pan Lu, Aojun Zhou, Kai-Wei Chang, Peng Gao, Hongsheng Li.
                </div>
            </li>
        </ul>

        <p align="center" style="font-size: 13px; color: #999; margin-top: 60px; border-top: 1px solid #eaeaea; padding-top: 15px;">
            &copy; 2024 Xiuwei Chen. Last update: 2024.05.
        </p>

    </div>
</div>
