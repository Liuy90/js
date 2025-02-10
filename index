const express = require('express');
const axios = require('axios');

const app = express();
const PORT = process.env.PORT || 3000;

app.use(express.json());

// 解析抖音链接的路由
app.post('/parse', async (req, res) => {
  const { url } = req.body;

  if (!url) {
    return res.status(400).json({
      success: false,
      message: '请提供抖音视频链接',
    });
  }

  try {
    // 调用第三方 API 解析抖音链接
    const apiUrl = `https://api.douyin.wtf/api?url=${encodeURIComponent(url)}`;
    const response = await axios.get(apiUrl);

    if (response.data && response.data.video_url) {
      return res.json({
        success: true,
        videoUrl: response.data.video_url,
      });
    } else {
      return res.status(500).json({
        success: false,
        message: '无法解析视频链接',
      });
    }
  } catch (error) {
    console.error('解析失败:', error);
    return res.status(500).json({
      success: false,
      message: '解析失败，请稍后重试',
    });
  }
});

// 启动服务器
app.listen(PORT, () => {
  console.log(`服务器正在运行，访问地址：http://localhost:${PORT}`);
});
