<script setup>
import { ref, onMounted, onUnmounted, nextTick } from 'vue'

// 假数据 - 20条发版记录
const releases = ref([
  {
    id: 'release-1',
    date: '2024-12-15',
    title: 'v2.1.0 重大功能更新',
    content: `
      <h3>新功能</h3>
      <ul>
        <li>新增用户画像分析功能，支持多维度数据统计</li>
        <li>优化首页推荐算法，点击率提升 15%</li>
        <li>新增暗黑模式自适应切换</li>
      </ul>
      <h3>性能优化</h3>
      <ul>
        <li>首屏加载时间缩短 30%</li>
        <li>图片懒加载策略优化</li>
        <li>接口请求合并，减少网络开销</li>
      </ul>
      <h3>Bug 修复</h3>
      <ul>
        <li>修复 iOS 系统下日期选择器异常问题</li>
        <li>修复登录页面白屏闪烁问题</li>
        <li>修复某些机型上拉加载数据重复问题</li>
      </ul>
    `
  },
  {
    id: 'release-2',
    date: '2024-12-01',
    title: 'v2.0.5 体验优化',
    content: `
      <h3>功能优化</h3>
      <ul>
        <li>搜索结果支持按时间/热度排序</li>
        <li>个人信息页改版，展示更清晰</li>
        <li>消息推送策略优化，减少打扰</li>
      </ul>
      <h3>界面调整</h3>
      <ul>
        <li>底部导航栏图标重新设计</li>
        <li>列表卡片增加阴影层次感</li>
        <li>按钮交互反馈优化</li>
      </ul>
    `
  },
  {
    id: 'release-3',
    date: '2024-11-20',
    title: 'v2.0.4 修复更新',
    content: `
      <h3>问题修复</h3>
      <ul>
        <li>修复特定网络环境下图片加载失败问题</li>
        <li>修复 Android 12 系统兼容性问题</li>
        <li>修复音频播放中断后无法续播问题</li>
        <li>修复长文本复制时丢失换行符问题</li>
      </ul>
    `
  },
  {
    id: 'release-4',
    date: '2024-11-10',
    title: 'v2.0.3 小版本更新',
    content: `
      <h3>功能增强</h3>
      <ul>
        <li>分享功能支持生成分享海报</li>
        <li>收藏夹支持分类管理</li>
        <li>搜索历史记录云端同步</li>
      </ul>
      <h3>其他优化</h3>
      <ul>
        <li>内存占用降低 20%</li>
        <li>应用启动速度提升</li>
      </ul>
    `
  },
  {
    id: 'release-5',
    date: '2024-10-28',
    title: 'v2.0.2 问题修复',
    content: `
      <h3>Bug 修复</h3>
      <ul>
        <li>修复分享到微信无法打开问题</li>
        <li>修复夜间模式切换闪烁问题</li>
        <li>修复输入法弹起布局错乱问题</li>
        <li>修复 Wi-Fi 与移动网络切换数据丢失问题</li>
      </ul>
    `
  },
  {
    id: 'release-6',
    date: '2024-10-15',
    title: 'v2.0.1 稳定更新',
    content: `
      <h3>稳定性提升</h3>
      <ul>
        <li>优化内存管理，减少内存泄漏</li>
        <li>提升接口请求成功率</li>
        <li>优化页面切换流畅度</li>
      </ul>
    `
  },
  {
    id: 'release-7',
    date: '2024-10-01',
    title: 'v2.0.0 重大版本更新',
    content: `
      <h3>全新架构</h3>
      <ul>
        <li>底层架构全面重构，性能大幅提升</li>
        <li>采用全新的组件化设计方案</li>
        <li>引入状态管理库，数据流更清晰</li>
      </ul>
      <h3>新功能</h3>
      <ul>
        <li>全新的个人中心界面</li>
        <li>智能推荐系统 2.0</li>
        <li>支持深色模式</li>
        <li>新增数据看板功能</li>
      </ul>
      <h3>迁移说明</h3>
      <p>旧版本用户数据已自动迁移，请放心更新。如遇问题可在设置中提交反馈。</p>
    `
  },
  {
    id: 'release-8',
    date: '2024-09-18',
    title: 'v1.9.5 体验优化',
    content: `
      <h3>用户体验</h3>
      <ul>
        <li>优化登录注册流程，减少操作步骤</li>
        <li>表单输入增加实时校验提示</li>
        <li>错误提示信息更友好</li>
      </ul>
    `
  },
  {
    id: 'release-9',
    date: '2024-09-05',
    title: 'v1.9.4 小版本更新',
    content: `
      <h3>功能优化</h3>
      <ul>
        <li>搜索功能支持模糊匹配</li>
        <li>历史记录支持一键清空</li>
        <li>支持自定义首页快捷入口</li>
      </ul>
    `
  },
  {
    id: 'release-10',
    date: '2024-08-22',
    title: 'v1.9.3 问题修复',
    content: `
      <h3>Bug 修复</h3>
      <ul>
        <li>修复某些图片无法显示缩略图问题</li>
        <li>修复分页加载数据错乱问题</li>
        <li>修复评论功能异常问题</li>
        <li>修复通知栏点击无法跳转问题</li>
      </ul>
    `
  },
  {
    id: 'release-11',
    date: '2024-08-10',
    title: 'v1.9.2 功能更新',
    content: `
      <h3>新功能</h3>
      <ul>
        <li>新增视频倍速播放功能</li>
        <li>支持离线缓存管理</li>
        <li>新增字体大小调节</li>
      </ul>
    `
  },
  {
    id: 'release-12',
    date: '2024-07-28',
    title: 'v1.9.1 体验优化',
    content: `
      <h3>体验优化</h3>
      <ul>
        <li>页面加载骨架屏优化</li>
        <li>下拉刷新动效优化</li>
        <li>按钮点击反馈优化</li>
      </ul>
    `
  },
  {
    id: 'release-13',
    date: '2024-07-15',
    title: 'v1.9.0 功能大更新',
    content: `
      <h3>重磅功能</h3>
      <ul>
        <li>全新会员体系上线</li>
        <li>新增创作者中心功能</li>
        <li>支持话题标签系统</li>
        <li>新增草稿箱功能</li>
      </ul>
      <h3>其他更新</h3>
      <ul>
        <li>个人主页支持自定义背景</li>
        <li>支持绑定第三方账号</li>
      </ul>
    `
  },
  {
    id: 'release-14',
    date: '2024-07-01',
    title: 'v1.8.5 稳定更新',
    content: `
      <h3>稳定性</h3>
      <ul>
        <li>修复偶发的崩溃问题</li>
        <li>优化内存占用</li>
        <li>提升接口响应速度</li>
      </ul>
    `
  },
  {
    id: 'release-15',
    date: '2024-06-20',
    title: 'v1.8.4 问题修复',
    content: `
      <h3>Bug 修复</h3>
      <ul>
        <li>修复登录超时后无法自动重连问题</li>
        <li>修复图片上传失败无提示问题</li>
        <li>修复特定机型卡顿问题</li>
      </ul>
    `
  },
  {
    id: 'release-16',
    date: '2024-06-08',
    title: 'v1.8.3 小版本更新',
    content: `
      <h3>功能优化</h3>
      <ul>
        <li>评论支持@好友</li>
        <li>支持消息免打扰设置</li>
        <li>新增账号安全检测功能</li>
      </ul>
    `
  },
  {
    id: 'release-17',
    date: '2024-05-25',
    title: 'v1.8.2 问题修复',
    content: `
      <h3>问题修复</h3>
      <ul>
        <li>修复支付流程中断问题</li>
        <li>修复推送通知延迟问题</li>
        <li>修复某些页面返回按钮失效问题</li>
      </ul>
    `
  },
  {
    id: 'release-18',
    date: '2024-05-12',
    title: 'v1.8.1 体验优化',
    content: `
      <h3>体验优化</h3>
      <ul>
        <li>优化首次加载引导流程</li>
        <li>改进新手教程交互</li>
        <li>提升列表滚动流畅度</li>
      </ul>
    `
  },
  {
    id: 'release-19',
    date: '2024-04-28',
    title: 'v1.8.0 新功能上线',
    content: `
      <h3>新功能</h3>
      <ul>
        <li>新增直播功能</li>
        <li>支持短视频拍摄与编辑</li>
        <li>新增积分商城</li>
        <li>支持私信功能</li>
      </ul>
      <h3>重要提示</h3>
      <p>新版本需要获取相机和麦克风权限才能使用拍摄功能。</p>
    `
  },
  {
    id: 'release-20',
    date: '2024-04-10',
    title: 'v1.7.5 最终版本',
    content: `
      <h3>版本说明</h3>
      <p>这是 1.7 系列的最终版本，我们将继续维护该版本的稳定性。</p>
      <h3>修复内容</h3>
      <ul>
        <li>修复已知问题</li>
        <li>优化核心功能</li>
      </ul>
      <h3>感谢</h3>
      <p>感谢所有用户的支持与反馈，欢迎升级到最新版本体验更多功能。</p>
    `
  }
])

const activeId = ref('release-1')
const contentRef = ref(null)
const navRef = ref(null)
let observer = null
let scrollTimeout = null
let isScrolling = false

// 点击左侧导航
const scrollToRelease = (id) => {
  // 滚动锁定，防止 Observer 干扰
  isScrolling = true
  clearTimeout(scrollTimeout)
  
  const targetEl = document.getElementById(id)
  if (targetEl) {
    targetEl.scrollIntoView({ behavior: 'smooth', block: 'start' })
    activeId.value = id
  }
  
  // 滚动动画结束后解锁（smooth 滚动约 300-500ms）
  scrollTimeout = setTimeout(() => {
    isScrolling = false
  }, 500)
}

// 监听滚动事件，用于检测手动滚动
const handleScroll = () => {
  isScrolling = true
  clearTimeout(scrollTimeout)
  scrollTimeout = setTimeout(() => {
    isScrolling = false
  }, 150)
}

// 初始化 Intersection Observer
const initObserver = () => {
  const options = {
    root: null,
    rootMargin: '-40% 0px -40% 0px',
    threshold: 0
  }

  observer = new IntersectionObserver((entries) => {
    // 如果正在滚动，不更新高亮
    if (isScrolling) return
    
    const visibleEntries = entries.filter(entry => entry.isIntersecting)
    
    if (visibleEntries.length > 0) {
      const topEntry = visibleEntries.reduce((prev, current) => {
        return prev.boundingClientRect.top < current.boundingClientRect.top ? prev : current
      })
      activeId.value = topEntry.target.id
      
      nextTick(() => {
        const navItem = navRef.value?.querySelector(`[data-id="${topEntry.target.id}"]`)
        if (navItem) {
          navItem.scrollIntoView({ behavior: 'smooth', block: 'nearest' })
        }
      })
    }
  }, options)

  releases.value.forEach(release => {
    const el = document.getElementById(release.id)
    if (el) observer.observe(el)
  })
}

onMounted(() => {
  nextTick(() => {
    initObserver()
    if (contentRef.value) {
      contentRef.value.addEventListener('scroll', handleScroll)
    }
  })
})

onUnmounted(() => {
  if (observer) {
    observer.disconnect()
  }
  clearTimeout(scrollTimeout)
  if (contentRef.value) {
    contentRef.value.removeEventListener('scroll', handleScroll)
  }
})
</script>

<template>
  <div class="release-page">
    <header class="page-header">
      <h1>发版详情</h1>
    </header>

    <div class="page-content">
      <!-- 左侧导航 -->
      <aside class="sidebar">
        <div class="sidebar-header">
          <span class="sidebar-title">目录</span>
        </div>
        <nav class="nav-list" ref="navRef">
          <div
            v-for="release in releases"
            :key="release.id"
            :data-id="release.id"
            class="nav-item"
            :class="{ active: activeId === release.id }"
            @click="scrollToRelease(release.id)"
          >
            <span class="nav-dot"></span>
            <span class="nav-text">{{ release.date }}</span>
          </div>
        </nav>
      </aside>

      <!-- 右侧内容 -->
      <main class="content" ref="contentRef">
        <div class="content-inner">
          <article
            v-for="release in releases"
            :key="release.id"
            :id="release.id"
            class="release-card"
          >
            <div class="release-header">
              <span class="release-date">{{ release.date }}</span>
              <h2 class="release-title">{{ release.title }}</h2>
            </div>
            <div class="release-body" v-html="release.content"></div>
          </article>
        </div>
      </main>
    </div>
  </div>
</template>

<style scoped>
.release-page {
  height: 100vh;
  display: flex;
  flex-direction: column;
  background: #f5f7fa;
}

.page-header {
  height: 60px;
  background: #fff;
  border-bottom: 1px solid #e8ecf0;
  display: flex;
  align-items: center;
  padding: 0 24px;
  flex-shrink: 0;
}

.page-header h1 {
  font-size: 20px;
  font-weight: 600;
  color: #1a1a2e;
  margin: 0;
}

.page-content {
  flex: 1;
  display: flex;
  overflow: hidden;
}

.sidebar {
  width: 200px;
  flex-shrink: 0;
  background: #fff;
  border-right: 1px solid #e8ecf0;
  display: flex;
  flex-direction: column;
}

.sidebar-header {
  padding: 16px;
  border-bottom: 1px solid #e8ecf0;
}

.sidebar-title {
  font-size: 14px;
  font-weight: 600;
  color: #666;
}

.nav-list {
  flex: 1;
  overflow-y: auto;
  padding: 8px 0;
}

.nav-item {
  display: flex;
  align-items: center;
  padding: 10px 16px;
  cursor: pointer;
  transition: all 0.2s;
  border-left: 3px solid transparent;
}

.nav-item:hover {
  background: #f0f4f8;
}

.nav-item.active {
  background: #e8f4ff;
  border-left-color: #3b82f6;
}

.nav-dot {
  width: 6px;
  height: 6px;
  border-radius: 50%;
  background: #c0c6d0;
  margin-right: 10px;
  transition: all 0.2s;
}

.nav-item.active .nav-dot {
  background: #3b82f6;
  box-shadow: 0 0 0 3px rgba(59, 130, 246, 0.2);
}

.nav-text {
  font-size: 13px;
  color: #666;
  transition: all 0.2s;
}

.nav-item.active .nav-text {
  color: #3b82f6;
  font-weight: 500;
}

.content {
  flex: 1;
  overflow-y: auto;
  padding: 24px;
}

.content-inner {
  max-width: 800px;
  margin: 0 auto;
}

.release-card {
  background: #fff;
  border-radius: 12px;
  padding: 24px;
  margin-bottom: 24px;
  box-shadow: 0 2px 8px rgba(0, 0, 0, 0.04);
  transition: box-shadow 0.3s;
}

.release-card:hover {
  box-shadow: 0 4px 16px rgba(0, 0, 0, 0.08);
}

.release-header {
  margin-bottom: 20px;
  padding-bottom: 16px;
  border-bottom: 1px solid #f0f2f5;
}

.release-date {
  display: inline-block;
  font-size: 12px;
  color: #999;
  background: #f5f7fa;
  padding: 4px 10px;
  border-radius: 4px;
  margin-bottom: 10px;
}

.release-title {
  font-size: 18px;
  font-weight: 600;
  color: #1a1a2e;
  margin: 0;
}

.release-body {
  font-size: 14px;
  line-height: 1.8;
  color: #4a5568;
}

.release-body :deep(h3) {
  font-size: 15px;
  font-weight: 600;
  color: #2d3748;
  margin: 20px 0 12px 0;
}

.release-body :deep(h3:first-child) {
  margin-top: 0;
}

.release-body :deep(ul) {
  margin: 0;
  padding-left: 20px;
}

.release-body :deep(li) {
  margin-bottom: 8px;
}

.release-body :deep(p) {
  margin: 12px 0;
}

.content::-webkit-scrollbar,
.nav-list::-webkit-scrollbar {
  width: 6px;
}

.content::-webkit-scrollbar-track,
.nav-list::-webkit-scrollbar-track {
  background: transparent;
}

.content::-webkit-scrollbar-thumb,
.nav-list::-webkit-scrollbar-thumb {
  background: #d0d5dd;
  border-radius: 3px;
}

.content::-webkit-scrollbar-thumb:hover,
.nav-list::-webkit-scrollbar-thumb:hover {
  background: #b0b8c4;
}
</style>
