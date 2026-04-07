目前分为四大块:

第一块: 头像


1. 顶部导航栏（知识沉淀、时间轴、技术栈）
这部分定义了页面的跳转逻辑。

文件： index.html

代码区域： 找 <nav> 标签里的 .nav-links 部分。

具体代码：

HTML
<div class="nav-links">
  <a href="#opensource" data-i18n="nav.opensource">Knowledge</a>
  <a href="#timeline" data-i18n="nav.timeline">Timeline</a>
  <a href="#skills" data-i18n="nav.skills">Stack</a>
</div>
修改提示： 如果你想改导航的名字，去 zh.json 改 nav 下对应的字段；如果你想改跳转位置，改 href="#xxx"。

2. 头像（中间的圆图）
这部分负责你的“门面”。

文件： index.html

代码区域： 找 <section id="intro"> 里的 .avatar-container。

具体代码：

HTML
<img src="assets/images/Avatar.jpg" alt="Avatar" class="avatar" data-i18n="intro.avatarAlt">
修改提示： * 想换照片：把新照片丢进 assets/images 文件夹，然后把 src="..." 里的名字换掉。

想改光晕效果：找它下面的 <div class="avatar-glow"></div>。

3. 个人描述（“你好，我是李” 及 下方文字）
这部分是你的核心介绍。

文件： index.html

代码区域： 紧跟着头像下方的 <h1> 和 <p> 标签。

具体代码：

HTML
<h1 class="gradient-text" data-i18n="intro.title">Hello</h1>
<p class="subtitle" data-i18n="intro.desc">...</p>
核心修改点（划重点）：
你看到代码里写的是 Hello 和 ...，但网页显示的是中文。所以修改文字内容请去：lang/zh.json。

找 "intro": { "title": "...", "desc": "..." } 这一段。

desc 里的换行是用 <br> 标签实现的，可以直接在那里修改你的履历和邮箱。



4:修改头像下方的社交链接 (Bilibili 和 GitHub)
在 main.js 中找到 const CONTACT_LINKS 这一段（通常在文件的前 100 行内）：

JavaScript
  const CONTACT_LINKS = [
    { 
      icon: 'fab fa-bilibili', 
      key: 'contact.bilibili', 
      link: 'https://space.bilibili.com/385516781/upload/video' // <--- 修改这里的网址为你的 B 站主页
    },



第二块:知识库


📍 修改位置：lang/zh.json
打开这个文件，找到 "opensource" 这一层大括号，你会看到以下内容：

1. 修改大标题和按钮文字
JSON
"opensource": {
  "title": "技术沉淀与知识库",   // 这里改顶部的蓝色大标题
  "btnCode": "查阅文档",        // 如果卡片有代码链接，这是按钮文字
  "btnDoc": "在线访问",         // 你截图里看到的蓝色按钮文字
2. 修改具体的卡片内容（以第一个卡片为例）
往下看你会看到 item1, item2... 每一个 item 对应一个卡片：

JSON
  "item1": {
    "title": "Linux 排障实战手册", // 修改卡片标题
    "desc": "记录日常运维中遇到的...", // 修改卡片下方的详细描述
    "tags": ["Linux", "Troubleshooting", "运维实战"] // 修改卡片里的灰色标签
  },
💡 进阶：如果你想增加或减少卡片的“数量”？
如果你在 zh.json 里加了 item5，网页是不会自动变出来的。这时你需要配合修改 assets/js/main.js：

打开 main.js。

找到 const OPEN_SOURCE_ITEMS = [...]。

增加卡片：在数组里多加一行 { key: 'opensource.item5', linkCode: null, linkDoc: '#' }。

减少卡片：直接删掉不需要的那一行。


修改知识库卡片中的“在线访问”链接
在 main.js 中找到 const OPEN_SOURCE_ITEMS 这一段。目前我给你写的代码里，链接都是用 '#' 占位的，你需要把它们换成你实际的文档地址：

JavaScript
  const OPEN_SOURCE_ITEMS = [
    { 
      key: 'opensource.item1', // Linux 排障实战手册
      linkCode: null, 
      linkDoc: 'https://你的文档地址1.com' // <--- 修改这里
    },



第三块: 时间轴

1. 修改具体文字内容（日期、标题、描述）
所有的文字描述都在 lang/zh.json 文件里。

文件路径： lang/zh.json

查找关键词： "timeline"

代码结构：

JSON
"timeline": {
  "title": "经历时间轴",
  "event1": {
    "date": "2023.06-2025.01",
    "title": "加入安徽东科智行...",
    "desc": "负责公司各部门的终端设备维护..."
  },
  "event2": { ... },
  "event6": {
    "date": "2026.03",
    "title": "参加上海大学计算机科学成人本科开学式",
    "desc": " "
  }
}
修改提示： 你想改哪一段经历，就改对应的 eventX。比如要把“开学式”改成“正式上课”，直接改 event6 的 title 即可。

2. 修改显示顺序或增减经历
如果你想增加一个新的时间点，或者让时间轴“倒序”变“正序”，需要去 main.js。

文件路径： assets/js/main.js

查找变量： const TIMELINE_EVENTS

具体代码：

JavaScript
const TIMELINE_EVENTS = [
  'timeline.event6',  // 这一行在最上面
  'timeline.event5',
  'timeline.event4',
  'timeline.event3',
  'timeline.event2',
  'timeline.event1',  // 这一行在最下面
];
修改方法：

想删掉某一行： 直接在这里删掉对应的 'timeline.eventX'。

想调换顺序： 挪动这几行的位置。数组里排在前面的，网页上就显示在最上面。

想增加一行： 先在 zh.json 里写好 event7，然后在这里把 'timeline.event7' 加进数组。


第四块: 技术栈



1. 修改“大分类”的名字（如：操作系统与底层）
如果你想把“IT基础架构”改成“网络与服务”，需要去 lang/zh.json。

文件路径： lang/zh.json

查找关键词： "skills"

具体代码：

JSON
"skills": {
  "title": "技术栈",
  "os": "操作系统与底层",        // 修改这里
  "infrastructure": "IT基础架构", // 修改这里
  "cloud": "云原生与自动化",      // 修改这里
  "tools": "监控与运维工具"       // 修改这里
}
2. 修改“具体技能”和“图标”（如：Linux、Docker）
如果你想把 “Zabbix” 删掉换成 “Ansible”，或者换个图标，需要去 assets/js/main.js。

文件路径： assets/js/main.js

查找变量： const TECH_STACK

具体代码结构：

JavaScript
const TECH_STACK = [
  {
    category: 'skills.os', // 对应 zh.json 里的 "os"
    items: [
      { name: 'Linux (CentOS/Ubuntu)', icon: 'fab fa-linux' },
      { name: 'Windows Server', icon: 'fab fa-windows' },
      { name: 'Shell Script', icon: 'fas fa-terminal' },
      { name: 'Python', icon: 'fab fa-python' },
    ],
  },
  {
    category: 'skills.infrastructure',
    items: [
      { name: 'TCP/IP & DNS', icon: 'fas fa-network-wired' },
      // ... 剩下的以此类推
    ],
  },
  // ... 后面还有 cloud 和 tools 分类
];
🛠️ 进阶：如何更换图标？
代码里的 icon: 'fab fa-linux' 这种字样使用的是 Font Awesome 6 图标库。

想找新图标： 你可以去 Font Awesome 官网 搜索。

使用方法： 比如你想加个 Java，搜到后复制它的类名（例如 fa-brands fa-java），然后在代码里写 icon: 'fab fa-java'。

fab 开头的一般是品牌图标（如 Linux, Python）。

fas 开头的一般是通用形状（如 数据库 fa-database, 终端 fa-terminal）。
