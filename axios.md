# Axios

**导入**

    const axios = require('axios').default;

**User: 向给定ID的用户发起请求**

    axios.get('/user?ID=12345')
      .then(function (response) { console.log(response); })   // 处理成功情况
      .catch(function (error) { console.log(error); })        // 处理错误情况
      .finally(function () {});                               // 总是会执行 

    axios.get('/user', { params: { ID: 12345 } }).then().catch().finally();  

**async/await 写法**

    async function getUser() {
      try {
        const response = await axios.get('/user?ID=12345');
        console.log(response);
      } catch (error) {}
    }    

## Axios 实例

**创建实例**

    const instance = axios.create({
      baseURL: 'https://some-domain.com/api/',
      timeout: 1000,
      headers: {'X-Custom-Header': 'foobar'}
    });

**实例方法**

- `axios.request(config)`
- `axios.get(url[, config])`
- `axios.delete(url[, config])`
- `axios.head(url[, config])`   
- `axios.options(url[, config])`   
- `axios.post(url[, data[, config]])`   
- `axios.put(url[, data[, config]])`   
- `axios.patch(url[, data[, config]])`   
- `axios.getUri([config])`   

## 请求配置 AxiosRequestConfig

- `url: '/user'`
- `method: 'get'`
- `baseURL: 'https://some-domain.com/api/'`
- `transformRequest: [function(data){ return data }]`
- `headers: {'X-Requested-With': XMLHttpRequest}`
- `params: { ID: 12345 }`
- `paramsSerializer: function(params){ return Qs.stringify(params, {arrayFormat: 'brackets'}) }`
- `data: 'Country=Brasil&City=Belo Horizonte'`
- timeout: 1000
- withCredentials: false
- adapter: function (config) {}
- auth: { username: 'janedoe', password: 's00pers3cret' }
- responseType: 'json'
- responseEncoding: 'utf8'
- xsrfCookieName: 'XSRF-TOKEN'
- xsrfHeaderName: 'X-XSRF-TOKEN'
- onUploadProgress: function (progressEvent) {}
- onDownloadProgress: function (progressEvent) {}
- maxContentLength: 2000
- maxBodyLength: 2000
- validateStatus: function (status) { return status >= 200 && status < 300 }
- maxRedirects: 5
- socketPath: null
- httpAgent: new http.Agent({ keepAlive: true })
- httpsAgent: new https.Agent({ keepAlive: true })
- 
```
proxy: {
    protocol: 'https',
    host: '127.0.0.1',
    port: 9000,
    auth: {
      username: 'mikeymike',
      password: 'rapunz3l'
    }
  }
```
- `cancelToken: new CancelToken(function (cancel) {})`
- `decompress: true`

## 拦截器 interceptors

请求或响应被 then 或 catch 处理前拦截

    axios.interceptors.request.use(
      function (config) {
        return config;  // 在发送请求之前做些什么
      },
      function(error) {
        return Promise.reject(error);   // 对请求错误做些什么
      }
    )
    // 移除拦截器
    axios.interceptors.request.eject(myInterceptor);