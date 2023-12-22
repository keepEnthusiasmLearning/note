# Axios

**安装**

    $ npm i axios

**引入**

    const axios = require('axios').default;

## 语法

**基本语法**

    axios.get('/url', data).then(
      function (response) { console.log("请求成功时") }
    ).catch(
      function (error) { console.log("请求错误时") }
    ).finally(
      function () { console.log("总是执行") }
    );

**async/await 语法**

    export const request = async () => {
      try {
        const response = await axios.get('/url', data);
        console.log("请求成功时")
        return response
      } catch (error: any) { 
        console.log("请求错误时")
        return Promise.reject(error) 
      } 
    }

## Axios 实例

**创建实例**

    const instance = axios.create({
      baseURL: 'https://some-domain.com/api/',
      timeout: 1000,
      headers: {'X-Custom-Header': 'foobar'}
    });

**实例方法**

    axios.request(config)
    axios.get(url[, config])
    axios.delete(url[, config])
    axios.head(url[, config])   
    axios.options(url[, config])   
    axios.post(url[, data[, config]])   
    axios.put(url[, data[, config]])   
    axios.patch(url[, data[, config]])   
    axios.getUri([config])   

**AxiosRequestConfig 请求配置**

    {
      url: '/user'
      method: 'get'
      baseURL: 'https://some-domain.com/api/'
      transformRequest: [function(data){ return data }]
      headers: {'X-Requested-With': XMLHttpRequest}
      params: { ID: 12345 }
      paramsSerializer: function(params){ return Qs.stringify(params, {arrayFormat: 'brackets'}) }
      data: 'Country=Brasil&City=Belo Horizonte'
      timeout: 1000
      withCredentials: false
      adapter: function (config) {}
      auth: { username: 'janedoe', password: 's00pers3cret' }
      responseType: 'json'
      responseEncoding: 'utf8'
      xsrfCookieName: 'XSRF-TOKEN'
      xsrfHeaderName: 'X-XSRF-TOKEN'
      onUploadProgress: function (progressEvent) {}
      onDownloadProgress: function (progressEvent) {}
      maxContentLength: 2000
      maxBodyLength: 2000
      validateStatus: function (status) { return status >= 200 && status < 300 }
      maxRedirects: 5
      socketPath: null
      httpAgent: new http.Agent({ keepAlive: true })
      httpsAgent: new https.Agent({ keepAlive: true })
      cancelToken: new CancelToken(function (cancel) {})
      decompress: true
      proxy: {
          protocol: 'https',
          host: '127.0.0.1',
          port: 9000,
          auth: { username: 'mikeymike', password: 'rapunz3l' }
        }
      }
    }


## 拦截器 interceptors

在 `.then` 和 `.catch` 前拦截请求和响应

**拦截请求**

    axios.interceptors.request.use(
      (config) => {
        // 发送请求前做些事
      },
      (error) => { return Promise.reject(error) }
    )

**拦截响应**

    axios.interceptors.response.use(
      // 2xx 范围内的状态码都会触发该函数。
      (response) => {
        if (response.data.code === 200) {
          // Success
          return res;
        }
        if(response.data.code === 11001 || response.data.code === 11002){
          console.log("Illegal token")
        }
      },
      // 超出 2xx 范围的状态码都会触发该函数。422、500
      (error) => { return Promise.reject(error) }
    )