---
title: Elog配置详解
date: '2024-05-15 23:12:55'
updated: '2024-05-16 00:14:32'
---

# Elog配置详解
参考 [Elog 文档](https://elog.1874.cool/)，本博客的 Elog 的配置如下：
```javascript
module.exports = {
  write: {
    platform: 'yuque',
    // Token 模式（需要语雀超级会员）
    yuque: {
      token: process.env.YUQUE_TOKEN,
      login: process.env.YUQUE_LOGIN,
      repo: process.env.YUQUE_REPO,
      onlyPublic: false,
      onlyPublished: true,
    },
    // 账号密码模式
    "yuque-pwd": {
      username: process.env.YUQUE_USERNAME,
      password: process.env.YUQUE_PASSWORD,
      login: process.env.YUQUE_LOGIN,
      repo: process.env.YUQUE_REPO,
    }
  },
  deploy: {
    platform: 'local',
    local: {
      outputDir: './source/_posts',
      filename: 'title',
      format: 'markdown',
      catalog: false,
      frontMatter: {
        enable: true,
        include: ['categories', 'tags', 'title', 'date', 'updated', 'permalink', 'cover', 'description'],
        timeFormat: true,
      }
    }
  },
  image: {
    enable: true,
    platform: 'local',
    local: {
      outputDir: './source/images',
      prefixKey: '/images'
    }
  },
}

```

## 语雀配置
{% note warning %}
Token 模式或者账号密码模式二选一即可，默认为账号密码模式，如果需要切换为 Token 模式，则修改`platform`为`yuque`即可
{% endnote %}
```javascript
write: {
    platform: 'yuque-pwd',
    yuque: { // Token 模式
      token: process.env.YUQUE_TOKEN,
      login: process.env.YUQUE_LOGIN,
      repo: process.env.YUQUE_REPO,
      onlyPublic: false,
      onlyPublished: true,
    },
    "yuque-pwd": { // 账号密码模式
      username: process.env.YUQUE_USERNAME,
      password: process.env.YUQUE_PASSWORD,
      login: process.env.YUQUE_LOGIN,
      repo: process.env.YUQUE_REPO,
      linebreak: false
    }
  },
```

- `token`为语雀Token，可从[此处](https://elog.1874.cool/notion/gvnxobqogetukays#token)获取
- `username`为语雀账号，一般为手机号
- `password`为语雀登录密码，如果没有设置过，可在账号设置中进行设置
- `login`为语雀路径，可从[此处](https://elog.1874.cool/notion/gvnxobqogetukays#login)获取
- `repo`为语雀仓库短名称，可从[此处](https://elog.1874.cool/notion/gvnxobqogetukays#repo)获取
- `onlyPublic`表示是否只下载互联网公开文档
- `onlyPublished`表示是否只下载已发布文档

## 本地配置
```javascript
local: {
  outputDir: './source/_posts',
    filename: 'title',
    format: 'markdown',
    catalog: false,
    frontMatter: {
      enable: true,
      include: ['categories', 'tags', 'title', 'date', 'updated', 'permalink', 'cover', 'description'],
      timeFormat: true,
    }
}
```

- `outputDir`表示文档的存放位置为项目根目录下的`docs/docs`文件夹中
- `filename`表示文档将以数据库的 `title` 字段命名，也就是文档名
- `format`表示文档将以 markdown 的形式保存
- `frontMatter.enable`表示在 markdown 文档开头添加 Front Matter
- `frontMatter.include`表示只输出数组中存在的字段，数据库的其他字段忽略

## 图床配置
```javascript
local: {
  outputDir: './source/images',
  prefixKey: '/images'
}
```

- `outputDir`表示图片的存放位置为项目根目录下的`source/images`文件夹中
- `prefixKey=/images`表示图片的统一前缀为`/images`，因为 Hexo 会将`source/images`文件夹视为[静态资源根目录](https://hexo.io/zh-cn/docs/asset-folders)，统一将图片放在这里，并指定图片前缀，Hexo 才能找到此图片

## 更多 Elog 配置详情，请阅读 [Elog 文档](https://elog.1874.cool/)
