# 使用**vite**创建vue3项目

1.检查环境

+ 查看本机node.js环境

+ ```she
	node -v
	```

+ 查看npm版本

+ ```shell
	npm -v
	```

2.

+ 1.使用vite创建项目

+ ```bash
	npm init vue@latest my-project
	```

+ 2.使用vue-cli创建

+ ```bash
	vue create my-project
	```

## 常用依赖及配置

+ 1.axios

	+ 1.安装

		[起步 | Axios中文文档 ](https://www.axios-http.cn/docs/intro)

	+ 2.axios统一请求响应拦截器

		在src下新建utils/request.js

		```js
		import { userStore } from '@/stores/user'
		import axios from 'axios'
		import router from '@/router'
		import { ElMessage } from 'element-plus'
		
		const baseURL = ''
		
		const instance = axios.create({
		  baseURL,
		  timeout: 100000
		})
		
		//请求拦截器
		instance.interceptors.request.use(
		  (config) => {
		    const store = userStore()
		    if (store.token) {
		      config.headers.Authorization = store.token
		    }
		    return config
		  },
		  (err) => Promise.reject(err)
		)
		
		//响应拦截器
		instance.interceptors.response.use(
		  (res) => {
		    if (res.data.code === 0) {
		      return res
		    }
		    ElMessage({ message: res.data.message || '服务异常', type: 'error' })
		    return Promise.reject(res.data)
		  },
		  (err) => {
		    ElMessage({
		      message: err.response.data.message || '服务异常',
		      type: 'error'
		    })
		    console.log(err)
		    if (err.response?.status === 401) {
		      router.push('/login').then(() => {
		        console.log('跳转成功')
		      })
		    }
		    return Promise.reject(err)
		  }
		)
		
		export default instance
		export { baseURL }
		
		```

+ 2.element-plus

	+ 1.安装

		[安装 | Element Plus](https://element-plus.org/zh-CN/guide/installation.html#环境支持)

	+ 2.配置按需导入

		[按需导入](https://element-plus.org/zh-CN/guide/quickstart.html#按需导入)

+ 3.pinia持久化

	+ 1.安装

		```shell
		yarn add pinia
		# 或者使用 npm
		npm install pinia
		```

		安装持久化插件

		```shell
		yarn add pinia-plugin-persistedstate
		
		npm i pinia-plugin-persistedstate
		```

	+ 2.配置

		store下新建index.js

		统一管理pinia

		```javascript
		/**
		 * 统一管理pinia 导出
		 */
		import persist from 'pinia-plugin-persistedstate'
		import { createPinia } from 'pinia'
		
		const pinia = createPinia()
		pinia.use(persist)
		
		export default pinia
		```

+ 4.less/sass 

	按需引入





