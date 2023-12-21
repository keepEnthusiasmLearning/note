## vite-plugin-mock

**Install**

    $ npm i mockjs -S
    $ npm i vite-plugin-mock -D

**Config to `@/vite.config.ts`**

    import { viteMockServe } from 'vite-plugin-mock'
    export default {
        plugins: [
            viteMockServe({ 
                mockPath?: 'mock',                  // 指定引入的文件路径
                ignore?: ignore: /^_/,              // 忽略引入 '_' 开头的文件
                logger: true                        // 是否在控制台上显示请求日志
                localEnabled?: command === 'serve',
                prodEnabled?: command ！=='serve',
                /**调用 setupProdMockServer 开启 mock 数据**/ 
                injectCode?: `
                    import { setupProdMockServer } from '../mock/_createProductionServer';
                    setupProdMockServer();
                `,
            }),
        ]
    }

**MockMethod to `@/mock/mockModule.ts`**

    import { MockMethod } from 'vite-plugin-mock'
    export default [
        {
            url: string;                            // 请求地址 '/api/get'
            method?: MethodType;                    // 请求方法 'get' 'post'
            timeout?: number;                       // 请求时间 default: 200
            statusCode?:number;                     // 状态码
            response?: ((opt: {                     // 响应 JSON
                    [key: string]: string;          // { code: 0, data: { name: ' '}}
                    body: Record<string,any>; 
                    query: Record<string,any>, headers: Record<string, any>; 
                }) => any) | any;
            rawResponse?: (req: IncomingMessage, res: ServerResponse) => void;      // 响应 非 JSON
        },
    ] as MockMethod[]


**Create to `@/mock/mockProdServer.ts`**

    import { createProdMockServer } from 'vite-plugin-mock/es/createProdMockServer'

    /* 引入 mock 下所有 ts */
    const modules = import.meta.glob<Recordable>('./**/*.ts', { eager: true });

    /* 遍历 modules 忽略 '/_' 文件 */
    const mockModules: any[] = [];
    Object.keys(modules).forEach((key) => {
      if (key.includes('/_')) {
        return;
      }
      mockModules.push(...modules[key].default);
    });

    /* 传入 mockModules 创建服务器 */
    export function setupProdMockServer() {
      createProdMockServer(mockModules);
    }
